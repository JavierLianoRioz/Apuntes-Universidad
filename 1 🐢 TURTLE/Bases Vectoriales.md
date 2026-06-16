## Teoría

Las bases de datos vectoriales marcan un cambio de paradigma profundo: pasamos de buscar coincidencias exactas de texto a buscar por **similitud de significado**. 

Están diseñadas para lidiar con el lenguaje natural y datos no estructurados, permitiendo búsquedas mucho más humanas gracias a la [[Búsqueda Semántica]].

### ¿Cómo funciona?
En vez de hablar de **tablas** (como en SQL) o **nodos** (como en Grafos), aquí hablamos de **vectores**.

El sistema funciona gracias a tres pilares fundamentales:
1. **[[Embedding]]**: Es la herramienta que convierte nuestros textos e ideas humanas en listas de números (vectores) que la máquina puede entender.
2. **[[Espacio Vectorial]]**: Es el "mapa" o universo matemático donde se guardan estas listas de números. Los conceptos que significan cosas parecidas acaban muy juntos en este mapa.
3. **Similitud y Distancia**: Cuando haces una búsqueda, el sistema no compara letras. Simplemente mide la distancia física o el ángulo entre los puntos del mapa. Si dos puntos están muy cerca matemáticamente, es que significan casi lo mismo. Para casos específicos, se puede calcular esta [[Similitud Manual]] sin usar bases de datos.

### El Problema de la Escala
Comparar una búsqueda nueva contra millones de vectores de uno en uno es inviable. Para solucionar esto se usan **Índices Vectoriales** como [[FAISS]]. Su función es organizar el mapa en sectores para encontrar a los "vecinos" más cercanos de forma ultra rápida, aproximando la búsqueda en lugar de calcularlo todo.

### ¿Qué casos de uso tienen?
Algunos ejemplos reales son:
- **Sistemas de recomendación**: (Encontrar productos de estilo similar aunque no compartan categorías exactas).
- **Buscadores inteligentes de documentos**: (Encontrar manuales corporativos describiendo el problema, sin saber la palabra exacta).
- **Asistentes Inteligentes y Bots**: Utilizando la arquitectura [[Generación Aumentada por Recuperación]] para que la IA responda basándose en los documentos internos de una empresa.

---

## Práctica

El flujo de trabajo en código (pipeline vectorial) para implementar esto siempre sigue un camino estandarizado.

### El Pipeline Vectorial
`Texto → Embedding (Modelo de IA) → Índice (Base de datos) → Búsqueda`

1. **Generación de Embeddings**: Pasamos nuestros textos por un modelo ligero (ej. `SentenceTransformers` en Python). Esto nos devuelve las matrices de números.
2. **Inicialización del Índice**: Creamos un índice usando una herramienta como [[FAISS]]. Le decimos qué método usar para medir distancias (por ejemplo, distancia Euclidiana - `IndexFlatL2`).
3. **Inserción de Datos**: Añadimos los números generados por el paso 1 a nuestro índice FAISS. *(Ojo: FAISS solo guarda números, la relación "número -> texto original" debes guardarla tú aparte en una lista).*
4. **Consultas**: Cuando un usuario busca algo, primero pasamos su frase por el **mismo modelo de embedding** del paso 1. Luego, le pedimos a FAISS que busque los `K` vectores más cercanos a esa consulta, devolviéndonos qué tan cerca están (su "score" de relevancia).

---

## Convergencia con Grafos

La frontera entre grafos y vectores se difumina con el uso de **Node Embeddings** (vía GDS en Neo4j).
- **Integración Técnica**: La posición y conectividad de un nodo en el grafo se traduce en una coordenada matemática (vector).
- **Valor Agregado**: Permite realizar búsquedas por similitud semántica que tienen en cuenta no solo el contenido del nodo, sino también su **contexto estructural** en la red.

> [!TIP] Arquitectura Recomendada


La frontera entre grafos y vectores se difumina con el uso de **Node Embeddings** (vía GDS en Neo4j).
- **Integración Técnica**: La posición y conectividad de un nodo en el grafo se traduce en una coordenada matemática (vector).
- **Valor Agregado**: Permite realizar búsquedas por similitud semántica que tienen en cuenta no solo el contenido del nodo, sino también su **contexto estructural** en la red.

> [!TIP] Arquitectura Recomendada
> Para un diseño robusto y orientado a objetos de este flujo, consulta la [[Implementación del Pipeline Vectorial]].