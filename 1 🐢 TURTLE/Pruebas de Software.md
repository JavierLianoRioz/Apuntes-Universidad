---
materia: Ingeniería de Software
categoria: universidad
---
# Pruebas de Software (Verificación y Validación)

La disciplina de **Pruebas** (Testing) en la Ingeniería de Software tiene como objetivo evaluar la calidad del producto, identificar defectos y verificar que el sistema cumple con los requisitos especificados.

---

## ¿Qué diferencia la Verificación de la Validación?
Aunque a menudo se usan como sinónimos, representan dos preguntas fundamentales distintas:
- **Verificación**: "¿Estamos construyendo el sistema correctamente?" (Cumplimiento de especificaciones técnicas).
- **Validación**: "¿Estamos construyendo el sistema correcto?" (Satisfacción de las necesidades reales del usuario).

---

## Niveles de Prueba
Las pruebas se organizan de forma jerárquica, desde la unidad más pequeña hasta el sistema completo:

1.  **Pruebas Unitarias**: Verifican el funcionamiento de un componente o clase de forma aislada.
    - *Objetivo:* Localizar errores en la lógica interna.
    - *Herramienta:* xUnit (JUnit, etc.).
2.  **Pruebas de Integración**: Verifican que los componentes interactúan correctamente entre sí.
    - *Objetivo:* Detectar fallos en las interfaces y la comunicación entre módulos.
3.  **Pruebas de Sistema**: Evalúan el sistema completo e integrado para verificar que cumple con los requisitos funcionales y no funcionales.
4.  **Pruebas de Aceptación**: Realizadas (o supervisadas) por el cliente para decidir si el producto está listo para su despliegue.

---

## ¿Cómo diseñamos pruebas efectivas?
Existen dos enfoques principales para diseñar casos de prueba:

### Pruebas de Caja Blanca (Estructurales)
Se basan en el conocimiento del código interno. El objetivo es cubrir todos los caminos de ejecución.
- **Métrica clave**: [[Complejidad del Software|Complejidad Ciclomática (McCabe)]]. Un valor alto indica que se necesitan más casos de prueba.

### Pruebas de Caja Negra (Funcionales)
Se basan en las especificaciones (entradas y salidas) sin mirar el código.
- **Base de diseño**: Los [[1 🐢 TURTLE/Casos de Uso]] y sus flujos (principal, alternativo y excepciones) son la fuente principal para generar estos tests.

---

## La Regla de Oro del Testing
==El testing no puede demostrar la ausencia de errores, solo su presencia.== Un sistema con todas las pruebas pasadas no es "perfecto", sino "suficientemente bueno" según los criterios de aceptación definidos.

---

## Referencias
1. [[Ingeniería de Software]]
2. [[1 🐢 TURTLE/Casos de Uso]]
3. **Mmasias**. *idsw1 e idsw2: Temario de la asignatura*. [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw1/README.md|Copia Local]].
