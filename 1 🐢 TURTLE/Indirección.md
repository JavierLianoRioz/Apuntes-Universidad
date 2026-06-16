---
materia: Ingeniería de Software
---
# Indirección

La **Indirección** es la estrategia arquitectónica fundamental para reducir el [[Acoplamiento]] delegando la responsabilidad de comunicación, instanciación o control a un componente intermediario (una *Invención Pura* que no existe en el [[Modelo del Dominio]]).

> **Regla de oro de Wheeler:** *"Cualquier problema en ciencias de la computación puede resolverse añadiendo un nivel de indirección... excepto el problema de tener demasiadas indirecciones."*

## Tipología de Intermediarios (Invenciones Puras)

Para proteger el [[Diseño Modular]] de dependencias cruzadas, se fabrican intermediarios especializados que actúan como "puentes" de comunicación:

### 1. Vista Separada (MVC / MVP / MVVM)
Desacopla la lógica de presentación (UI) del modelo subyacente. El modelo muta y notifica cambios sin conocer quién ni cómo lo renderiza, permitiendo cambiar la interfaz sin tocar la lógica de negocio.

### 2. Controlador
Actúa como coordinador entre eventos externos (inputs de usuario o mensajes de red) y las operaciones del dominio. Su misión es evitar que la interfaz y el dominio se conozcan directamente, centralizando la lógica de navegación y flujo.

### 3. Creador (Factory / Builder)
Encapsula la complejidad de instanciación de un objeto. El cliente solicita una instancia a través de un intermediario (el Creador) sin conocer sus dependencias internas ni su proceso de construcción, cumpliendo con la inversión de dependencias.

---
## Referencias
1. **Mmasias**. *idsw2: Temario de Ingeniería de Software*.
