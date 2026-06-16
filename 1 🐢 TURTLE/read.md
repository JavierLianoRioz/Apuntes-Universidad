---
materia: Sistemas Operativos
---
# read

`read()` es una llamada al sistema para leer datos desde un descriptor de fichero.

## Ejemplo de Uso
```c
#include <unistd.h>
#include <stdio.h>

int main() {
    char buffer[100];
    printf("Escribe algo: ");
    
    // Leemos de stdin (descriptor 0)
    ssize_t leidos = read(0, buffer, sizeof(buffer) - 1);
    
    if (leidos > 0) {
        buffer[leidos] = '\0'; // Aseguramos el fin de cadena
        printf("Has escrito: %s", buffer);
    }
    return 0;
}
```

## Valor de Retorno
- **> 0**: Número de bytes leídos.
- **0**: Fin de fichero (EOF).
- **-1**: Error.

La regla de oro: Nunca asumas que `read()` lee todos los bytes solicitados; comprueba siempre el valor de retorno.
