---
materia: Ingeniería de Software
categoria: universidad
---
# Gestión de la Configuración y Mantenimiento

Estas disciplinas de soporte en RUP garantizan la integridad del producto a lo largo de su ciclo de vida y aseguran que el software siga siendo útil y funcional tras su entrega.

---

## Gestión de la Configuración y Cambios
Su objetivo es rastrear y controlar los cambios en los artefactos del proyecto (código, modelos, documentos).

### Conceptos Clave
- **Línea de Base (Baseline)**: Una versión revisada y aprobada de un artefacto que sirve como base para el desarrollo posterior. Solo puede cambiarse mediante un procedimiento formal de control de cambios.
- **Espacio de Trabajo (Workspace)**: Entorno aislado donde un desarrollador realiza cambios sin afectar al resto del equipo.
- **Control de Versiones (CVS)**: Herramientas (como Git) que permiten gestionar la historia de cambios, ramificaciones (branches) y fusiones (merges).

### ¿Por qué es crítica esta disciplina?
- Evita la pérdida de trabajo por sobrescritura accidental.
- Permite volver a una versión estable si un cambio introduce errores graves.
- Facilita la **Integración Continua**: La arquitectura se integra y prueba constantemente para producir incrementos de calidad.

---

## Mantenimiento y Evolución
El mantenimiento comienza cuando el software se entrega al cliente. No es solo "arreglar bugs"; es la gestión de la evolución del sistema.

### Tipos de Mantenimiento
1.  **Correctivo**: Reparar defectos encontrados por los usuarios.
2.  **Adaptativo**: Modificar el software para que funcione en un nuevo entorno (ej. cambio de Sistema Operativo o base de datos).
3.  **Perfectivo**: Añadir nuevas funcionalidades o mejorar el rendimiento y la eficiencia.
4.  **Preventivo**: Refactorización y mejora interna para evitar problemas futuros (limpieza de deuda técnica).

### La Evolución en el Modelo de Dominio
¡OJO! El entendimiento del negocio cambia. El **Modelo del Dominio (MdD)** debe evolucionar junto con el conocimiento de la organización. Un modelo rígido que no permite cambios es una señal de fallo en el diseño inicial.

---

## Referencias
1. [[Rational Unified Process]]
2. [[Modelo del Dominio]]
3. **Mmasias**. *idsw1: Temario de la asignatura*. [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw1/README.md|Copia Local]].
