---
materia: Ingeniería de Software
revisado: true
---
# Modelo del Dominio (MdD)

El **Modelo del Dominio** es la representación de las clases conceptuales más importantes del mundo real en el contexto de nuestra solución. Es el mapa que nos permite entender la realidad antes de intentar codificarla.

---

## ¿Por qué necesitamos entender la realidad antes que el código?
Las soluciones de software no existen en el vacío; se aplican sobre una realidad con procesos y reglas propias. Intentar programar sin entender estas reglas es una receta para el desastre técnico.

### ¿Qué beneficios aporta crear un mapa conceptual del negocio?
El MdD actúa como un puente entre dos mundos que a menudo hablan idiomas distintos:
- Genera un **vocabulario común** entre desarrolladores, clientes y expertos del dominio.
- Permite comprender la estructura y dinámica de la organización sin el ruido de la tecnología.
- Identifica los requisitos de información fundamentales —lo que el sistema debe recordar— antes de considerar cualquier restricción informática.

### ¿Cómo evitar confundir el negocio con la implementación?
¡OJO! Es vital no contaminar el dominio con conceptos técnicos. El MdD debe ser puro:
- **No es un diseño de Base de Datos**: No pienses en tablas ni claves foráneas.
- **No son clases de software**: No pienses en métodos, tipos de datos específicos (ej. `ArrayList`) o patrones de diseño.
- **Es independiente del entorno**: No importa si vas a usar SQL, NoSQL o Grafos; el dominio permanece inalterado.

### El Lenguaje Ubicuo y la No-Contaminación
El objetivo principal del Modelo del Dominio no es diagramar, sino **"Hablar como el cliente"** (Lenguaje Ubicuo). El equipo técnico debe adoptar la terminología exacta del negocio (economía, logística, etc.) en el código (clases, métodos, variables). 

Se debe evitar estrictamente la **contaminación técnica** en esta capa; no deben existir conceptos de bases de datos, UI o frameworks mezclados con la lógica pura de negocio. 

**La regla de oro:** Modelas para entender el negocio, no para diseñar el código.

---

## ¿Cómo se construye un modelo de dominio efectivo?
El proceso de construcción es iterativo y se basa en la extracción de conceptos a partir de la narrativa del negocio.

### ¿Qué metodología seguimos para destilar la esencia del dominio?

```mermaid
graph TD
    1[Listar Clases Conceptuales] --> 2[Representar Modelo Inicial]
    2 --> 3[Añadir Asociaciones]
    3 --> 4[Añadir Atributos]
    4 --> 5[Iterar y Refinar]
```

1.  **Hallar Clases Conceptuales**: Identifica ideas, cosas u objetos —Sustantivos—. 
    - *Técnica:* Analiza descripciones textuales y busca objetos físicos, transacciones (ej. Venta), roles (ej. Cliente) o lugares.
2.  **Identificar Asociaciones**: Conexiones con significado entre objetos. 
    - *Tip:* Usa el sentido común. Ni tantas que saturen el diagrama, ni tan pocas que se pierda información vital.
3.  **Identificar Atributos**: Propiedades relevantes que deben recordarse (ej. nombre, fecha, precio). 
    - *¡OJO!* Si tienes dudas de si algo es un atributo o una clase, inclínalo hacia **clase conceptual**.

### ¿Cómo se visualizan estas relaciones en la práctica?

```mermaid
classDiagram
    Tienda "1" -- "*" Registro : tiene
    Registro "1" -- "*" Venta : captura
    Venta "1" -- "*" LineaVenta : contiene
    LineaVenta "*" -- "1" Articulo : describe
    Venta "*" -- "1" Pago : se_abona_con
    
    class Tienda {
        nombre
        direccion
    }
    class Venta {
        fecha
        hora
    }
    class LineaVenta {
        cantidad
    }
    class Articulo {
        precio
        descripcion
        itemid
    }
```

### ¿Qué recursos visuales complementan la vista estática?
Aunque el diagrama de clases conceptuales es el corazón del MdD, a veces necesitamos capturar el comportamiento y el cambio:
- **Diagramas de Actividad**: Visualizan procesos de negocio o flujos de trabajo (el "diagrama de flujo" del dominio).
- **Diagramas de Estado**: Capturan los diferentes estados por los que pasa una entidad (ej. Pedido: Pendiente -> Pagado -> Enviado) y los eventos que disparan esas transiciones. Son el "vídeo" que complementa la "foto" estática de las clases.

```mermaid
stateDiagram-v2
    [*] --> Pendiente
    Pendiente --> Pagado : Pago recibido
    Pagado --> Enviado : Preparar envío
    Enviado --> Entregado : Confirmar recepción
    Enviado --> Devuelto : Rechazo cliente
    Devuelto --> [*]
    Entregado --> [*]
```

### ¿Qué errores suelen descarrilar el modelado?
- **Confundir con BD**: Crear una clase "VentaID" en lugar de relacionar directamente "Venta" con sus líneas.
- **Sobre-modelar**: Intentar capturar cada detalle minúsculo antes de entender los procesos básicos —la parálisis por análisis—.
- **Falta de Validación**: No contrastar el modelo con los expertos. Si el cliente no entiende tu MdD, tu modelo no refleja la realidad.

---

## Referencias
1. [[Ingeniería de Software]]
2. [[Disciplina de Requisitos]]
3. **Mmasias**. *idsw1: Temario de la asignatura de Ingeniería de Software*. [GitHub](https://github.com/mmasias/idsw1) / [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw1/README.md|Copia Local]].
