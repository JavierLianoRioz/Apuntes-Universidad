---
materia: Sistemas Operativos
---
# write

`write()` escribe datos en un descriptor de fichero.

## Ejemplo de Uso
```c
#include <unistd.h>
#include <string.h>

int main() {
    char *mensaje = "Escribiendo en stdout...\n";
    
    // Escribimos en stdout (descriptor 1)
    write(1, mensaje, strlen(mensaje));
    
    return 0;
}
```

La regla de oro: Al igual que `read`, comprueba el retorno para asegurar que el buffer se envió completamente.
