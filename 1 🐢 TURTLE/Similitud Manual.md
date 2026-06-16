# Similitud Manual (Sin Índices)

En sistemas pequeños o para entender la base matemática de [[FAISS]], podemos calcular qué tan parecidos son dos textos comparando sus [[Embedding|embeddings]] directamente, sin necesidad de usar un índice complejo.

## Similitud del Coseno

Es la métrica estándar. No mide la distancia física (en línea recta), sino el **ángulo** entre dos vectores. 
- Si el ángulo es 0°, los vectores apuntan a la misma dirección (Similitud = 1).
- Si el ángulo es 90°, no tienen nada que ver (Similitud = 0).

### Implementación en Python (NumPy)
Si tenemos dos vectores `A` y `B` (obtenidos de un modelo de embedding):

```python
import numpy as np

def similitud_coseno(vec_a, vec_b):
    # Producto escalar (Dot product)
    dot_product = np.dot(vec_a, vec_b)
    
    # Normas (Magnitudes) de los vectores
    norm_a = np.linalg.norm(vec_a)
    norm_b = np.linalg.norm(vec_b)
    
    # Fórmula del coseno
    return dot_product / (norm_a * norm_b)

# Ejemplo
score = similitud_coseno(embedding_1, embedding_2)
print(f"La similitud es de: {score:.4f}")
```

## Por qué es útil saber esto
1. **Validación:** Sirve para comprobar que tu índice FAISS está funcionando correctamente.
2. **Simplicidad:** Si solo tienes 10 o 20 documentos, es más rápido calcular el coseno uno a uno que inicializar una librería de búsqueda masiva.
3. **Comprensión:** Te permite ver que la búsqueda semántica es, en el fondo, una simple multiplicación y división de listas de números.

## Distancia Euclidiana vs Similitud del Coseno
A veces podríamos tener la tentación de calcular la distancia física, en línea recta, entre dos vectores (Distancia Euclidiana). Sin embargo, en el procesamiento de lenguaje natural esto presenta un problema grave: **la magnitud (tamaño) del vector puede distorsionar el significado**.

- **El problema de la Distancia Euclidiana:** Dos vectores que apuntan exactamente a la misma dirección semántica pero que tienen distinto tamaño (por ejemplo, porque una frase repite la misma idea muchas veces, amplificando la magnitud), tendrán una distancia euclidiana más grande y erróneamente parecerán más diferentes.
- **La solución del Coseno:** La similitud del coseno aísla puramente la **dirección** e ignora la magnitud total del vector. Así, mientras la flecha "apunte" hacia el mismo significado en el espacio vectorial, el sistema comprenderá que ambos conceptos son equivalentes semánticamente, sin dejarse engañar por la longitud del texto o del vector subyacente.
