---
materia: Bases de Datos 2
categoria: universidad
---
# NoSQL: Sistemas de Persistencia No Relacionales

NoSQL engloba un conjunto de tecnologías de bases de datos diseñadas para superar las limitaciones de escalabilidad, flexibilidad y rendimiento del modelo relacional tradicional (SQL) ante grandes volúmenes de datos o esquemas dinámicos.

---

## ¿Por qué surge el paradigma NoSQL?

Las bases de datos relacionales tradicionales se diseñaron en una época donde el almacenamiento era costoso y el tráfico era predecible. Al escalar en la era moderna, aparecen limitaciones críticas:

- **Límites de Escalabilidad Vertical:** Aumentar CPU/RAM de un único servidor es extremadamente costoso y tiene un límite físico insuperable. SQL no escala horizontalmente de forma nativa con facilidad debido a la necesidad de mantener consistencia en transacciones distribuidas.
- **Esquemas Rígidos:** Cualquier cambio de esquema requiere migraciones costosas que bloquean las tablas en producción.
- **Coste de Relaciones Complejas (Joins):** A medida que la profundidad de las conexiones crece, las operaciones de `JOIN` en SQL degradan el rendimiento de forma exponencial.

---

## ¿Qué diferencia a ACID de BASE?

Las bases de datos SQL priorizan la consistencia absoluta, mientras que la mayoría de los motores NoSQL eligen la disponibilidad y escalabilidad, lo que se formaliza en estos dos paradigmas:

### El paradigma ACID (SQL)
- **A**tomicidad: La transacción se realiza por completo o no se realiza en absoluto.
- **C**onsistencia: Los datos siempre cumplen con las reglas de integridad del esquema.
- **I**solation (Aislamiento): Las transacciones concurrentes no interfieren entre sí.
- **D**urabilidad: Una vez confirmada la transacción, los cambios persisten incluso ante fallos de energía.

### El paradigma BASE (NoSQL)
- **B**asically **A**vailable (Básicamente Disponible): El sistema garantiza disponibilidad; responderá siempre, aunque sea con un error o datos desactualizados.
- **S**oft State (Estado Blando): El estado de los datos puede cambiar con el tiempo sin intervención del usuario debido a la replicación.
- **E**ventual Consistency (Consistencia Eventual): El sistema convergirá hacia un estado consistente en todos sus nodos en algún momento futuro (la consistencia no es inmediata).

---

## ¿Cuáles son los cinco grandes modelos de datos NoSQL?

Se descompone de la siguiente manera según cómo estructuran la información físicamente:

### 1. Clave-Valor (Key-Value)
El modelo más simple. Los datos se guardan como pares donde una clave única recupera un valor opaco (el motor no inspecciona su interior).
- **Caso de uso típico:** Almacenamiento y recuperación de sesiones de usuario o caché rápida con latencias menores a 5 ms (ej. Redis).

### 2. Documental (Document-oriented)
Almacena la información en documentos estructurados (JSON/BSON). Cada documento puede tener un esquema completamente diferente.
- **Caso de uso típico:** Catálogos de e-commerce donde cada producto tiene propiedades heterogéneas, o sistemas con evolución rápida del modelo (ej. MongoDB).

### 3. Columnares (Wide-Column)
Los datos se organizan en familias de columnas en lugar de filas rígidas. Permite lecturas rápidas de columnas específicas sobre miles de millones de filas.
- **Caso de uso típico:** Registro analítico masivo de sensores (IoT) o series temporales (ej. Cassandra).

### 4. Grafos (Graph)
Representa la información mediante Nodos (entidades), Relaciones (conexiones directas en disco) y Propiedades. Elimina el coste de los `JOIN` relacionales.
- **Caso de uso típico:** Motores de recomendación, redes sociales o detección de fraudes y lavado de dinero (ej. Neo4j).

### 5. Vectoriales (Vector Databases)
Almacenan y realizan búsquedas sobre vectores matemáticos multidimensionales (embeddings) calculados mediante modelos de Machine Learning.
- **Caso de uso típico:** Búsquedas por similitud semántica, reconocimiento de imágenes o memoria para Inteligencia Artificial y agentes RAG (ej. FAISS, Pinecone).

---

## ¿Cómo elegir el motor adecuado?

La regla de oro del diseño en persistencia es: **el problema y el patrón de acceso determinan la base de datos, no la preferencia del desarrollador**.

| Requerimiento | Elección Recomendada | Justificación |
| :--- | :--- | :--- |
| Alta consistencia (Ej: banca, matrículas) | **SQL Relacional** | Requiere transacciones estrictas bajo ACID. |
| Catálogo dinámico y lectura rápida de objetos | **NoSQL Documental** | Estructuras jerárquicas flexibles que mapean objetos de código. |
| Latencia mínima en lecturas sencillas | **NoSQL Clave-Valor** | Acceso directo por clave con estructuras en memoria. |
| Relaciones densas o análisis de caminos | **NoSQL Grafos** | Recorrido físico eficiente sin coste de joins SQL. |
| Analítica masiva de datos en tiempo real | **NoSQL Columnar** | Agregaciones analíticas rápidas sobre flujos masivos de escritura. |
| Similitud de conceptos en lenguaje natural | **NoSQL Vectorial** | Búsqueda semántica usando distancias matemáticas en embeddings. |

**¡OJO!** Un error típico de diseño es forzar un motor NoSQL por "moda" en un sistema que por naturaleza requiere consistencia transaccional fuerte (como una pasarela de pagos), lo que provocará inconsistencias de datos graves y difíciles de depurar a largo plazo.
