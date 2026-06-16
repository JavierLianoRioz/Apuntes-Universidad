---
materia: Ingeniería de Software
---
# Principios de Diseño OO (SOLID)

Los principios **SOLID** son un conjunto de cinco reglas de diseño orientado a objetos que, aplicadas en conjunto, permiten crear sistemas más fáciles de mantener, escalar y entender. Son la base fundamental para combatir la rigidez y la fragilidad del software.

---

## ¿Qué pilares sostienen un diseño orientado a objetos profesional?
En el desarrollo de software, el cambio es la única constante. Los principios SOLID actúan como un escudo contra el caos que genera el crecimiento descontrolado del código.

### ¿De qué manera estas cinco reglas combaten la rigidez del software?
1.  **SRP: Responsabilidad Única** (Single Responsibility)
    - *Concepto:* Una clase debe tener una sola razón para cambiar —debe servir a un único actor—.
    - *Ejemplo (Empleado):* Separar la información personal del `Empleado` de la lógica de `CalculadoraSalario`.

2.  **OCP: Abierto/Cerrado** (Open/Closed)
    - *Concepto:* El software debe estar **abierto para la extensión**, pero **cerrado para la modificación**.

3.  **LSP: Sustitución de Liskov** (Liskov Substitution)
    - *Concepto:* Las clases derivadas deben poder sustituir a sus clases base sin alterar el comportamiento esperado.

4.  **ISP: Segregación de Interfaces** (Interface Segregation)
    - *Concepto:* Los clientes no deben ser forzados a depender de interfaces que no utilizan.

5.  **DIP: Inversión de Dependencias** (Dependency Inversion)
    - *Concepto:* Depende de abstracciones (interfaces), no de implementaciones concretas.

---

## ¿Cómo elegimos la estructura de relación adecuada?
La decisión entre herencia y composición marca la diferencia entre un sistema flexible y uno rígido.

### Herencia vs. Composición: ¿Cuándo usar cada una?

- **Heurística #2Think (Composición sobre Herencia)**: La herencia fija el comportamiento en tiempo de compilación (estático). La composición permite extraer la variabilidad a interfaces (Patrón Strategy) y cambiar colaboradores en **tiempo de ejecución** (Runtime).

**Diferenciación Práctica en Implementación:**
- **Uso vs. Asociación**: El **Uso** es la relación más débil; la referencia es *efímera* (parámetro o variable local en un método).
- **Composición vs. Agregación**: 
  - **Composición (Exclusiva)**: El ciclo de vida está ligado (instanciación dentro del constructor).
  - **Agregación (Compartida)**: El ciclo de vida es independiente (inyección desde el exterior).

### Antipatrón: Descomposición Funcional
Ocurre al transicionar de programación estructurada a OO sin cambiar la mentalidad.
- **Clases-Verbo:** Convertir cada función en una clase (ej. `CalcularPrecio`, `ValidarDatos`).
- **Síntomas:** Clases con un único método (`ejecutar()`), sin estado, que actúan como meros contenedores de lógica procedural (clases anémicas).
- **Impacto:** Degrada la [[Cohesión]] y anula las ventajas del polimorfismo.

---

### Doble Despacho (Double Dispatch)
Es una técnica para eliminar el uso de `instanceof` en jerarquías donde el comportamiento depende de dos tipos de objetos. Se basa en el **Patrón Visitor**:
1.  **Primer Despacho**: El objeto llama a `aceptar(visitante)`.
2.  **Segundo Despacho**: Dentro de `aceptar`, el objeto llama a `visitante.visitar(this)`.

---

## Referencias
1. **Mmasias**. *idsw2: Diseño Orientado a Objetos*. [GitHub Repository](https://github.com/mmasias/idsw2) y en copia local: [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/03-diseñoOO/README.md|Temario Diseño OO]].
