
### Enunciado

Las galerías de arte mantienen información acerca de artistas, sus nombres (que son únicos),  
lugares de nacimiento, edad, y estilo de arte. Para cada pieza de arte, se almacena: el artista,  
el a ̃no que fue hecha, el título (único), tipo de arte (por ejemplo pintura, litografía, escultura,  
fotografía), y también el precio. Las piezas de arte también son clasificadas en grupos de varios tipos, por ejemplo, retratos, vida, obras de Picasso, o trabajos del siglo 19 ; una pieza de arte puede pertenecer a m ́as de un grupo. Cada grupo es identificado por su nombre (como los  
dados anteriormente) que describe al grupo. 
### Solicitado
```sql
Artista{
Nombre
Lugar_Nacimiento
Edad
Estilo_Arte
}

Pieza_Arte{
Titulo
Nombre_Artista
Año
Tipo_Arte
Precio
}

Grupo{
id
nombre
descripcion
}

Pertenece{
id_grupo
titulo
}
```

### Crear tablas
```sql
CREATE TABLE Artista{
Nombre VARCHAR(20) PRIMARY KEY,
Lugar_Nacimiento VARCHAR(20) NOT NULL,
Edad INT NOT NULL,
Estilo_Arte VARCHAR(20) NOT NULL
}

CREATE TABLE Pieza_Arte{
Titulo VARCHAR(20) PRIMARY KEY,
Nombre_Artista VARCHAR(20) NOT NULL,
Anho INT NOT NULL,
Tipo_Arte VARCHAR(20) NOT NULL,
Precio INT NOT NULL
FOREIGN KEY (Nombre_Artista) REFERENCE Artista(Nombre);
}

CREATE TABLE Grupo{
id SERIAL PRIMARY KEY,
nombre VARCHAR(20) NOT NULL,
descripcion TEXT NOT NULL
}

CREATE TABLE Pertenece{
id_Grupo INT,
titulo VARCHAR(20) NOT NULL
FOREIGN KEY (titulo) REFERENCE Pieza_Arte(Titulo);
FOREIGN KEY (id_Grupo) REFERENCE Grupo(id);
}
```

### Insertar 
- Por cada tabla creada realizar 4 inserciones.
```sql
INSERT INTO Artista(Nombre, Lugar_Nacimiento, Edad, Estilo_Arte) VALUE 
("luis", )


```


### Consultas
```sql
-- Cantidad de artistas (distintos) que han realizado una pieza de arte entre los anos 2010 y 2020. 
SELECT COUNT(DISTINCT nombre_artista) AS numero 
FROM pieza_arte 
WHERE ano BETWEEN 2010 AND 2020; 

-- Ranking de los grupos con mas obras, de manera descendente. 
SELECT COUNT(titulo) AS cantidadObras 
FROM pertenece 
GROUP BY id_grupo 
ORDER BY cantidadObras DESC; 

-- Nombre y edad de los artistas que hayan realizado una obra dentro de algun grupo que contenga en la descripcion la palabra retrato. 
SELECT DISTINCT nombre_artista, edad 
FROM artista 
JOIN pieza_arte ON artista.nombre = pieza_arte.nombre_artista 
JOIN pertenece ON pieza_arte.titulo = pertenece.titulo 
JOIN grupo ON grupo.id = pertenece.id_grupo 
WHERE grupo.descripcion ILIKE '%retrato%'; 

-- Descripcion del grupo que contenga la Pieza de arte con el mayor precio. 
SELECT descripcion 
FROM grupo 
JOIN pertenece ON pertenece.id_grupo = grupo.id 
JOIN pieza_arte ON pertenece.titulo = pieza_arte.titulo 
WHERE pieza_arte.precio = (SELECT MAX(precio) FROM pieza_arte); 

-- Id de los grupos en donde este la obra Estilo único y El payaso 
SELECT DISTINCT id_grupo 
FROM pertenece 
WHERE titulo = 'Estilo único' OR titulo = 'El payaso'; 

-- Artistas que han realizado al menos 3 piezas de arte. 
SELECT nombre_artista 
FROM pieza_arte 
GROUP BY nombre_artista 
HAVING COUNT(titulo) >= 1; 

-- Nombre y edad de los artistas que tengan una obra con un precio de al menos 100.00 
SELECT DISTINCT artista.nombre, artista.edad 
FROM artista 
JOIN pieza_arte ON artista.nombre = pieza_arte.nombre_artista 
WHERE precio >= 100000; 

-- Título de las obras que pertenecen al grupo INSIDES 
SELECT pertenece.titulo 
FROM pertenece 
JOIN grupo ON pertenece.id_grupo = grupo.id 
WHERE grupo.nombre_grupo = 'INSIDES'; 

-- Artistas que no tienen ninguna obra registrada en la galera. 
SELECT artista.nombre 
FROM artista LEFT J
OIN pieza_arte ON artista.nombre = pieza_arte.nombre_artista 
WHERE pieza_arte.nombre_artista IS NULL; 

-- Nombre y estilo de los artistas nacidos en el año 1963. 
SELECT nombre, estilo 
FROM artista 
WHERE DATE_PART('year', nacimiento) = 1963;
```

### Procedimientos

