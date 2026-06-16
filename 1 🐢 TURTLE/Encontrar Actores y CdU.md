---
revisado: true
materia: Ingeniería de Software
---
# Encontrar Actores y CdU

Esta actividad es el punto de partida ineludible para delimitar el sistema. Consiste en identificar con precisión quiénes interactúan con el software y qué objetivos pretenden alcanzar mediante esa interacción.

---

## ¿Cómo definimos las fronteras de nuestro sistema?
Para no perdernos en un desarrollo infinito, debemos establecer qué queda dentro y qué queda fuera de nuestra responsabilidad técnica.

### ¿Quiénes son los protagonistas externos de la interacción?
Un **Actor** representa un **rol** que una entidad externa desempeña al interactuar con el sistema. 
- **¡OJO!** El actor no es una persona específica —como "Pepe"—, sino el rol que desempeña —como "Administrador" o "Cliente"—.
- Pueden ser otros sistemas, dispositivos de hardware o incluso el **Tiempo** (especialmente para tareas automáticas como la generación de backups nocturnos).

### ¿Qué objetivos persiguen los actores al interactuar con el software?
==Un **Caso de Uso** es la especificación de una secuencia de acciones que dan un **resultado observable de interés** para un actor.== No es una función interna, sino una meta cumplida.

### ¿Por qué es vital delimitar el alcance desde el primer momento?
- **Delimitar el sistema**: Define los límites de la responsabilidad del equipo de desarrollo.
- **Comunicación**: Crea un catálogo de funcionalidades entendible por el cliente sin necesidad de tecnicismos.
- **Base para estimación**: Permite visualizar la magnitud real del proyecto y los recursos necesarios.

---

## ¿Cómo descubrimos los elementos del modelo en la realidad?
El descubrimiento no es un proceso mecánico, sino una investigación sobre las necesidades del negocio.

### ¿Qué preguntas nos ayudan a desvelar los roles externos?
Para hallar los **Actores**, debemos observar el entorno del sistema y preguntarnos:
- ¿Quién o qué usa el sistema para realizar su trabajo diario?
- ¿Quién obtiene información del sistema y quién es el encargado de proveerla?
- ¿Qué otros sistemas externos necesitan intercambiar datos con nuestra solución?

### ¿De qué manera identificamos las metas de valor para cada actor?
Para cada actor identificado, buscamos sus metas fundamentales:
- ¿Qué necesita realizar el actor con los objetos de negocio? (Crear, modificar, eliminar o listar información).
- ¿Qué eventos externos significativos deben ser notificados al sistema por este actor?

### ¿Cómo visualizamos el mapa completo de funcionalidades?
El resultado de esta investigación es el **Modelo de Casos de Uso**, un diagrama que muestra las relaciones de participación y un **Glosario** que unifica los términos para evitar ambigüedades.

```mermaid
flowchart LR
    subgraph Sistema ["Sistema de Ventas"]
        UC1([Gestionar Inventario])
        UC2([Realizar Compra])
        UC3([Consultar Historial])
    end

    Admin[Administrador] --- UC1
    User[Cliente] --- UC2
    User --- UC3
```

> [!TIP] Nombramiento
> La regla de oro: el nombre de un caso de uso siempre debe empezar por un **verbo** (ej. "Realizar Compra", "Validar Usuario"). Esto enfatiza la acción y el objetivo final.

---

## Referencias
1. [[1 🐢 TURTLE/Casos de Uso]]
2. **Mmasias**. *idsw1: Temario de la asignatura de Ingeniería de Software*. [GitHub](https://github.com/mmasias/idsw1) / [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw1/README.md|Copia Local]].
