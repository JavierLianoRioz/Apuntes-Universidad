---
materia: Ingeniería de Software
categoria: universidad
---
# Priorizar Casos de Uso

La **Priorización** es el proceso estratégico de decidir qué casos de uso se implementarán primero. En un mundo de recursos y tiempo limitados, esta actividad es vital para gestionar la incertidumbre y entregar valor lo antes posible.

---

## ¿Por qué no todas las funcionalidades deben construirse al mismo tiempo?
Intentar construir todo a la vez es el camino más rápido hacia el caos. Necesitamos un orden lógico que garantice la estabilidad del sistema.

### ¿Qué riesgos mitigamos al elegir el orden correcto?
Priorizar no es solo una cuestión de preferencia del cliente, sino de supervivencia del proyecto:
- **Gestionar Riesgos**: Atacamos lo más difícil o incierto al principio —si vamos a fallar, mejor hacerlo pronto y barato—.
- **Planificar Iteraciones**: Proporciona el criterio para decidir qué funcionalidades entrarán en cada ciclo de desarrollo.
- **Gestionar Expectativas**: Asegura que el cliente vea el mayor valor de negocio en las etapas tempranas.

### ¿En qué variables nos basamos para tomar decisiones estratégicas?
Evaluamos los CdU utilizando cuatro ejes fundamentales:
- **Valor para el Negocio**: ¿Qué tan crítico es este proceso para que la empresa funcione?
- **Riesgo Técnico**: ¿Es una tecnología que desconocemos o un algoritmo de alta complejidad?
- **Arquitectura**: ¿Este CdU ayuda a definir la estructura base y los cimientos del sistema?
- **Dependencias**: ¿Existen otras funcionalidades que no pueden existir sin esta?

**La regla de oro:** Primero se implementa aquello que tiene **más riesgo técnico** y **más valor arquitectónico**.

---

## ¿Cómo ejecutamos la priorización en un entorno cambiante?
La priorización no es una foto fija al inicio del proyecto; es un proceso dinámico que evoluciona con el aprendizaje del equipo.

### ¿De qué manera evoluciona la estrategia a lo largo del proyecto?
A medida que avanzamos, el conocimiento sobre el dominio y la tecnología aumenta, permitiéndonos ajustar el rumbo.

| Factor de Decisión | Acción Sugerida |
| :--- | :--- |
| **Alto Riesgo + Alta Arquitectura** | Implementar obligatoriamente en la Fase de Elaboración (Iteraciones tempranas). |
| **Bajo Riesgo + Alto Valor** | Implementar durante la Fase de Construcción para completar el producto. |
| **Baja Prioridad / Poca Visibilidad** | Dejar para las últimas iteraciones o descartar si el presupuesto se agota. |

> [!IMPORTANT] Objetivos de la Priorización
> El objetivo final es equilibrar la entrega de valor constante con una gestión efectiva de los recursos. Si algo es muy arriesgado, queremos descubrir sus problemas antes de haber invertido todo el presupuesto.

---

## Referencias
1. **Mmasias**. *idsw1: Temario de la asignatura de Ingeniería de Software*. [GitHub](https://github.com/mmasias/idsw1) / [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw1/README.md|Copia Local]].
