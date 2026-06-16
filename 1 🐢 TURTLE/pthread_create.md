---
materia: Sistemas Operativos
---
# pthread_create

`pthread_create()` inicia un nuevo hilo en el proceso actual.

## Ejemplo de Uso
```c
#include <pthread.h>
#include <stdio.h>

void* funcion_hilo(void* arg) {
    printf("Hilo ejecutándose. Argumento: %s\n", (char*)arg);
    return NULL;
}

int main() {
    pthread_t id_hilo;
    char* mensaje = "Hola desde el hilo";

    // Creamos el hilo
    pthread_create(&id_hilo, NULL, funcion_hilo, (void*)mensaje);

    // Esperamos a que termine
    pthread_join(id_hilo, NULL);
    
    printf("Hilo finalizado.\n");
    return 0;
}
```

La regla de oro: Pasa los argumentos mediante punteros y recuerda que el hilo comparte el espacio de memoria del padre.
