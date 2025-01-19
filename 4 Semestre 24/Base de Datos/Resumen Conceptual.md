
---
## Superclave
>Una **superclave** es un conjunto de una o más columnas (atributos) que puede utilizarse para identificar de manera única una fila en una tabla de base de datos. Una superclave puede contener atributos adicionales que no sean necesarios para la identificación única.

## Clave Primaria
>La **clave primaria** es un tipo especial de superclave que se utiliza para identificar de manera única cada registro en una tabla. La clave primaria no permite valores nulos y debe ser única en toda la tabla.

#### Características:
- Identifica unívocamente cada fila de la tabla.
- No puede contener valores nulos.
- Debe ser única.

## Clave Candidata
>Una **clave candidata** es un conjunto mínimo de atributos que puede identificar de manera única un registro en la tabla. Una tabla puede tener múltiples claves candidatas, y una de ellas será seleccionada como la clave primaria.

#### Características:
- Cualquier clave candidata puede ser clave primaria.
- No contiene atributos redundantes.

---
## Modelos E-R (Entidad-Relación)
>Un **modelo Entidad-Relación (E-R)** es una representación gráfica que describe la estructura lógica de una base de datos. Se utiliza para visualizar entidades (objetos) y las relaciones entre ellas.

### Componentes:
- **Entidades**: Representan objetos o cosas del mundo real.
- **Atributos**: Propiedades o características de las entidades.
- **Relaciones**: Definen la forma en que las entidades están vinculadas.

## Relaciones (n:m, 1:n, 1:1)
>Las relaciones en un modelo de base de datos describen la cardinalidad entre dos entidades.

- **n:m**: Una entidad A se puede relacionar con muchas entidades B, y viceversa.
- **1:n**: Una entidad A se puede relacionar con muchas entidades B, pero una entidad B solo se relaciona con una A.
- **1:1**: Una entidad A se relaciona con una sola entidad B y viceversa.

---
## Modelo Relacional
>El **modelo relacional** es un enfoque para la gestión de bases de datos que organiza los datos en tablas (relaciones). Cada tabla tiene filas (tuplas) y columnas (atributos). Las relaciones entre tablas se manejan mediante claves primarias y claves foráneas.

### Componentes:
- **Tuplas**: Filas que representan registros.
- **Atributos**: Columnas que representan las características de los datos.
- **Relaciones**: Vínculos entre diferentes tablas mediante claves.

---
# Conceptos Adicionales

## Normalización
>La **normalización** es el proceso de organizar los datos en una base de datos para reducir la redundancia y mejorar la integridad de los datos. Se descompone una tabla grande en tablas más pequeñas y se definen relaciones entre ellas. Esto minimiza la duplicidad y asegura que las dependencias sean adecuadas.

### Formas normales:
1. **Primera Forma Normal (1FN)**: Eliminar duplicados y garantizar que cada columna contenga solo valores atómicos.
2. **Segunda Forma Normal (2FN)**: Cumplir con 1FN y eliminar dependencias parciales; todos los atributos dependen completamente de la clave primaria.
3. **Tercera Forma Normal (3FN)**: Cumplir con 2FN y eliminar dependencias transitivas, es decir, que los atributos no dependan de otros atributos no clave.

# Formas Normales

## Primera Forma Normal (1FN)
Una tabla está en **Primera Forma Normal (1FN)** si:
- No contiene grupos repetidos o datos multivaluados.
- Todos los atributos contienen solo valores atómicos (no divisibles).

### Ejemplo (Sin 1FN):
| ID  | Nombre     | Teléfonos          |
| --- | ---------- | ------------------ |
| 1   | Juan Pérez | 555-1234, 555-5678 |
| 2   | Ana García | 555-9876           |

En este caso, la columna `Teléfonos` contiene varios valores en una sola celda, lo que viola la 1FN.

### Ejemplo (En 1FN):
| ID  | Nombre     | Teléfono |
| --- | ---------- | -------- |
| 1   | Juan Pérez | 555-1234 |
| 1   | Juan Pérez | 555-5678 |
| 2   | Ana García | 555-9876 |

Aquí, los teléfonos se han separado en filas distintas, cumpliendo con la 1FN.

---

## Segunda Forma Normal (2FN)
Una tabla está en **Segunda Forma Normal (2FN)** si:
- Está en 1FN.
- Todos los atributos no clave dependen completamente de la clave primaria (no hay dependencias parciales).

### Ejemplo (Sin 2FN):
| ID_Cliente | Pedido  | FechaPedido | Ciudad    |
| ---------- | ------- | ----------- | --------- |
| 1          | Pedido1 | 2024-01-01  | Madrid    |
| 1          | Pedido2 | 2024-01-02  | Madrid    |
| 2          | Pedido3 | 2024-01-03  | Barcelona |

En este caso, `Ciudad` depende solo de `ID_Cliente`, no de la clave compuesta `ID_Cliente, Pedido`, lo que viola la 2FN.

### Ejemplo (En 2FN):
**Tabla Clientes**:

| ID_Cliente | Ciudad    |
| ---------- | --------- |
| 1          | Madrid    |
| 2          | Barcelona |

**Tabla Pedidos**:

| ID_Cliente | Pedido  | FechaPedido |
| ---------- | ------- | ----------- |
| 1          | Pedido1 | 2024-01-01  |
| 1          | Pedido2 | 2024-01-02  |
| 2          | Pedido3 | 2024-01-03  |

Al separar la información de la ciudad en otra tabla, se elimina la dependencia parcial.

---

## Tercera Forma Normal (3FN)
Una tabla está en **Tercera Forma Normal (3FN)** si:
- Está en 2FN.
- No hay dependencias transitivas, es decir, los atributos no clave no dependen de otros atributos no clave.

### Ejemplo (Sin 3FN):
| ID_Empleado | Nombre      | ID_Departamento | NombreDepto |
| ----------- | ----------- | --------------- | ----------- |
| 1           | Carlos Ruiz | 10              | Ventas      |
| 2           | Ana López   | 20              | Marketing   |

En este caso, `NombreDepto` depende de `ID_Departamento`, que no es clave, creando una dependencia transitiva.

### Ejemplo (En 3FN):
**Tabla Empleados**:

| ID_Empleado | Nombre      | ID_Departamento |
| ----------- | ----------- | --------------- |
| 1           | Carlos Ruiz | 10              |
| 2           | Ana López   | 20              |

**Tabla Departamentos**:

| ID_Departamento | NombreDepto |
| --------------- | ----------- |
| 10              | Ventas      |
| 20              | Marketing   |

Separando la información del departamento en una tabla aparte, se elimina la dependencia transitiva.


---
# Álgebra Relacional

>El **álgebra relacional** es un conjunto de operaciones que se utilizan para consultar y manipular datos en una base de datos relacional. Estas operaciones toman una o más relaciones (tablas) como entrada y producen una nueva relación como resultado.

## Operadores principales

### 1. Proyección (`π`)
>La **proyección** selecciona columnas específicas de una tabla, descartando las demás. Devuelve una relación con solo los atributos seleccionados.

- **Sintaxis**: `π_atributos(relación)`
- **Ejemplo**: Si tienes una tabla `Clientes` con los atributos `ID`, `Nombre`, `Ciudad`, la proyección `π_Nombre,Ciudad(Clientes)` devolvería una tabla con solo los atributos `Nombre` y `Ciudad`.

### 2. Selección (`σ`)
>La **selección** se utiliza para filtrar filas de una tabla que cumplen con una condición específica. Devuelve una relación con solo las filas que satisfacen la condición.

- **Sintaxis**: `σ_condición(relación)`
- **Ejemplo**: `σ_Ciudad='Madrid'(Clientes)` devolvería todos los registros de clientes que vivan en Madrid.

### 3. Unión (`∪`)
>La **unión** combina dos relaciones y devuelve una nueva relación que contiene todas las tuplas (filas) que están en cualquiera de las dos relaciones.

- **Sintaxis**: `Relación1 ∪ Relación2`
- **Ejemplo**: Si tienes dos tablas de clientes de diferentes ciudades, la unión de ambas devuelve todos los clientes sin duplicados.

### 4. Intersección (`∩`)
>La **intersección** devuelve solo las tuplas que están presentes en ambas relaciones.

- **Sintaxis**: `Relación1 ∩ Relación2`
- **Ejemplo**: Devuelve los clientes que aparecen en ambas listas de clientes.

### 5. Diferencia (`−`)
>La **diferencia** devuelve las tuplas que están en la primera relación, pero no en la segunda.

- **Sintaxis**: `Relación1 − Relación2`
- **Ejemplo**: Si tienes una lista de clientes y quieres ver quiénes están solo en una de las listas y no en la otra.

### 6. Producto Cartesiano (`×`)
>El **producto cartesiano** combina todas las filas de la primera relación con todas las filas de la segunda, formando pares de tuplas.

- **Sintaxis**: `Relación1 × Relación2`
- **Ejemplo**: Si tienes una tabla de clientes y otra de pedidos, el producto cartesiano generaría todas las combinaciones posibles de cliente y pedido.

### 7. Join (Unión por coincidencia)
>El **join** combina filas de dos tablas basándose en una condición de coincidencia entre los atributos.

- **Sintaxis**: `Relación1 ⋈ condición Relación2`
- **Ejemplo**: `Clientes ⋈ Clientes.ID = Pedidos.ClienteID Pedidos` uniría las tablas `Clientes` y `Pedidos` en base al `ID` del cliente.

### 8. División (`/`)

> La **división** se utiliza para encontrar todos los elementos de una relación que están relacionados con **todos** los elementos de otra relación.

- **Sintaxis**: `RelaciónA ÷ RelaciónB`
- **Ejemplo**: `Empleado_Proyecto ÷ Proyectos_Requeridos` devolvería los empleados que han trabajado en **todos** los proyectos requeridos.

## Otros aspectos del álgebra relacional

### Clausura
>El **álgebra relacional** tiene la propiedad de **clausura**, lo que significa que las operaciones producen relaciones como resultado, que a su vez pueden ser utilizadas como entrada para otras operaciones.

### Relaciones
>Las operaciones del álgebra relacional se aplican sobre **relaciones** (tablas) que siguen las propiedades del **modelo relacional**, como la consistencia y la integridad referencial.

### Operaciones extendidas
>Además de las operaciones básicas, hay operaciones extendidas como **agregación** (SUM, COUNT, AVG), que permiten realizar cálculos sobre los datos en una relación.


![[Pasted image 20240926010357.png]]
