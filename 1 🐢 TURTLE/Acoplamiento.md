---
materia: Ingeniería de Software
---
# Acoplamiento

El **Acoplamiento** es la métrica que evalúa el grado de interdependencia entre los componentes de un sistema. En un diseño ideal, buscamos un **bajo acoplamiento** para que los cambios queden localizados y no se propaguen en una reacción en cadena.

---

## ¿Por qué la interdependencia excesiva es el enemigo silencioso del cambio?
Cuando dos módulos están demasiado unidos, pierden su autonomía. Un cambio en la interfaz de uno obliga a reescribir el otro, multiplicando el esfuerzo y el riesgo de errores.

### ¿De qué maneras pueden quedar "encadenados" nuestros componentes?
Podemos clasificar el acoplamiento según su naturaleza y la dirección de la dependencia:

- **Aferente (Ca)**: Indica cuántas clases externas dependen de ti. Mide tu "popularidad" y el riesgo de que un cambio en tu código rompa a otros.
- **Eferente (Ce)**: Indica de cuántas clases externas dependes tú. Un valor alto te hace frágil ante cambios ajenos.
- **Acoplamiento de Contenido (Evitar)**: Ocurre cuando un módulo modifica directamente el estado interno de otro —una violación total de la encapsulación—.
- **Directo vs Indirecto**: Las dependencias pueden ser explícitas (herencia) o a través de intermediarios que ocultan la verdadera complejidad.

### ¿Qué dimensiones definen la fuerza de una conexión?
El acoplamiento no es solo "usar otra clase"; tiene matices técnicos que determinan qué tan difícil será cambiar esa relación:

1.  **Visibilidad**: ¿Es la relación exclusiva (Privada) o compartida (Pública)?
2.  **Temporalidad**:
    - *Efímera:* Limitada a una operación específica (Uso).
    - *Persistente:* Durante toda la vida del objeto (Composición).
3.  **Versatilidad**: Capacidad de intercambiar colaboradores. Baja versatilidad implica dependencia de clase concreta; alta versatilidad implica dependencia de interfaz.


**La regla de oro:** Minimiza la visibilidad, acorta la temporalidad y maximiza la versatilidad.

---

### ¿Cómo podemos limitar el conocimiento mutuo entre los objetos?
Para combatir el acoplamiento, aplicamos la **Ley de Demeter (LoD)** —también llamada "Principio del Menor Conocimiento"—. Esta dicta que un método solo debe interactuar con sus "amigos cercanos":
1.  El propio objeto.
2.  Sus propios atributos.
3.  Los parámetros que recibe el método.
4.  Objetos creados dentro del propio método.

**¡OJO!** Evita las "cadenas de trenes" del tipo `pedido.getCliente().getDireccion().getCalle()`. Esto crea una dependencia frágil con toda la estructura de navegación de los objetos.

**Solución Técnica: Métodos de Delegación**
En lugar de navegar por la estructura del colaborador, solicita la información directamente al "amigo cercano". La clase `Pedido` debería tener un método `getCalleCliente()` que encapsule la navegación interna, ocultando la estructura de `Cliente` y `Direccion`.

#### Code Smells de Acoplamiento
- **Intimidad Inapropiada**: Cuando una clase usa excesivamente los detalles internos de otra clase.
- **Envidia de Características**: Un método que parece más interesado en los datos de una clase diferente a la que pertenece.
- **Intermediario**: Una clase que simplemente delega a otra.
- **Cadena de Mensajes**: Series de llamadas largas e interconectadas.

---

## ¿Qué estrategias nos permiten liberar a los módulos de sus ataduras?
Reducir el acoplamiento requiere un cambio de mentalidad: pasar de la dependencia de lo concreto a la dependencia de lo abstracto.

### ¿Cómo construimos interfaces que fomenten la independencia técnica?
- **Programación contra Interfaces**: No dependas de una implementación específica (ej. `MySQLDatabase`), sino de una abstracción (ej. interfaz `Database`). Esto permite cambiar el motor sin tocar la lógica de negocio.
- **Inyección de Dependencias**: No crees tus propias dependencias mediante `new`; deja que un tercero (un contenedor o el llamador) te las proporcione desde fuera.
- **Tell, Don't Ask**: En lugar de pedir datos a un objeto para tomar una decisión externa, delega la acción directamente al objeto que posee la información.

**La regla de oro:** Menos conocimiento mutuo equivale a más libertad para evolucionar el sistema de forma independiente y segura.

---

## Referencias
1. **Mmasias**. *idsw2: Acoplamiento*. [GitHub Repository](https://github.com/mmasias/idsw2) y en copia local: [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/02-diseñoModular/acoplamiento.md|Teoría de Acoplamiento]].
://github.com/mmasias/idsw2) y en copia local: [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/02-diseñoModular/acoplamiento.md|Teoría de Acoplamiento]].
