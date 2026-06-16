---
materia: Sistemas Operativos
---
# Programación con Hilos (Pthreads)

A diferencia de los procesos, los hilos (threads) comparten el mismo espacio de direcciones. Esto permite una comunicación extremadamente rápida pero introduce la necesidad de una sincronización rigurosa.

## ¿Cómo gestionamos el ciclo de vida de un hilo?

En UNIX, utilizamos la librería POSIX Threads (`pthread`).

1.  **[[pthread_create]]**: Crea un nuevo hilo de ejecución dentro del proceso actual.
2.  **[[pthread_join]]**: Bloquea el hilo llamante hasta que el hilo especificado termine. Es el equivalente a `wait()` para procesos.

## ¿Cómo evitamos el caos en la memoria compartida?

### El uso de Mutex

Un **Mutex** (Mutual Exclusion) actúa como un cerrojo para proteger secciones críticas de código.

- **SINTAXIS:** `pthread_mutex_lock(&m); ...sección crítica... pthread_mutex_unlock(&m);`

La regla de oro: Minimiza el tiempo que mantienes un mutex bloqueado para maximizar el paralelismo real de la aplicación.

¡OJO! Al compilar programas con hilos, debes incluir el flag `-lpthread` en el comando `gcc` para enlazar la librería correspondiente.