---
materia: Bases de Datos 2
---

# Simulacro de Examen: Bases de Datos 2 (MongoDB & Neo4j)

Este simulacro consta de **10 preguntas prácticas** distribuidas entre MongoDB y Neo4j, simulando la estructura final del examen. Se han omitido todas las preguntas teóricas para centrarse exclusivamente en la resolución técnica.

---

## Bloque 1: MongoDB (5 Ejercicios)

### ¿Cómo operamos sobre documentos y rendimiento?

**Ejercicio 1 (CRUD):** En la colección `cursos`, inserta un documento con: `nombre: "Arquitectura de Software"`, `nivel: "avanzado"`, `creditos: 6`, `departamento: "Informatica"` y `profesor: "Dr. Lopez"`.

```js
db.cursos.insertOne(
	{
		nombre: "Arquitectura de Software",
		nivel: "avanzado",
		creditos: 6,
		departamento: "Informatica",
		profesor: "Dr. Lopez"
	}
)
```

**Ejercicio 2 (Update):** Actualiza el curso "Arquitectura de Software" para que pase a tener **7 créditos**.

**Ejercicio 3 (Aggregation):** Utilizando la colección `sensores`, calcula la **temperatura promedio** agrupada por cada `zona`. El documento resultante debe tener la estructura `{ _id: "nombre_zona", promedio: valor }`.

**Ejercicio 4 (Aggregation):** En la colección `libros`, calcula el **total de libros** disponibles por cada `categoria`.

**Ejercicio 5 (Optimización):** Crea un **índice compuesto** en la colección `cursos` que cubra los campos `nivel` (ascendente) y `creditos` (descendente).

---

## Bloque 2: Neo4j Cypher (5 Ejercicios)

### ¿Cómo navegamos y consultamos el grafo?

**Ejercicio 6 (Match):** Obtén todas las personas que trabajan en alguna empresa y muestra el nombre de la persona y de la empresa.

**Ejercicio 7 (Agregación):** Obtén las empresas junto con el número total de empleados que tiene cada una.

**Ejercicio 8 (Filtros):** Encuentra los nombres de las personas que viven en una ciudad distinta a la de sus amigos.

**Ejercicio 9 (Caminos):** Encuentra todos los caminos (paths) de amistad de longitud entre 1 y 3 saltos entre personas, devolviendo el path y su longitud.

**Ejercicio 10 (Funciones):** Obtén los nombres de las personas junto con todas las tecnologías que usan, agrupadas en una lista (colección).

---

## ¿Cómo preparamos el entorno de pruebas?

### Para MongoDB

Asegúrate de cargar los datasets de `universidad`, `tienda`, `iot` y `biblioteca` disponibles en `8 📚 BIBLIOTECA/9 💢 OTROS/Examenes-Practicos/`.

### Para Neo4j

Se asume un esquema con etiquetas `:Persona`, `:Empresa`, `:Ciudad`, `:Proyecto` y `:Tecnologia`, y relaciones como `:TRABAJA_EN`, `:VIVE_EN`, `:AMIGO_DE` y `:USA_TECNOLOGIA`.

---

## Consejos de Examen

- **¡OJO!** — En MongoDB, usa `explain("executionStats")` para verificar si tus índices se están usando (etapa `IXSCAN`).
- **La regla de oro:** En Cypher, usa `DISTINCT` cuando realices conteos o recolectes listas para evitar duplicados si hay múltiples caminos.

---

## Referencias

1. [[MongoDB]] — Guía rápida de comandos.
2. [[Cypher]] — Guía rápida de grafos.
3. [[8 📚 BIBLIOTECA/9 💢 OTROS/preguntas_grafos.md|Banco de ejercicios Neo4j]] — Fuente original.

---

[[Bases de datos 2|⬅️ Volver a la nota de la asignatura]]
