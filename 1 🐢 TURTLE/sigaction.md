---
materia: Sistemas Operativos
---
# sigaction

`sigaction()` es la llamada al sistema recomendada para capturar y gestionar señales de forma robusta.

## Ejemplo de Uso
```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void mi_manejador(int sig) {
    printf("He recibido la señal %d\n", sig);
}

int main() {
    struct sigaction sa;
    sa.sa_handler = mi_manejador;
    sigemptyset(&sa.sa_mask);
    sa.sa_flags = 0;

    sigaction(SIGINT, &sa, NULL); // Captura Ctrl+C

    while(1) {
        printf("Esperando señal... (Ctrl+C para capturar)\n");
        sleep(2);
    }
    return 0;
}
```

La regla de oro: Evita usar `signal()`; `sigaction()` es el estándar profesional por su seguridad y control.
