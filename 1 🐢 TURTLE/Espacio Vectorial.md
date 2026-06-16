# Espacio Vectorial

Imagina un mapa gigante, pero en lugar de tener solo 2 dimensiones (norte-sur, este-oeste), tiene cientos de dimensiones. Cada punto en ese mapa representa una idea, palabra o documento.

- Las dimensiones son como características implícitas del concepto (¿es animal? ¿es rápido? ¿es un sentimiento positivo?).
- Textos con **significado parecido** terminan ubicados en "barrios" muy cercanos dentro de ese mapa.
- Textos completamente contrarios o no relacionados terminan en puntas opuestas.

Cuando haces una consulta en una base de datos vectorial, el sistema ubica tu pregunta en este mapa y busca a sus "vecinos más cercanos". Para saber quiénes son, simplemente mide la **distancia matemática** entre los puntos. A menor distancia, mayor similitud.

Sin embargo, en este mapa ocurren comportamientos matemáticos curiosos que pueden afectar a los resultados, como se detalla en [[Fenómenos del Espacio Vectorial]].