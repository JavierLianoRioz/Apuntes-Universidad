---
materia: Ingeniería de Software
---
# Diseño por Contrato (DbC)

El **Diseño por Contrato** es un enfoque que formaliza las obligaciones mutuas entre los componentes de un sistema. En lugar de usar programación defensiva (verificaciones redundantes), establecemos acuerdos claros de quién es responsable de qué.

---

## ¿En qué consiste el "Acuerdo" entre componentes?
Un contrato se define mediante tres pilares fundamentales que deben cumplirse para garantizar la fiabilidad del software:

1.  **Precondiciones**: Lo que el cliente (quien llama) debe garantizar antes de invocar el método.
    - *Si falla:* El error es del **cliente** (bug en el uso).
2.  **Postcondiciones**: Lo que el proveedor (el método) garantiza después de su ejecución.
    - *Si falla:* El error es del **proveedor** (bug en la implementación).
3.  **Invariantes de Clase**: Condiciones que deben ser ciertas durante toda la vida del objeto (antes y después de cada llamada pública).

---

## ¿Cómo implementamos estos contratos en el código?
En lenguajes como Java, utilizamos mecanismos distintos según la naturaleza del fallo:

### Assert vs. Excepciones
- **`assert`**: Se usa para verificar precondiciones en **código interno** (bajo nuestro control). Se pueden desactivar en producción.
- **Excepciones**: Se usan en la **frontera del sistema** (entrada de usuario, APIs externas) para manejar condiciones de error que no son necesariamente bugs de programación.

| Situación | Mecanismo | Justificación |
| :--- | :--- | :--- |
| Bug del programador | `assert` | El contrato se ha roto por un error de lógica. |
| Error de entorno/usuario | `Exception` | Condición esperable que el sistema debe gestionar. |

---

## ¿Por qué el diseño por contrato mejora la calidad?
- **Localización del Fallo**: El error salta exactamente donde se viola el contrato, no "varias llamadas después".
- **Documentación Viva**: Los contratos actúan como documentación técnica que no se desactualiza.
- **Elimina Redundancia**: Si el contrato garantiza que un dato no es nulo, no hace falta volver a comprobarlo dentro del método.

**La regla de oro:** "Hable con sus amigos, no con extraños", pero asegúrese de que sus amigos cumplan su palabra (contrato).

---

## Violaciones del Contrato en la Herencia
Un diseño por contrato sólido exige coherencia en la jerarquía (LSP):
- **Herencia por Limitación:** La subclase restringe el contrato de la base (ej. lanza `UnsupportedOperationException`). Es una violación crítica que rompe el polimorfismo.
- **Referencia:** Ver [[Taxonomía de la Herencia]] para casos de uso correcto e incorrecto.

---

## Referencias
1. **Bertrand Meyer**. *Object-Oriented Software Construction*. (Creador del concepto).
2. **Mmasias**. *idsw2: Diseño por contrato*. [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/02-diseñoModular/diseñoContrato.md|Temario DbC]].
