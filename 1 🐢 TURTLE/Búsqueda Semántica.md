# Búsqueda Semántica

Es un tipo de búsqueda que intenta comprender la **intención** del usuario y el **significado** de las palabras, en lugar de buscar coincidencias exactas de texto (como hace el típico `Control+F` o un `WHERE` en SQL).

Por ejemplo, si buscas "perro feliz" en un sistema tradicional, solo te devolverá textos que contengan exactamente esas palabras.
En un sistema con búsqueda semántica, te puede devolver un documento que hable de "un caniche alegre", porque el sistema "entiende" que los conceptos están relacionados.

Para lograr esto, la búsqueda semántica convierte las palabras en números (ver [[Embedding]]) y las ubica en un "mapa" (ver [[Espacio Vectorial]]) para comparar qué tan cerca están los conceptos entre sí.

---

## Robustez y Calibración del Pipeline

#### 1. Umbrales Dinámicos Adaptativos
Para evitar el ruido de respuestas irrelevantes, se implementan thresholds basados en el **score promedio** de los resultados devueltos por la query, permitiendo que el sistema se adapte a la densidad del espacio vectorial en tiempo de ejecución.

#### 2. Robustez ante "Ruido" (Contaminación Semántica)
El aumento de dominios no relacionados en una base vectorial (ej. mezclar medicina con economía) degrada la precisión del ranking.
- **Solución**: Implementar **Búsqueda Multidominio Agrupada**, filtrando por metadatos de categoría simultáneamente al cálculo de similitud para mantener la pureza contextual.

#### 3. Feedback Semántico por Historial
Uso del historial de interacciones del usuario como "queries de entrada" adicionales. Esto permite que el sistema actúe como un recomendador de feedback semántico, ajustando los resultados según la trayectoria previa del usuario.

#### 4. Resiliencia Ortográfica
Los modelos de embedding modernos (basados en sub-tokens) son intrínsecamente robustos a errores tipográficos. A diferencia de la búsqueda por palabras clave, el pipeline vectorial mantiene la recuperación semántica incluso ante fallos ortográficos leves, capturando la intención subyacente.