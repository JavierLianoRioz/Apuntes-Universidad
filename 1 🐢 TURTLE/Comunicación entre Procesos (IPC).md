---
materia: Sistemas Operativos
---
# Comunicación entre Procesos (IPC)

La **Comunicación entre Procesos** (Inter-Process Communication) permite que procesos independientes intercambien datos y sincronicen su ejecución. Dado que cada proceso tiene su propio espacio de memoria aislado, el kernel debe proporcionar canales seguros para esta interacción.

## ¿Cómo fluye la información de forma unidireccional?

### Pipes Anónimos

El mecanismo más clásico de UNIX. Permite conectar la salida de un proceso con la entrada de otro.

- **EL ESQUELETO:** `int fd[2]; pipe(fd);`
    - `fd[0]`: Extremo de LECTURA.
    - `fd[1]`: Extremo de ESCRITURA.

La regla de oro: Siempre cierra los descriptores no utilizados en cada proceso tras un `fork()` para evitar bloqueos infinitos al esperar el EOF.

## ¿Cómo compartimos memoria de forma masiva?

Para intercambiar grandes volúmenes de datos sin la sobrecarga de copiar información, usamos la proyección de memoria.

- **[[mmap]]**: Mapea un fichero o memoria anónima en el espacio de direcciones del proceso. Con el flag `MAP_SHARED`, los cambios son visibles para otros procesos.