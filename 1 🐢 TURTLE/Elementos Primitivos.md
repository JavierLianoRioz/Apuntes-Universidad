---
materia: Ingeniería de Software
---
# Elementos Primitivos

En el contexto de la **[[Complejidad del Software]]** y el estudio de los sistemas complejos, los **Elementos Primitivos** son las unidades básicas o componentes de más bajo nivel en una jerarquía que ya no se descomponen más para el propósito del análisis actual.

---

## ¿Hasta dónde debemos descomponer un sistema para entender su esencia?
La descomposición es una herramienta fundamental de la inteligencia humana, pero requiere un punto de parada para no caer en el infinito.

### ¿Por qué lo que es simple para unos es complejo para otros?
La elección de qué componentes son "primitivos" es relativamente arbitraria y depende enteramente del observador. No existe un elemento primitivo absoluto en el universo del software; su definición es una decisión de diseño.

**La regla de oro:** ==Un elemento es primitivo cuando el detalle de su funcionamiento interno ya no es relevante para entender el comportamiento del sistema que lo contiene.==

### ¿Cómo cambia la unidad básica según el punto de vista del observador?
Para ilustrar esta relatividad, podemos observar cómo cambian las primitivas según el dominio:

- **Cartografía:** Para un geógrafo político, la unidad primitiva es el **país**; para un urbanista, es el **distrito**.
- **Organizaciones:** Para un general, la primitiva es el **batallón**; para un sargento, es el **soldado**.
- **Software:** 
	- En arquitectura de sistemas, las primitivas pueden ser los **servicios o contenedores**.
	- En la programación, son los **tipos de datos básicos** (integers, booleans) o las sentencias del lenguaje.

---

## ¿Cómo utilizamos la atomicidad para construir mejores abstracciones?
Decidir qué es primitivo es el primer paso para ocultar la complejidad innecesaria.

### ¿De qué manera la elección de primitivas afecta a la encapsulación?
Al definir un límite donde un componente se considera primitivo, estamos aplicando activamente la **Abstracción** y la **Encapsulación**. Estamos trazando una línea donde el "cómo" interno deja de importar para centrarnos únicamente en el "qué" ofrece esa pieza al resto del sistema superior.

---

Por lo que un elemento primitivo no es un sistema de mínimo común múltiplo, sino es un sistema que nos asegura no definir complejidad inútil que ensucie el sistema.

---

## Referencias
1. **Mmasias**. *idsw2: Software y Sistemas Complejos*. [GitHub Repository](https://github.com/mmasias/idsw2).
2. **Booch, G.** *Análisis y Diseño Orientado a Objetos con Aplicaciones*.
