# Estrategias de Filtrado Vectorial

En sistemas reales, la búsqueda por similitud pura no suele ser suficiente. A menudo necesitamos combinar la potencia de la [[Búsqueda Semántica]] con filtros rígidos de toda la vida (metadatos como fecha, categoría o ID de usuario).

Como [[FAISS]] puro solo entiende de vectores y no de texto ni etiquetas, existen dos estrategias principales para gestionar este "Filtrado Multidominio":

## 1. Filtrado de Metadatos (Metadata Filtering)

Dado que FAISS no guarda información estructurada, debemos mantener una estructura de datos externa (como un DataFrame de Pandas, un diccionario o una base de datos SQL) sincronizada por posición con el índice vectorial.

### Pre-filtrado (Pre-filtering)
Primero filtras tus metadatos y luego buscas en FAISS solo sobre esos IDs.
- **Ventaja:** Resultados 100% precisos según tus reglas de negocio.
- **Desventaja:** Si el filtro es muy estricto y quedan pocos datos, la búsqueda vectorial pierde sentido.

### Post-filtrado (Post-filtering)
Primero haces la búsqueda en FAISS (pides por ejemplo el `Top-100`) y de esos resultados, descartas los que no cumplan tus filtros de metadatos.
- **Ventaja:** Es muy rápido de implementar.
- **Desventaja:** Corres el riesgo de quedarte sin resultados si ninguno de los `Top-K` recuperados cumple las condiciones de metadatos.

## 2. Búsqueda Híbrida
Es la técnica más avanzada. Consiste en realizar dos búsquedas en paralelo:
1. Una búsqueda por **palabras clave** (Keyword search tradicional).
2. Una búsqueda por **similitud semántica** (Vectorial).

Luego se combinan ambos resultados mediante algoritmos como RRF (Reciprocal Rank Fusion) para dar un peso equilibrado a lo que el usuario escribió exactamente y a lo que el sistema entiende por significado.