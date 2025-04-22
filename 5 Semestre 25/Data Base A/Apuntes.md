
---
# PPT1

El sistema para administrar una *base de datos* es conocida como **DBMS** donde las principales del mercado son *Microsoft SQL Server, Oracle, MySQL, Progress*.

- Modelo Entidad Relación
Es una técnica de diseño gráfico de una base de datos donde se muestra información relativa a los datos y sus relaciones.

Las bases de datos relacionadas deben cumplir con ciertas propiedades que garantizan su correcto funcionamiento, eficiencia y seguridad

1. Integridad de los datos.
2. Independencia de Datos
3. Consistencia de los Datos
4. Concurrencia y Control de Transacciones
5. Atomicidad y ACID
6. Seguridad y Control de Acceso

Las cuatro funciones básica s de persistencia son las **CRUD** en las cuales se encuentran:
- **C**reate 
- **R**ead
- **U**pdate
- **D**elete

Tales como lo mencionado existe *Insert* para insertar los registros en una tabla, *Select* para seleccionar registros de una o más tablas, que permite acciones como filtraciones (where), cruces (join) y agregación (group), por otro lado *Update* para actualizar campos de una tabla y por ultimo *Delete* para eliminar registros de una tabla.

### Vocabulario
> SQL : Structured Query Language
> DBMS : Data base management system

---
# PPT2

Modelo Relacional (RDBMS)

Es la base de la mayoría de los DBMS que se utilizan actualmente y su estructura es:
1. Tablas (Entidades)
2. Filas (Tuplas)
3. Columnas (Atributos)
4. Concurrencia y Control de Transacciones
5. Relaciones entre tablas
6. Cardinalidad
7. Llaves (Claves-Keys)

### Sistemas de Gestión de Bases de datos
- **Concurrencia**: Varios usuarios pueden acceder y actualizar datos al mismo tiempo, preservando la consistencia de los datos.
- **Mínima Redundancia**: los datos solo están repetidos por justificadas razones.
- **Reducción de Inconsistencias**: En teoría, no deben producirse problemas.
- **Soporte de Transacciones**: Se puede definir "Transacciones" que aseguren la ejecución completa de un conjunto de operaciones sobre los mismos datos por varios usuarios.
- **Preservar la Integridad**: Se puede emplear mecanismos para asegurar que los datos están "Correctos".
- **Mejor manejo de la seguridad**: Se puede establecer un mejor control de la seguridad.
- **Estándares**: Se puede forzar estándares para su aplicación en todos los sistemas.

Los 8 servicios que debe proporcionar una DBMS:

1. Almacenamiento de datos, recuperación y actualización
2. Un catalogo accesible al usuario con la descripción de los datos
3. Soporte a transacciones
4. Control de accesos concurrentes
5. Servicios de recuperación
6. Seguridad de accesos (autorizaciones)
7. Soporte a comunicaciones de datos
8. Integridad de datos

Las RDBMS garantizan  y deben cumplir con las propiedades ya mencionadas donde;

- Tipos de Integridad
	1. *Integridad de Entidad*: Cada fila en una tabla debe tener un identificador único.
	2. *Integridad referencial*: Mantiene la coherencia entre tablas mediante claves foráneas.
	3. *Integridad de dominio*: Restringe los valores permitidos para cada columna según su tipo de datos.
- Independencia de Datos
	1. *Independencia Lógica*: Se puede modificar las relaciones y estructuras de datos sin cambiar las aplicaciones que acceden a ellas.
	2. *Independencia Física*: Los cambios en la forma de almacenamiento no afectan a la estructura lógica de los datos.
- Consistencia de los Datos
	1. Asegura que la base de datos pasa de un estado válido a otro después de cada transacción.
- Concurrencia y Control de Transacciones
	1. Permite que múltiples usuarios accedan a la base de datos simultáneamente sin interferencias ni pérdida de datos y sus mecanismos son: 
		1. *Bloqueo de registros (Locking)*: Evita que múltiples usuarios modifiquen la misma fila simultáneamente.
		2. *Versionado de registros*: Permite acceso sin bloqueos mediante versiones de datos.
- Atomicidad ACID:
	1. *Atomicidad*: Una transacción se ejecuta completamente o no se ejecuta en absoluto.
	2. *Consistencia*: La base de datos siempre permanece en un estado válido.
	3. *Aislamiento*: Las transacciones se ejecutan de forma independiente unas de otras.
	4. *Durabilidad*: Una vez confirmada, una transacción se mantiene incluso en caso de fallo del sistema.
- Seguridad y Control de Acceso
	1. *Autenticación*: Verificación de identidad de los usuarios.
	2. *Autorización*: Controla qué acciones pueden realizar los usuarios en la base de datos.

La *Redundancia* es cuando los datos se repiten continua e innecesariamente por las tablas, por ello existe la normalización que consiste en la *transformación de las vistas de un usuario complejas*, donde la idea es pasar por un proceso que consiste en designar y aplicar una serie de reglas a las relaciones obtenidas tras el paso del modelo entidad-relación al modelo relacional.

**Primera forma normal**
- Todos los atributos llave están definidos.
- No hay grupos repetidos en la tabla. Cada fila contiene un solo valor, no un conjunto de ellos.
- Todos los atributos son dependientes de la llave primaria.
- Todos los atributos son atómicos. Un atributo es atómico si los elementos del dominio son simples e indivisibles.
- Los campos no clave deben identificarse por la clave.
- No debe existir variación en el número de columnas.
- Debe existir una independencia del orden tanto de las filas como de las columnas.
**Segunda forma normal**
- Una tabla 1NF está en 2NF si y solo si, dada una clave primaria  y cualquier atributo no sea un constituyente de la clave primaria, el atributo no clave depende de toda la clave primaria en vez de solo de una parte de ella.
- En términos levemente más formales, una tabla 1NF está en 2NF si y solo si ninguno de sus atributos (no principales) son funcionalmente dependientes de una parte (subconjunto propio) de una clave candidata (un atributo no principal es uno que no pertenece a ninguna clave candidata).
### Vocabulario
> RDBMS : Relation data base management system
> DBMS : Data base management system

---
# AYUDANTIA PRESOLEMNE

### Transactions
Todas las transacciones son ACID (En este curso).

Begin transaction : Comenzar una transaccion.
Rolback : Sirve para testear y volver a la situación antigua.
Commit : Se realizan los cambios.

- **Estructura** : 
``` sql
BEGIN TRANSACTION;

Update - Set - Where --SQL

ROLLBACK; --Nada de esto paso
COMMIT; --Transacción realizada
```

### Dead Locks

Se basa en Transacciones 

- Si esta en espera solo debe terminar la transacción hasta que se actualice o libere.
- El ultimo en actuar muere cuando están cruzados las transacciones.


### CRUD

- **Select**
1.Recibe un conjunto de condiciones, que pueden ser de selección o de  
asociación.  
• 1.1. El sistema parte por las de selección, con el fin de optimizar la  
consulta. Una condición de selección va a disminuir la cantidad de  
datos o de filas que hay que relacionar. Dentro del explain esto  
estará dentro de la línea más profunda o más identada del plan de  
ejecución.  
2.Busca filas que cumplan la selección.  
3. Asocia esas filas con las otras tablas.  
4. Esto implica una cantidad "N" de accesos (bloques, tanto bloque  
secuencial, como bloque (nodo) del árbol en caso de que hubiera índice)  
al dispositivo de almacenamiento secundario.  
5. Obtiene el resultado solicitado.

- **Insert**
3. Trae a memoria el ultimo bloque de la tabla => 1 acceso  
4. Si el bloque tiene espacio, se agrega la fila a ese bloque  
5. Si no hay espacio => genera un nuevo bloque y agrega la fila.  
6. Graba el bloque en el disp. De almacenamiento al final de la tabla => + 1  
ac  
7. Si hay índice:  
8. Se busca el nodo en donde se debe agregar el valor del atributo =>  
Logm N  
9. Una vez ubicado el nodo se trae a memoria (nodo = bloque del árbol). Si  
hay espacio en ese nodo => se agrega el nuevo valor.  
10. Si no hay espacio se debe hacer un proceso adicional. (Block Split)

- **Block Split**
• Si no hay espacio en el nodo, se produce un fenómeno  
llamado Block Split, en donde el nodo se divide en 2, cada  
parte con la mitad de los valores, por lo tanto se inserta el  
valor más la dirección a memoria.  
• Además, se crea o se promueve al nodo superior el valor + la  
dirección del elemento que quedo justo en el medio, donde  
se hizo el corte => 2 accesos +  
• Recursivamente se puede producir los 2 casos anteriores, en  
el peor de los casos se tendrá: 2 * Logm N accesos + . En  
promedio es solo Logm N accesos +.  
• Por esto la inserción en personas2 se tardaba mas que  
en personas1

- **Delete**
1. Buscar filas que cumplan con la condición de selección => N Accesos  
(bloques que traer a memoria)  
2. Marcar en el bloque la eliminación de la fila, luego grabar esto en el disp. de  
almacenamiento => +1 acceso por bloque  
3. Que pasa si hay índice?  
4. Se busca el nodo en donde se debe eliminar el valor y la dirección del  
atributo.  
5. Eliminar este valor y grabar el nodo nuevamente en el disp. de  
almacenamiento. => + 1 acceso  
* Recordar: nodo tiene largo fijo. No hay problema de block Split,  
eliminación física y lógica.

- **Update**
1. Buscar filas que cumplan con la condición de selección. => n accesos  
2. Marcar en el bloque la fila como eliminada, actualizar y regrabar la fila en el disp. de  
almacenamiento. => 1 acceso  
3. Trae el ultimo bloque de la tabla en cuestión => +1 acceso  
4. Si hay espacio se agrega la fila a ese bloque.  
5. Si no hay espacio se genera un nuevo bloque para insertar la fila actualizada. =>  
+1 acceso.  
6. Que pasa si hay índice?  
7. Se busca el nodo en cuestión => Logm N acceso  
8. En el nodo se actualiza la dirección. El espacio será el mismo, así que no hay  
problema, luego se graba en el disp. de almacenamiento. +1 acceso.


### Plan de ejecución del motor de la db

1. Consulta SQL
	- Es la instrucción SQL ingresada por el usuario.
2. Parser
	- Convierte la consulta en una estructura de árbol (árbol de sintaxis). 
	- Revisa la sintaxis y comprueba que las tablas sean validas
3. Reescritor
	- Se plica reglas de reescritura a la consulta
	- Se usa, por ejemplo, en vistas y reglas definidas para transformar la consulta antes de su ejecución
4. Optimizador
	- Evalúa diferentes formas de ejecutar la consulta
	- Elige el plan con el menor costo estimado basándose en estadísticas de la base de datos
	- Considera el uso de índices, joins, secuencias de acceso a datos, etc
5. Planificador
	- Convierte el plan de ejecución seleccionado en instrucciones detalladas que el motor de PostgreSQL puede ejecuta
6. Ejecutor
	- Ejecuta la consulta
7. Resultado
	- Imprime la consulta

#### Fin

