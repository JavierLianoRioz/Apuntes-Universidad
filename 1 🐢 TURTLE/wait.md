---
materia: Sistemas Operativos
---
# wait

La llamada `wait()` bloquea al proceso padre hasta que uno de sus hijos termine.

## Propósito
- **Sincronización:** Esperar a que el trabajo del hijo finalice.
- **Limpieza:** Permite al kernel eliminar la entrada del hijo de la tabla de procesos, evitando [[Procesos Zombie]].

## Ejemplo de Uso
```c
#include <sys/wait.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    if (fork() == 0) {
        printf("Hijo trabajando...\n");
        sleep(2);
        return 0;
    } else {
        printf("Padre esperando al hijo...\n");
        wait(NULL); // Bloquea hasta que el hijo termine
        printf("Hijo finalizado. El padre continúa.\n");
    }
    return 0;
}
```

La regla de oro: El padre tiene la responsabilidad legal de llamar a `wait()` por cada hijo que cree.
