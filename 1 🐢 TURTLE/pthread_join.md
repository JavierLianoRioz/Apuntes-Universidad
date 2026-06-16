---
materia: Sistemas Operativos
---
# pthread_join

`pthread_join()` espera a que un hilo termine. Es el equivalente a `wait()` para procesos.

La regla de oro: Si no haces `join` de un hilo (o lo marcas como *detached*), sus recursos no se liberarán al terminar.
