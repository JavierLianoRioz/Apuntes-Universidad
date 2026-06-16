---
materia: Sistemas Operativos
---
# close

`close()` cierra un descriptor de fichero, liberando el recurso en el kernel.

La regla de oro: Cierra siempre tus descriptores, especialmente tras un `fork()`, para evitar fugas de recursos y bloqueos en tuberías.
