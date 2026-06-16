# Embedding

Un embedding es básicamente un "traductor". Es el proceso (o la función) que toma algo del mundo real, como una palabra, una frase o incluso una imagen, y lo convierte en una lista de números (un vector).

Esa lista de números representa las **coordenadas** que ubican a ese concepto dentro del [[Espacio Vectorial]].

Para crear embeddings, no lo hacemos a mano. Usamos modelos de Inteligencia Artificial que ya han sido entrenados leyendo millones de textos (como `SentenceTransformers` en Python) para que sepan cómo "traducir" correctamente el significado humano a números.