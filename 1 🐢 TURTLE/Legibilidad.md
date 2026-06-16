---
materia: Ingeniería de Software
---
# Legibilidad (Clean Code)

La **Legibilidad** es el principio que asegura que el código sea comprensible para los seres humanos. Como decía Tom Love: *"Una línea de código se escribe una vez y se lee cientos de veces"*.

---

## ¿Cómo escribimos código que hable por sí mismo?
Un código legible reduce la deuda técnica y facilita el mantenimiento. Se basa en tres pilares:

### 1. Nombrado con Intención
Los nombres deben revelar el propósito, no la implementación.
- **CamelCase**: Estándar para clases (`ClaseEjemplo`) y métodos (`metodoEjemplo`).
- **Nombres del Dominio**: Usa términos del negocio (ej. `Saldo`, `Cliente`) en lugar de términos técnicos genéricos.
- **Evita Codificaciones**: No uses prefijos tipo `strNombre` o `intEdad` (Notación Húngara). El tipo lo da el lenguaje, el nombre da la **intención**.

### 2. Comentarios: ¿Ayuda o Confesión?
Un comentario suele ser una señal de que el código no es lo suficientemente claro.
- **👍 Comentarios Aclaratorios**: Explican el "por qué" de una decisión compleja o legal.
- **💩 Comentarios Redundantes**: `i++; // Incrementa i`. Estorban y se desactualizan.
- **Regla de Oro**: *"No comentes código malo, re-escríbelo"*.

### 3. Formato y Jerarquía
El código debe tener una estructura visual que refleje su lógica.
- **Sangría (Indentación)**: Hace visible la jerarquía de ámbitos.
- **Líneas en Blanco**: Separan grupos lógicos de operaciones.
- **Cercanía**: Las variables deben declararse cerca de donde se usan.

---

## ¿Qué principios universales rigen la calidad del código?
Existen tres acrónimos que todo ingeniero debe tener grabados:

- **DRY (Don't Repeat Yourself)**: Evita la duplicidad de conocimiento. Cada pieza de lógica debe tener una única representación en el sistema.
- **YAGNI (You Aren't Going to Need It)**: No añadas funcionalidades "por si acaso". Implementa las cosas cuando realmente las necesites.
- **KISS (Keep It Simple, Stupid)**: La simplicidad es el grado máximo de sofisticación. Evita la sobreingeniería.

---

## Referencias
1. **Robert C. Martin**. *Clean Code: A Handbook of Agile Software Craftsmanship*.
2. **Mmasias**. *idsw2: Legibilidad*. [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/01-diseño/03-legibilidad.md|Temario Legibilidad]].
