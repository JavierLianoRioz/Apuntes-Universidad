---
materia: Bases de Datos 2
categoria: universidad
---

# Bases de Datos 2

Esta asignatura explora el ecosistema de las bases de datos **NoSQL**, centrándose en paradigmas que permiten gestionar grandes volúmenes de datos y relaciones complejas que escapan al modelo relacional tradicional.

---

## ¿Cuál es el núcleo de la materia?

El curso se fundamenta en el estudio de las bases [[NoSQL]], analizando cómo diferentes estructuras de almacenamiento optimizan el rendimiento y la flexibilidad según las necesidades del sistema.

---

## Criterios de Selección (Patrones de Examen)
Ante la pregunta de qué base de datos es la más adecuada:

- **Bases de Datos de Grafos (Neo4j)**: Para analizar **relaciones complejas** entre entidades (ej: investigadores, publicaciones y citas académicas).
- **Bases de Datos Documentales (MongoDB)**: Para sistemas con **atributos heterogéneos** (productos con diferentes propiedades según el proveedor) o donde la velocidad de lectura de la entidad completa sea crítica.
- **Bases de Datos Vectoriales**: Para búsquedas basadas en **similitud semántica** o **embeddings**.
- **Bases de Datos de Series Temporales / Columnares**: Para analítica de **grandes volúmenes de sensores** (IoT) a gran escala.

---

## ¿Qué tramos cubrimos en el segundo parcial?

El foco del segundo bloque se desplaza hacia tecnologías más especializadas —fundamentales para la ingeniería de datos moderna— que se descomponen de la siguiente manera:

- **[[Bases de Grafos]]**: Para el modelado de conexiones intensas y navegación de relaciones.
- **[[Bases Vectoriales]]**: Esenciales para la búsqueda por similitud y el manejo de **Embeddings**.

**¡OJO!** Es fundamental repasar el [[Taller Bases de datos 22 Abril 2026 Neo4j|Primer Taller del segundo parcial]] para consolidar la implementación práctica de estos modelos.

---

## ¿Cómo afrontamos el examen final?

La evaluación para el final (late-game) se aleja de la teoría pura para centrarse en la resolución de problemas prácticos. Esto significa que debemos dominar la sintaxis y el modelado aplicados a casos de uso —preguntas de tipo resuelve— utilizando dos motores específicos:

- **[[MongoDB]]**: Como máximo exponente práctico del paradigma orientado a documentos.
- **[[Cypher|Neo4j]]**: Como herramienta central para lanzar consultas sobre las relaciones en grafos.

**Error típico:** Estudiar únicamente los conceptos teóricos y obviar la práctica con las queries. La soltura en la sintaxis de estos sistemas será determinante.

---


---

## Evolución de la Consistencia y Transacciones

El paradigma NoSQL ha convergido hacia capacidades transaccionales que antes eran exclusivas del modelo relacional:

- **Transacciones ACID en Documental**: MongoDB (v4.0+) permite transacciones multi-documento, rompiendo el mito de la inconsistencia eventual. Esto permite usar modelos documentales en casos de uso críticos (Banca, Seguros).
- **Causal Consistency**: La capacidad de garantizar el orden causal en sistemas distribuidos permite que las bases de datos NoSQL cumplan con las garantías de "Read-your-own-writes" incluso en clústeres globales.
