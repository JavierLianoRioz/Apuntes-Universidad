# RAG (Generación Aumentada por Recuperación)

El **RAG** (Retrieval-Augmented Generation) es una técnica donde combinamos una base de datos de información con un modelo de Inteligencia Artificial (como ChatGPT).

Sirve para darle al modelo de lenguaje una especie de "memoria a largo plazo" basada en tus propios documentos, evitando que invente respuestas (alucinaciones).

### Cómo funciona paso a paso:
1. El usuario hace una pregunta.
2. Usamos [[Búsqueda Semántica]] para encontrar los párrafos más relevantes dentro de nuestros documentos.
3. Le pasamos la pregunta original junto con esos párrafos recuperados a la IA y le decimos: *"Responde a la pregunta usando ÚNICAMENTE esta información que te acabo de dar"*.

De esta forma, la IA tiene el contexto exacto que necesita para dar una respuesta precisa y confiable.