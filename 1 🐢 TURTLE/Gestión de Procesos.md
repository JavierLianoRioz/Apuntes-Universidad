---
materia: Sistemas Operativos
---
# Gestión de Procesos

La **Gestión de Procesos** es una de las tareas más críticas del sistema operativo. Un proceso no es solo un programa en ejecución; es una entidad dinámica que posee su propio espacio de direcciones, hilos de ejecución y recursos asignados por el kernel.

## ¿Cómo nace un proceso?

En UNIX, los procesos no se crean desde cero con un binario, sino que se clonan.

### El ciclo fork-exec

Este es el mecanismo fundamental de creación de procesos:

1.  **[[fork]]**: El proceso actual (padre) crea una copia exacta de sí mismo.
    - **SINTAXIS:** `pid_t pid = fork();`
    - **Retorno:** El padre recibe el **PID** del hijo; el hijo recibe **0**.
2.  **[[exec]]**: El hijo suele llamar a una función de la familia `exec` (como `execl` o `execvp`) para sustituir su imagen de memoria por un nuevo binario.

## ¿Cuáles son los estados críticos de la jerarquía?

La relación padre-hijo debe gestionarse con cuidado para no agotar los recursos del sistema.

- **[[Procesos Zombie]]**: Un hijo que ha terminado pero cuya entrada en la tabla de procesos sigue existiendo porque el padre no ha llamado a `wait()`.
- **[[Procesos Huérfanos]]**: Hijos cuyo padre ha muerto. Son adoptados automáticamente por el proceso `init` (PID 1).

### ¿Cómo sincronizamos la terminación?

Para evitar zombies, el padre debe usar la llamada **[[wait]]** o **[[waitpid]]**. Esto permite recoger el estado de salida del hijo y liberar su entrada en la tabla de procesos.

¡OJO! Un exceso de procesos zombie puede impedir la creación de nuevos procesos al llenar la tabla de procesos del sistema, aunque no consuman CPU ni memoria.