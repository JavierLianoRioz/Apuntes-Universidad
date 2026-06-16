---
materia: Sistemas Operativos
categoria: universidad
---
# Procesos Huérfanos

Un **Proceso Huérfano** es un proceso que sigue en ejecución pero cuyo proceso padre ha finalizado (ha muerto).

---

## Causa

Ocurre cuando un proceso padre termina su ciclo de vida antes que sus procesos hijos creados mediante la llamada al sistema [[fork]].

---

## Consecuencia y Adopción

A diferencia de los [[Procesos Zombie|zombies]], los procesos huérfanos no se quedan bloqueados sin limpiar. El kernel del Sistema Operativo detecta la muerte del padre y **reasigna el hijo huérfano** a un proceso tutor:

1.  **Adopción por `init`:** Tradicionalmente, el proceso `init` (PID 1) adopta a todos los huérfanos.
2.  **Limpieza Automática:** El proceso `init` ejecuta de forma constante la llamada [[wait]] sobre sus hijos adoptivos, garantizando que cuando el proceso huérfano termine, sus recursos y su entrada en la tabla de procesos se liberen inmediatamente.

---

## Caso de Uso: Daemons

La regla de oro: La creación intencional de procesos huérfanos es una técnica estándar para la creación de **Daemons** (servicios que corren en segundo plano). 

Para independizar un proceso de la terminal que lo lanzó, se realiza un doble `fork` y se deja morir al proceso padre intermedio, forzando a que el proceso de ejecución real sea adoptado por `init` y pierda su terminal de control asociada.
