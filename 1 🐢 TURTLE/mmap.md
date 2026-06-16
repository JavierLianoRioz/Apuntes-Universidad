---
materia: Sistemas Operativos
---
# mmap

`mmap()` es una llamada al sistema que proyecta archivos o dispositivos en la memoria.

## Ejemplo de Uso (Memoria Compartida)
```c
#include <sys/mman.h>
#include <stdio.h>
#include <unistd.h>
#include <string.h>

int main() {
    // Creamos memoria compartida anónima
    int *compartido = mmap(NULL, sizeof(int), PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);
    *compartido = 100;

    if (fork() == 0) {
        *compartido = 200; // El hijo modifica
        return 0;
    } else {
        sleep(1);
        printf("Valor compartido: %d\n", *compartido); // El padre ve 200
    }
    return 0;
}
```

## Ventajas
- Evita copias innecesarias entre espacio de usuario y kernel.
- Permite acceso aleatorio a ficheros como si fueran arrays en memoria.

La regla de oro: Al usar `mmap` para memoria compartida entre procesos, la sincronización debe gestionarse mediante otras herramientas de control de concurrencia si varios procesos escriben simultáneamente.
