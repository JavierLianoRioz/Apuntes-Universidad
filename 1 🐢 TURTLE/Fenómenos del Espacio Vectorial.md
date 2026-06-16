# Fenómenos del Espacio Vectorial

Al trabajar con [[Embedding|embeddings]] y [[Espacio Vectorial|espacios vectoriales]], existen comportamientos matemáticos que afectan directamente a la calidad de la recuperación y que pueden generar resultados inesperados si no se comprenden bien.

## 1. Ambigüedad y Falta de Contexto
Un vector representa un punto fijo en el espacio. Si buscamos una palabra aislada con múltiples significados (polisemia), el sistema fallará al no tener contexto para decidir en qué zona del mapa ubicarse.

*   **Ejemplo:** La palabra "Banco". Sin contexto, el embedding resultante estará en una posición "promedio" entre el sector financiero y el sector de mobiliario urbano, lo que probablemente no devolverá resultados precisos para ninguno de los dos.
*   **Solución:** Los embeddings deben generarse siempre sobre frases o párrafos completos para que el modelo pueda desambiguar el significado.

## 2. Contaminación Semántica
Ocurre cuando se mezclan en el mismo índice vectorial documentos de dominios radicalmente opuestos o sin relación.

*   **Efecto:** Al medir distancias, conceptos que son similares en un dominio (ej. "Virus" en medicina) pueden verse "atraídos" o confundidos por conceptos de otro dominio (ej. "Virus" en ciberseguridad), distorsionando el vecindario del [[Espacio Vectorial]].

## 3. Saturación Semántica
Se produce cuando inyectamos demasiados vectores que son casi idénticos en la misma zona del mapa.

*   **Impacto:** Los scores de similitud se vuelven extremadamente cercanos entre sí (ej. todos los resultados devuelven 0.999). Esto dificulta enormemente el ranking y el filtrado, ya que el sistema no tiene "espacio matemático" suficiente para distinguir cuál es realmente mejor.

## 4. Proximidad Geométrica vs Diferencia Semántica
Este es el fenómeno más contraintuitivo: **Frases con significados opuestos suelen caer muy cerca geométricamente.**

*   **El porqué:** Los modelos de embedding actuales se fijan mucho en la estructura y el contexto. 
    *   Frase A: "El gato está vivo".
    *   Frase B: "El gato está muerto".
*   Ambas comparten el 80% de las palabras y el contexto estructural ("El gato está..."). Para el modelo, el contexto es tan similar que los ubica casi en el mismo punto, a pesar de que para un humano la diferencia semántica es total.
*   **Conclusión:** La búsqueda vectorial es excelente para encontrar el "tema" del que se habla, pero puede ser ciega ante negaciones o cambios críticos de una sola palabra.

## 5. Inestabilidad del Espacio Vectorial
El comportamiento del sistema no es rígido; depende por completo del diseño y los pesos del [[Embedding]]. Un sistema vectorial es altamente sensible:
*   **Efecto:** Pequeñas modificaciones en los pesos de un concepto o la adición de una nueva dimensión pueden reorganizar masivamente las distancias. Aumentar exageradamente la magnitud de una palabra hará que domine el espacio, atrayendo resultados que semánticamente no deberían estar tan cerca.

## 6. Colapso del Espacio Vectorial
Ocurre cuando el modelo de representación fuerza a que dos conceptos diferentes asuman posiciones idénticas o casi idénticas en el mapa (por un mal diseño del embedding o falta de dimensiones diferenciadoras).
*   **Efecto:** La pérdida de diferenciación destruye la utilidad del sistema. Si "perro" y "gato" colapsan en el mismo punto exacto, el sistema será incapaz de distinguirlos en cualquier consulta compuesta, afectando a todas las combinaciones que los usen.

## 7. Ruido en el Espacio
Se produce al intentar representar palabras o conceptos desconocidos (fuera del vocabulario del modelo) asignándoles valores por defecto o ruido.
*   **Efecto:** El ruido evita que el sistema devuelva errores al encontrar palabras nuevas, pero introduce ambigüedad. Un efecto acumulativo de palabras ruidosas en una frase terminará generando similitudes poco informativas y acercando la consulta a regiones irrelevantes del [[Espacio Vectorial]].