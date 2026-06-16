---
materia: Sistemas Operativos
---
# waitpid

`waitpid()` es una versión más versátil de `wait()` que permite esperar a un hijo específico o usar opciones no bloqueantes.

## Sintaxis
```c
pid_t pid = waitpid(target_pid, &status, options);
```

La regla de oro: Usa `WNOHANG` en las opciones si quieres consultar el estado del hijo sin detener la ejecución del padre.
