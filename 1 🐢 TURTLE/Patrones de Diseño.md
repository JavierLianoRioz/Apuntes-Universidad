---
materia: Ingeniería de Software
categoria: universidad
---
# Patrones de Diseño (GoF)

Los **Patrones de Diseño** son soluciones probadas y reutilizables para problemas comunes que ocurren durante el diseño de software orientado a objetos. Representan las "mejores prácticas" destiladas por ingenieros experimentados.

---

## ¿Por qué no reinventar la rueda en el diseño de software?
Cada problema de diseño tiene sutilezas que pueden llevar a sistemas rígidos o difíciles de mantener. Los patrones proporcionan un lenguaje común y una estructura robusta para abordar estos retos.

### ¿Cómo clasificamos las soluciones según su propósito?
Los patrones se dividen en tres categorías principales según el problema que resuelven:
1.  **Creacionales**: Se encargan de los mecanismos de creación de objetos, aumentando la flexibilidad y la reutilización del código existente.
2.  **Estructurales**: Explican cómo ensamblar objetos y clases en estructuras más grandes, manteniendo estas estructuras flexibles y eficientes.
3.  **De Comportamiento**: Se encargan de la comunicación efectiva y la asignación de responsabilidades entre objetos.

---

## Patrones Estructurales Clave

### Fachada (Facade)
Proporciona una interfaz unificada y simplificada para un conjunto de interfaces en un subsistema complejo.
- **Problema**: Un sistema tiene muchas piezas moviéndose y el cliente no debería conocer la complejidad interna.
- **Solución**: Una clase "Fachada" que coordina las llamadas a los subsistemas.

```java
// FACHADA: SeguridadFachada.iniciarSesion(usuario, pass)
//   ├─ Coordina: SistemaAutenticacion
//   ├─ Coordina: SistemaAutorizacion
//   └─ Coordina: SistemaNotificacion
```

### Adaptador (Adapter)
Permite que objetos con interfaces incompatibles colaboren.
- **Problema**: Tienes una clase antigua (Legacy) que necesitas usar con una interfaz nueva.
- **Solución**: Una clase intermedia que "traduce" las llamadas.

---

## Patrones Creacionales Clave

### Fábrica Abstracta (Abstract Factory)
Proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas.
- **Uso típico**: Cuando el sistema debe ser independiente de cómo se crean sus productos.

### Singleton
Garantiza que una clase tenga una única instancia y proporciona un punto de acceso global a ella.
- **¡OJO!**: Debe usarse con moderación, ya que puede introducir acoplamiento global y dificultades en las pruebas unitarias.

---

## ¿Cómo elegir el patrón adecuado?
La regla de oro: **No fuerces el uso de patrones**. Un patrón mal aplicado añade complejidad innecesaria (Sobreingeniería). Úsalos solo cuando el diseño lo pida para mejorar la flexibilidad o resolver un problema de acoplamiento real.

---

## Referencias
1. [[Principios de Diseño OO]]
2. **Mmasias**. *idsw2: Temario de la asignatura de Ingeniería de Software*. [GitHub](https://github.com/mmasias/idsw2) / [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/README.md|Copia Local]].
