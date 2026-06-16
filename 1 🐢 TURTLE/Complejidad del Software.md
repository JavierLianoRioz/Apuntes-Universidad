---
materia: Ingeniería de Software
---
# Complejidad del Software

**Definición de Brad Cox:** El software es "información suministrada por el desarrollador para que el ordenador manipule de forma automática la información del usuario".

El desarrollo de software es considerado por muchos —como Frederick Brooks— como el trabajo más complejo que jamás haya emprendido la humanidad. Esta complejidad no es accidental, sino inherente a la naturaleza del software.

#### Asimetría Hombre-Máquina
La complejidad se dispara por la brecha de capacidades:
- **Humano:** Sobresale en reconocimiento de **patrones cualitativos** pero es lento y propenso al error en cálculos repetitivos.
- **Máquina:** Posee capacidad **cuantitativa infinita** (velocidad y precisión sin cansancio) pero carece de juicio semántico.

---

## ¿Qué hace que un sistema sea intrínsecamente complejo?
Un sistema de software no es solo código; es un conjunto de clases, módulos y paquetes que se relacionan mediante herencia, composición y paso de mensajes. Según Grady Booch, los sistemas complejos comparten características fundamentales:

### ¿Cuáles son las leyes que rigen la estructura del software?
- **Estructura Jerárquica**: Descomposición recursiva en subsistemas hasta alcanzar [[Elementos Primitivos]].
- **Primitivos Relativos**: La definición del nivel "base" es subjetiva al observador (ej. arquitecto vs. urbanista).
- **Separación de Asuntos (SoC)**: Las conexiones intra-componente (cohesión) deben ser más fuertes que las inter-componente (acoplamiento).
- **Patrones Comunes**: Reutilización de combinaciones finitas de subsistemas que unifican la jerarquía.
- **Ley de Gall (Formas Intermedias Estables)**: ==Un sistema complejo diseñado desde cero **nunca** funcionará. Siempre debe evolucionar incrementalmente desde un sistema simple funcional.==

---

### ¿Qué herramientas conceptuales nos permiten vencer la entropía?
Para gestionar esta complejidad, la ingeniería de software se apoya en cuatro pilares:
1.  **Abstracción**: Proceso de extraer las características esenciales ignorando detalles superfluos.
2.  **Encapsulación**: Oculta los detalles de implementación de una abstracción.
3.  **Modularidad**: Descomposición en piezas poco acopladas y muy cohesivas.
4.  **Jerarquía**: Ordenamiento de las abstracciones (clasificación o composición).

#### Jerarquización de Sistemas Complejos
Propiedades de una jerarquía sana:
- **Acíclica:** Sin dependencias mutuas.
- **Direccional:** Flujo de dependencia vertical constante hacia capas inferiores.
- **Estable:** El núcleo debe cambiar con menos frecuencia que la periferia.

**La regla de oro:** ==El principal enemigo de la fiabilidad y la calidad del software es la complejidad. Todo aquello que no sea necesario dar a conocer, **no se debe dar a conocer**.==

---

## ¿Cómo podemos dimensionar el reto al que nos enfrentamos?
Para entender la magnitud de lo que construimos, usamos la **Métrica Quijotesca**:

| Métrica | Don Quijote | Proyecto Software (Mediano) |
| :--- | :--- | :--- |
| **Extensión** | ~300.000 palabras | ~100.000 líneas (~300.000 palabras) |
| **Entidades** | Decenas (personajes) | Centenares (identificadores/clases) |
| **Interconectividad** | Lineal/Narrativa | Alta (grafos de dependencias) |

**Conclusión:** El software de una aplicación media excede con creces la capacidad intelectual humana individual.

---

## ¿Cómo medimos la complejidad de forma objetiva?
Más allá de la percepción cualitativa, existen métricas que permiten cuantificar el riesgo y la dificultad de mantenimiento de un fragmento de código.

### Complejidad Ciclomática (Métrica de McCabe)
Esta métrica mide el número de **caminos independientes** a través del código fuente de un programa. Cuantos más caminos (if, while, for, switch), mayor es la probabilidad de error y más difícil es probar el sistema.

- **La fórmula básica:** $M = E - N + 2P$
    - $E$: Número de aristas (conexiones).
    - $N$: Número de nodos (instrucciones).
    - $P$: Componentes conexos (normalmente 1).
- **Interpretación de resultados:**
    - **1-10**: Código simple y fácil de probar.
    - **11-20**: Código complejo; riesgo moderado.
    - **21-50**: Código muy complejo; riesgo alto. **¡OJO!** Se recomienda refactorizar.
    - **>50**: Código inmanejable; peligro extremo.

**La regla de oro:** Mantener la complejidad ciclomática por debajo de **10-15** por método garantiza que el código sea legible y testeable.

---

## Referencias
1. **Mmasias**. *idsw2: Temario de la asignatura de Ingeniería de Software II*. [GitHub Repository](https://github.com/mmasias/idsw2) y en copia local: [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/00-introduccion/software.md|Software y Complejidad]].
