---
materia: Sistemas Operativos
---
# Proceso Zombie

Un **Proceso Zombie** es un proceso que ha finalizado su ejecución (ha llamado a `exit`), pero todavía tiene una entrada en la tabla de procesos del Sistema Operativo.

## Causa
Ocurre cuando el proceso padre no ha ejecutado la llamada al sistema [[wait]] para recoger el código de salida del hijo.

## Consecuencia
Aunque no consume memoria ni CPU, ocupa una ranura en la tabla de procesos. Si hay demasiados, el sistema no podrá crear nuevos procesos.

La regla de oro: Un zombie se elimina automáticamente cuando el padre muere (es adoptado por `init`) o cuando el padre llama a `wait()`.
