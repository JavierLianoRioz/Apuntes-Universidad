---
materia: Sistemas Operativos
categoria: universidad
---
# Programación de Sistemas (UNIX)

La **Programación de Sistemas** es la disciplina que se encarga de desarrollar software que proporciona servicios a otro software o que interactúa directamente con el núcleo del sistema operativo. En el contexto de UNIX, esto implica el uso intensivo del lenguaje C y la interfaz de llamadas al sistema.

## ¿Por qué UNIX es el estándar para programar sistemas?

La filosofía UNIX se basa en la simplicidad y la modularidad. Al exponer una interfaz coherente basada en descriptores de fichero y procesos, permite que el desarrollador tenga un control granular sobre el hardware sin perder la portabilidad.

### ¿Cómo interactuamos con el kernel?

La interacción se divide en dos capas que a menudo se confunden pero que tienen propósitos distintos:

1.  **[[System Calls]]**: Son la entrada directa al núcleo. Funciones como `read()`, `write()` o `fork()` detienen la ejecución del usuario y saltan al modo supervisor para que el kernel realice una tarea privilegiada.
2.  **[[LibC]]**: Es la biblioteca estándar de C. Proporciona envoltorios (*wrappers*) más amigables (como `printf()` o `malloc()`) que internamente pueden llamar a una o varias *System Calls*.

### ¿Cuáles son los dominios de ejecución?

Para construir aplicaciones robustas en UNIX, debemos dominar tres áreas de control:

- **Espacio de Procesos**: La creación y gestión de la jerarquía mediante [[Gestión de Procesos]].
- **Concurrencia**: La gestión de múltiples flujos de ejecución con [[Programación con Hilos (Pthreads)]].
- **Sincronización y Eventos**: El uso de [[Gestión de Señales]] para manejar interrupciones y eventos asíncronos.

La regla de oro: El éxito en la programación de sistemas reside en entender el flujo de datos a través de los [[Entrada-Salida de Bajo Nivel|Descriptores de Fichero]] y la gestión responsable de la memoria y los recursos del sistema.