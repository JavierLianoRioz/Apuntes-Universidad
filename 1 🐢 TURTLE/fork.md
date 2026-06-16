---
materia: Sistemas Operativos
---
# fork

La llamada al sistema `fork()` se utiliza para crear un nuevo proceso duplicando el proceso llamante. El nuevo proceso se denomina proceso hijo.

## Comportamiento
- El hijo es una copia exacta del padre (memoria, descriptores de fichero, etc.).
- Tras el `fork`, ambos procesos continúan ejecutándose desde la instrucción inmediatamente posterior a la llamada.

## Valor de Retorno
- **En el padre:** Devuelve el PID del hijo creado.
- **En el hijo:** Devuelve `0`.
- **Error:** Devuelve `-1`.

## Ejemplo de Uso
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("Error en fork");
    } else if (pid == 0) {
        printf("Soy el HIJO. Mi PID es %d\n", getpid());
    } else {
        printf("Soy el PADRE. He creado al hijo con PID %d\n", pid);
    }
    return 0;
}
```

La regla de oro: Siempre comprueba el valor de retorno para separar la lógica de ejecución del padre y el hijo.
