---
materia: Ingeniería de Software
---
# Taxonomía de la Herencia

La taxonomía de la herencia es una clasificación técnica esencial para evaluar la validez de las jerarquías de clases y garantizar la salud del diseño orientado a objetos.

## Tipos de Relación y su Validez

### 1. Herencia por Especialización (Extensión)
- **Estado:** **CORRECTA**.
- **Dualidad de Procesos:** Se define por la tensión entre la **Especialización** (proceso descendente de refinamiento) y la **Generalización** (proceso ascendente de abstracción de elementos comunes).
- **Garantía de Polimorfismo:** Es el único tipo de herencia que asegura un **Polimorfismo seguro** y predecible, al mantener la integridad del contrato original.
- **Modelos Canónicos:** Relaciones de identidad clara como `Socio -> Persona` o `Empleado -> Persona`.

### 2. Herencia por Limitación
- **Estado:** **INCORRECTA**.
- **Origen Semántico:** Error de diseño derivado de confundir la relación "Es parecido a" con la relación técnica "Es un".
- **Incertidumbre Conductual:** Genera fragilidad en el cliente, quien no puede anticipar qué métodos de la clase base han sido "anulados" o lanzarán excepciones (ej. `UnsupportedOperationException`).
- **Caso de Estudio (Pila):** `Pila` heredando de `Lista`. La Pila intenta limitar la interfaz base anulando `insertarEnPosicion(i)`, violando la expectativa de comportamiento de una `Lista` y el [[Principios de Diseño OO|LSP]].

### 3. Herencia por Construcción
- **Estado:** **INCORRECTA**.
- **Dicotomía Implementación/Interfaz:** El subtipo acepta la **implementación** (código) de la superclase pero rechaza su **interfaz semántica** (contrato).
- **Riesgo de Corrupción:** Exposición accidental de métodos públicos indeseados. 
    - *Ejemplo:* Una `Agenda` que hereda de `Array` y expone erróneamente `sort()` o `clear()`, permitiendo que agentes externos corrompan la lógica interna de la agenda. Sustituir por Composición.
- **Ejemplos Típicos:** `Agenda -> Array`, `Conjunto -> Lista`.

---

## Fundamentos Estructurales
- **Comportamiento vs. Tipo:** Es vital distinguir entre **Herencia de Implementación** (reutilización de código) y **Subtipado** (herencia de contratos e identidad de tipos).
- **Mecánica de Violación LSP:** La herencia por limitación y construcción rompen el [[Principios de Diseño OO|Principio de Sustitución de Liskov]] al debilitar las precondiciones o fortalecer las postcondiciones que el cliente espera de la clase base.

---
## Referencias
1. **Mmasias**. *idsw2: Temario de Ingeniería de Software*.
