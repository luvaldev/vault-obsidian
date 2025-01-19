# Resumen de Tecnologías

## **XML (eXtensible Markup Language)**

### Uso Recomendado
- **Almacenamiento y transmisión de datos estructurados** con una jerarquía clara.
- Ideal para **intercambio de datos** entre sistemas heterogéneos.
- Usado para archivos de configuración, documentos legales o datos estructurados.

### Ventajas
- Amplio soporte en diferentes plataformas y lenguajes.
- Validación mediante DTD o XML Schema.

### Ejemplo de Sintaxis
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ejemplo atributo="valor">
    <elemento>Contenido</elemento>
    <!-- Comentario -->
</ejemplo>
```

### Casos de Uso
- Documentación técnica.
- Configuración de software.
- Interoperabilidad entre aplicaciones (SOAP).

---

## **RDF (Resource Description Framework)**

### Uso Recomendado
- Para **modelar datos semánticos** con relaciones entre recursos.
- Ideal para aplicaciones de **web semántica** y representación de conocimiento.
- Representación de información como tripletas.

### Ventajas
- Estandarización en la representación de relaciones.
- Interoperabilidad para sistemas basados en datos distribuidos.

### Ejemplo de Tripletas
- **Sujeto**: `http://example.org/Camila`
- **Predicado**: `http://example.org/esAmigaDe`
- **Objeto**: `http://example.org/Ana`

### Casos de Uso
- Representación de ontologías (por ejemplo, en bioinformática).
- Sistemas de recomendación basados en relaciones.

---

## **SPARK SQL**

### Uso Recomendado
- Realizar consultas sobre bases de datos RDF.
- Ideal para proyectos con relaciones complejas en datos semánticos.

### Ventajas
- Potente para consultar relaciones y patrones en tripletas.
- Flexibilidad en consultas sobre grandes grafos RDF.

### Ejemplo de Consulta
```sparql
SELECT ?amiga ?edad
WHERE {
    ?amiga ex:esAmigaDe <http://example.org/Camila> .
    ?amiga ex:tieneEdad ?edad .
}
```

### Casos de Uso
- Extracción de datos de grafos como Wikidata.
- Consultas avanzadas en sistemas de web semántica.

---

## **MongoDB (NoSQL, orientada a documentos)**

### Uso Recomendado
- Manejo de datos **sin esquema fijo** o con cambios frecuentes.
- Ideal para aplicaciones web y móviles que usan datos JSON.
- Proyectos que requieren **escalabilidad horizontal**.

### Ventajas
- Flexibilidad para almacenar datos con diferentes estructuras.
- Consultas rápidas y gran desempeño.

### Ejemplo de Documento
```json
{
    "nombre": "Producto A",
    "precio": 1000,
    "categorias": ["tecnología", "hogar"]
}
```

### Ejemplo de Consulta
```javascript
db.productos.find({ precio: { $gt: 500 } })
```

### Casos de Uso
- Ecommerce: almacenamiento de productos, usuarios y pedidos.
- Aplicaciones IoT (Internet of Things).
- Sistemas de contenido dinámico.

---

## **Neo4j (NoSQL, orientada a grafos)**

### Uso Recomendado
- Modelado y consulta de **relaciones complejas** entre entidades.
- Ideal para proyectos basados en redes, grafos o interconexiones.

### Ventajas
- Optimizado para explorar relaciones y patrones en grafos.
- Consultas eficientes para datos altamente conectados.

### Ejemplo de Nodo
```cypher
(:Usuario {nombre: "Carlos", edad: 28})
```

### Ejemplo de Consulta en Cypher
```cypher
MATCH (u:Usuario)-[:AMIGO_DE]->(a:Usuario)
WHERE u.nombre = "Carlos"
RETURN a.nombre
```

### Casos de Uso
- Redes sociales (amigos, seguidores).
- Sistemas de recomendaciones (usuarios-productos).
- Análisis de rutas o conexiones (logística, redes de transporte).

---

## **Comparación General**

| **Tecnología** | **Ventaja Principal**                    | **Mejor Uso**                         |
|----------------|------------------------------------------|----------------------------------------|
| **XML**        | Interoperabilidad y validación estructural | Intercambio de datos entre sistemas.  |
| **RDF**        | Modelado semántico y datos enlazados      | Representación de conocimiento.       |
| **SPARQL**     | Consultas sobre grafos RDF               | Análisis de relaciones semánticas.    |
| **MongoDB**    | Flexibilidad y escalabilidad             | Datos JSON dinámicos o sin esquema.   |
| **Neo4j**      | Relaciones complejas y datos conectados  | Redes sociales, grafos, recomendaciones. |
