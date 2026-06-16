---
materia: Ingeniería de Software
categoria: universidad
---
# Estructurar el Modelo de Casos de Uso

Estructurar el modelo de casos de uso (CdU) es la actividad de la disciplina de Requisitos que se encarga de simplificar y organizar el modelo para evitar la redundancia, facilitar la mantenibilidad y clarificar las relaciones entre los requisitos funcionales.

---

## ¿Por qué es necesario estructurar el modelo de casos de uso?

Durante la fase de especificación, el modelo de casos de uso puede crecer descontroladamente y llenarse de duplicidades. La estructuración aplica principios de modularidad y reutilización para:
- Extraer funcionalidad común compartida por múltiples casos de uso.
- Aislar flujos opcionales o excepcionales sin oscurecer la lógica principal.
- Organizar el modelo en paquetes cohesivos para reducir la carga cognitiva de los desarrolladores y stakeholders.

---

## ¿Cuáles son las relaciones clave entre Casos de Uso?

Se descompone de la siguiente manera mediante tres relaciones fundamentales en UML:

```javascript
// EL ESQUELETO: [Caso de Uso Origen] ─── <<tipo_relación>> ───> [Caso de Uso Destino]
```

### 1. Inclusión (`<<include>>`)
Una relación de inclusión indica que el caso de uso origen **requiere incondicionalmente** del comportamiento del caso de uso destino para completar su flujo.
- **Propósito:** Evitar la duplicación de especificaciones de comportamiento común.
- **Ejemplo:** `Procesar Pago` es un `<<include>>` obligatorio tanto de `Comprar Producto` como de`Pagar Suscripción`.

### 2. Extensión (`<<extend>>`)
Una relación de extensión indica que el caso de uso de extensión (origen) **puede insertar condicionalmente** su comportamiento en el caso de uso base (destino).
- **Propósito:** Mantener el flujo base limpio y permitir la extensibilidad opcional del sistema.
- **Punto de Extensión:** La posición específica en el caso de uso base donde se puede insertar el flujo alternativo.
- **Ejemplo:** `Aplicar Descuento` extiende a `Calcular Total` solo si se cumple la condición "El usuario tiene un cupón válido".

### 3. Generalización
Indica que un caso de uso hijo hereda el comportamiento, los puntos de extensión y las relaciones del caso de uso padre, pudiendo añadir o sobrescribir comportamiento.
- **Propósito:** Modelar especializaciones de procesos de negocio.
- **Ejemplo:** `Autenticarse con Huella` es una generalización del caso de uso padre `Autenticarse`.

---

## ¿Cómo se diferencian los casos de uso concretos de los abstractos?

La regla de oro de la estructuración distingue el nivel de instanciación de los casos de uso:

- **Casos de Uso Concretos:** Son iniciados directamente por un actor y representan una secuencia completa de acciones que aporta valor directo al negocio.
- **Casos de Uso Abstractos:** No son instanciados por sí mismos de forma aislada. Existen únicamente para ser reutilizados por otros casos de uso mediante relaciones de inclusión, extensión o generalización.

---

## ¿Cuáles son los criterios y beneficios de una buena estructuración?

La toma de decisiones de diseño en el modelo debe equilibrar tres factores críticos:

| Factor | Criterio de Diseño | Beneficios Obtenidos |
| :--- | :--- | :--- |
| **Cohesión** | Agrupar los casos de uso en paquetes funcionales según el dominio del negocio. | **Comprensión:** Separación lógica y organización jerárquica clara del sistema. |
| **Minimización de Dependencias** | Reducir y documentar claramente los acoplamientos entre casos de uso de distintos paquetes. | **Mantenibilidad:** Los cambios en un módulo específico no propagan fallos a otros. |
| **Reutilización** | Extraer operaciones obligatorias comunes como `include` y variaciones opcionales como `extend`. | **Escalabilidad:** Estructura limpia preparada para incorporar nuevas funcionalidades. |

**¡OJO!** Un error típico de diseño es abusar de las relaciones `<<include>>` para realizar una descomposición funcional del sistema (dividir un caso de uso simple en pequeños "pasos" secuenciales como notas individuales). Esto destruye la semántica de RUP: un caso de uso debe representar una secuencia de acciones completa y con valor de negocio para un actor.
