---
materia: Sistemas Operativos
---
# exec

La familia de funciones `exec()` sustituye la imagen del proceso actual por un nuevo programa.

## Funcionamiento
- El proceso conserva su PID, pero su memoria, código y datos son reemplazados por los del nuevo binario.
- No hay retorno si la llamada tiene éxito (ya que el código llamante deja de existir).

## Ejemplo de Uso
```c
#include <unistd.h>
#include <stdio.h>

int main() {
    printf("Voy a ejecutar el comando 'ls'...\n");
    
    // execl(path, comando, argumento, ..., NULL)
    execl("/bin/ls", "ls", "-l", NULL);
    
    // Si execl tiene éxito, esta línea NUNCA se ejecutará
    perror("Error al ejecutar exec");
    return 1;
}
```

La regla de oro: `exec()` se usa casi siempre dentro de un hijo creado con `fork()` para cargar un nuevo programa sin destruir al padre.
