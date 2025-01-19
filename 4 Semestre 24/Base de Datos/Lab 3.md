
### Tablas:
```sql
Ubicaciones(  
id_ubicacion INT PRIMARY KEY,  
ciudad VARCHAR(100) NOT NULL,  
pais VARCHAR(100) NOT NULL  
);
  
Restaurantes(  
id_restaurante INT PRIMARY KEY,  
nombre VARCHAR(100) NOT NULL,  
direccion TEXT NOT NULL,  
id_ubicacion INT NOT NULL,  
FOREIGN KEY (id_ubicacion) REFERENCES Ubicaciones(id_ubicacion)  
);
  
Categorías(  
id_categoria INT PRIMARY KEY,  
nombre VARCHAR(50) NOT NULL  
); 
 
Platos(  
id_plato INT PRIMARY KEY,  
nombre VARCHAR(100) NOT NULL,  
precio DECIMAL(10, 2) NOT NULL,  
id_restaurante INT NOT NULL,  
id_categoria INT NOT NULL,  
FOREIGN KEY (id_restaurante) REFERENCES Restaurantes(id_restaurante),  
FOREIGN KEY (id_categoria) REFERENCES Categorías(id_categoria)  
);  

Clientes(  
id_cliente INT PRIMARY KEY,  
nombre VARCHAR(100) NOT NULL,  
correo VARCHAR(150) UNIQUE NOT NULL  
);

Valoraciones(  
id_valoracion INT PRIMARY KEY,  
id_cliente INT NOT NULL,  
id_plato INT NOT NULL,  
calificacion INT CHECK (calificacion BETWEEN 1 AND 5),  
comentario TEXT,  
FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente),  
FOREIGN KEY (id_plato) REFERENCES Platos(id_plato)  
);
```

---
### Funciones

1. Calcular el promedio de calificaciones de un plato
```sql
CREATE OR REPLACE FUNCTION prom(idPlato INT)
RETURNS DECIMAL AS $$
DECLARE promedio DECIMAL;
BEGIN

SELECT AVG(calificacion) INTO promedio
FROM Valoraciones
WHERE idPlato = Valoraciones.id_plato;

RETURN promedio;

END;
$$ LANGUAGE plpgsql;
```

2. Verificar si un cliente ya hizo una valoración para un plato
```sql
CREATE OR REPLACE FUNCTION verfClient(idClient INT , idPlato INT)
RETURNS BOOLEAN AS $$
BEGIN

IF EXISTS(
SELECT 1 
FROM Valoraciones
WHERE id_cliente = idClient AND id_plato = idPlato;
) THEN
	RETURN TRUE;
ELSE
	RETURN FALSE;
END IF;

END;
$$ LANGUAGE plpgsql;
```
### Procedimientos

3. Actualizar precios de platos por un porcentaje
```sql
CREATE OR REPLACE PROCEDURE precioAct(porcentaje INT, idPlato INT)
LANGUAGE plpgsql AS $$
BEGIN

UPDATE Platos
SET precio = precio * (1 + (porcentaje / 100));
WHERE idPlato = id_plato;

RAISE NOTICE 'El plato se actualizo en un % porciento, quedando en %', porcentaje, precio;

END $$;
```

4. Listar platos con sus valoraciones usando un cursor
```sql
CREATE OR REPLACE PROCEDURE listPlato()
LANGUAGE plpgsql AS $$
DECLARE

idPlato INT
calft INT

mouse CURSOR FOR SELECT id_plato, calificacion FROM Valoraciones;

BEGIN

	OPEN mouse;
	
	LOOP
	
		FETCH mouse INTO idPlato, calft;
		
		EXIT WHEN NOT FOUND;

		RAISE NOTICE 'Id del plato : % , Calificación : %', idPlato, calft;
	END LOOP;

	CLOSE mouse;

END $$;
```
### Trigger

5. Validar calificación antes de insertar (asegurarse que las calificaciones están dentro del  
rango 1-5)
```sql
CREATE OR REPLACE FUNCTION validation()
RETURNS TRIGGER AS $$
BEGIN
	IF (NEW.calificacion > 5 OR NEW.calificacion < 1) THEN
	RAISE EXCEPTION 'ERROR DE VALORES: La calificación debe estar entre 1 y 5'
	END IF;

	RETURN NEW;
END
$$ LANGUAGE plpgsql;

CREATE TRIGGER validationTrigger
BEFORE INSERT
ON Valoraciones
FOR EACH ROW
EXECUTE FUNCTION validation();
```

6. Actualizar el promedio de calificaciones del restaurante al insertar o eliminar una  
valoración usando cursores
```sql
CREATE OR REPLACE FUNCTION actualizarProm()
RETURNS TRIGGER AS $$
DECLARE
    total_calificaciones NUMERIC := 0;
    cantidad_calificaciones INT := 0;
    nuevo_promedio NUMERIC := 0;
BEGIN
    -- Calcular el total y la cantidad de calificaciones para el restaurante
    SELECT COALESCE(SUM(V.calificacion), 0), COUNT(V.calificacion)
    INTO total_calificaciones, cantidad_calificaciones
    FROM Valoraciones V
    INNER JOIN Platos P ON V.id_plato = P.id_plato
    WHERE P.id_restaurante = (
        SELECT id_restaurante
        FROM Platos
        WHERE id_plato = COALESCE(NEW.id_plato, OLD.id_plato)
        LIMIT 1
    );

    -- Calcular el nuevo promedio
    IF cantidad_calificaciones > 0 THEN
        nuevo_promedio := total_calificaciones / cantidad_calificaciones;
    ELSE
        nuevo_promedio := 0; -- Sin calificaciones, promedio es 0
    END IF;

    -- Actualizar el promedio en la tabla Restaurantes
    UPDATE Restaurantes
    SET promedio_calificaciones = nuevo_promedio
    WHERE id_restaurante = (
        SELECT id_restaurante
        FROM Platos
        WHERE id_plato = COALESCE(NEW.id_plato, OLD.id_plato)
        LIMIT 1
    );

    RETURN NULL; -- El trigger no altera las filas directamente
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER actualizarPromTrigger
AFTER INSERT OR DELETE OR UPDATE
ON Valoraciones
FOR EACH ROW
EXECUTE FUNCTION actualizarProm();
```
