---
materia: Ingeniería de Software
---
# Diseño Modular

El **Diseño Modular** es el proceso de descomponer un sistema de software en un conjunto de piezas —módulos— poco acopladas y altamente cohesivas. Su objetivo es dominar la complejidad permitiéndonos entender, cambiar o corregir partes del sistema de forma aislada.

---

## ¿Cómo podemos dividir un problema inabordable en piezas manejables?
Enfrentarse a un sistema monolítico es una tarea imposible para la mente humana. La modularidad nos permite aplicar el principio de *divide et impera* para reducir la carga cognitiva.

### ¿En qué métricas nos basamos para evaluar la calidad de un módulo?
Un buen diseño modular se basa en equilibrar tres métricas fundamentales que determinan la salud de la arquitectura:

1.  **[[Cohesión]]**: Mide qué tan fuerte están relacionadas las responsabilidades dentro de un solo módulo. Buscamos que un módulo haga "una sola cosa y la haga bien" (Cohesión Funcional).
2.  **[[Acoplamiento]]**: Mide el grado de interdependencia entre módulos. Buscamos minimizar las dependencias para que un cambio en una pieza no rompa el resto del sistema.
3.  **Tamaño Adecuado**: Los componentes deben respetar los límites cognitivos humanos para ser comprensibles.
    - **Regla 7±2 (Miller)**: La memoria de trabajo humana solo puede retener unos 7 elementos simultáneamente.
    - **Ley de Proximidad (Gestalt)**: La lógica relacionada debe mantenerse cercana físicamente para no sobrecargar la memoria de trabajo.
    - **Cotas Dimensionales Óptimas:**
        - **Clase:** Máximo 5 atributos, 20-25 métodos, y 200-500 líneas de código (LOC).
        - **Método:** Máximo 2-3 parámetros (solución: **Objetos de Configuración**), 15-25 líneas de código, y máximo 3 niveles de anidación.
        - **Paquete:** Máximo 12-20 clases para mantener la cohesión.
    - **Complejidad Ciclomática (McCabe)**: Mide el número de caminos independientes en el código (`CC = Condiciones + Salidas`). 1-10 (Simple), 11-20 (Complejo), >20 (Refactorizar urgentemente).

#### Dimensiones de la Ineficacia Arquitectónica
- **Ineficacia (Plazo):** El tiempo de entrega se dispara.
- **Ineficiencia (Coste):** El consumo de recursos excede el valor.
- **Inefectividad (Ámbito):** El sistema no cumple con el objetivo de negocio.

#### Cuadrante de Mantenibilidad
Identificación de síntomas según la incapacidad del sistema:
- **Viscoso:** Difícil de entender (Estructura desorganizada).
- **Rígido:** Difícil de modificar (Cambios en cascada).
- **Inmóvil:** Difícil de reutilizar (Alto acoplamiento).
- **Frágil:** Difícil de probar (Efectos secundarios inesperados).


### ¿Qué herramientas conceptuales protegen la integridad de nuestro diseño?
Para lograr una modularidad efectiva, nos apoyamos en dos conceptos clave que actúan como fronteras:
- **Abstracción**: Define la interfaz o "vista exterior" de lo que hace el módulo, ocultando la complejidad subyacente.
- **Encapsulación**: Oculta los detalles internos de cómo se realiza la tarea, protegiendo al resto del sistema de cambios en la implementación.

**La regla de oro:** El bajo acoplamiento y la alta cohesión forman un círculo virtuoso; delegar responsabilidades a los objetos apropiados mejora ambos simultáneamente.

---

## ¿Cómo implementamos una arquitectura que resista el paso del tiempo?
El diseño modular no es solo una estructura estática; es una disciplina de interacción que debe guiar cada línea de código.

### ¿Qué reglas de oro guían la interacción entre objetos?
- **Tell, Don't Ask**: Indica a los objetos qué hacer en lugar de pedirles sus datos para decidir tú. Esto reduce el acoplamiento y respeta la encapsulación.
- **Programación contra Interfaces**: Depende de abstracciones en lugar de implementaciones concretas. Esto permite intercambiar componentes (ej. cambiar un motor de base de datos) sin afectar al resto del sistema.
- **Ley de Demeter**: "No hables con extraños". Un objeto solo debe comunicarse con sus "amigos cercanos" (sus propios atributos, parámetros u objetos que él mismo cree).

### ¿Cómo identificamos cuando nuestro diseño está empezando a degradarse?
Un diseño modular en decadencia suele presentar síntomas claros —conocidos como *code smells*— que debemos atajar cuanto antes:
- **Rigidez**: El sistema es difícil de cambiar porque cualquier modificación afecta a demasiadas partes inconexas.
- **Fragilidad**: El software se rompe en lugares inesperados tras realizar un cambio aparentemente inofensivo.
- **Inmovilidad**: Es imposible reutilizar partes del sistema en otros proyectos porque están demasiado "pegadas" entre sí.

---

## Referencias
1. **Mmasias**. *idsw2: Diseño Modular*. [GitHub Repository](https://github.com/mmasias/idsw2) y en copia local: [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/02-diseñoModular/README.md|Temario Diseño Modular]].
