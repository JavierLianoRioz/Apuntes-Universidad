# Implementación del Pipeline Vectorial

Una de las mejores prácticas para estructurar un motor de [[Búsqueda Semántica]] con [[Bases Vectoriales]] es encapsular toda su lógica en componentes orientados a objetos. Esta separación de responsabilidades facilita construir herramientas reutilizables y aplicables a distintos dominios.

## Encapsulación del Sistema
En lugar de tener el modelo de [[Embedding]] y el índice [[FAISS]] dispersos como funciones separadas, se agrupan en una única clase (por ejemplo, `BuscadorSemantico`). Esto garantiza que los siguientes elementos siempre estén sincronizados:
- Los datos (textos originales).
- El índice vectorial matemático.
- Las funciones internas de transformación de texto a números.

```python
class BuscadorSemantico:
    def __init__(self, base_textos):
        self.base = base_textos
        self.index, self.vectores = self._construir_indice(base_textos)

    def _construir_indice(self, textos):
        # Lógica central para crear embeddings e inyectarlos directamente en FAISS
        pass

    def buscar(self, query, k=3):
        # Lógica controlada de consulta que retorna los K vecinos con score
        pass
```

## Control de Relevancia y Filtrado
Los sistemas en producción no deben devolver cualquier resultado simplemente porque sean "los más cercanos". Se implementan técnicas adicionales de refinamiento:
- **Transformación de Score:** Ya que FAISS (con `IndexFlatL2`) devuelve distancia matemática pura (donde un valor menor indica mejor coincidencia), invertimos y acotamos esto a una métrica de certidumbre (score entre 0 y 1) mediante una transformación aritmética: `score = 1 / (1 + distancia)`.
- **Umbrales de Filtrado:** Las búsquedas pasan por una criba que descarta automáticamente cualquier resultado cuyo score sea menor a un valor mínimo de confianza (ej: `0.5`). Esto previene respuestas basura cuando la consulta del usuario cae "fuera de dominio".

## Inserción Dinámica
Un pipeline vectorizado y maduro permite la ingesta de nuevos datos sobre la marcha sin tener que reconstruir la base completa:
1. Genera el embedding numérico únicamente para el nuevo texto ingresado.
2. Inyecta este nuevo vector dinámicamente en el final del índice FAISS.
3. Actualiza el diccionario interno de metadatos (la matriz que asocia el ID del vector de FAISS con el `String` real original).

## Independencia de Dominio
Una arquitectura así de encapsulada es completamente agnóstica respecto a la información que contiene. Si instanciamos la misma clase `BuscadorSemantico` inicializándola con textos de medicina molecular o con el catálogo de herramientas de una ferretería, el modelo subyacente y la búsqueda funcionarán a la perfección sin requerir absolutamente ningún rediseño de código. Esto expone la potencia real del [[Espacio Vectorial]].