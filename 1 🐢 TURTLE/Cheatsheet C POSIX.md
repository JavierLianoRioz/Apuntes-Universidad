---
id: Cheatsheet-C-POSIX
aliases:
  - API POSIX
  - System Calls C
tags:
  - sistemas-operativos
  - c
  - posix
  - cheatsheet
---
# Cheatsheet C POSIX

Referencia rápida de las llamadas al sistema ([[System Calls]]) y funciones de la biblioteca estándar de C orientadas a la [[Programación de Sistemas (UNIX)]].

## [[Gestión de Procesos]]

- **[[fork]]**: Crea un proceso hijo duplicando exactamente el proceso llamante.
  ```c
  pid_t pid = fork(); // Retorna 0 al proceso hijo, el PID del hijo al padre, y -1 en caso de error
  
  if (pid < 0) { 
      perror("Error en fork"); 
  } else if (pid == 0) { 
      /* HIJO */ 
  } else { 
      /* PADRE */ 
  }
  ```
- **[[exec]] (Familia)**: Sustituye la imagen del proceso actual (memoria, código, datos) por un nuevo programa, conservando el PID original.
  ```c
  const char *ruta_programa = "/bin/ls"; // Ruta absoluta al binario ejecutable
  const char *arg0 = "ls";               // Por convención, el primer argumento es el nombre del programa
  const char *arg1 = "-l";               // Argumentos adicionales que recibe el programa objetivo
  
  execl(ruta_programa, arg0, arg1, NULL); // NULL es obligatorio para indicar el final de la lista de argumentos
  perror("Error en execl");
  ```
- **[[wait]]**: Bloquea al proceso padre hasta que uno de sus procesos hijos termine, previniendo la formación de [[Procesos Zombie]].
  ```c
  int estado_hijo; // Almacenará el código de salida y estado del hijo (ej. si fue matado por una señal)
  
  wait(&estado_hijo); // Espera a que CUALQUIER proceso hijo termine
  ```
- **[[waitpid]]**: Versión avanzada de `wait()` que permite esperar por un hijo específico o usar opciones (ej. ejecución no bloqueante).
  ```c
  pid_t pid_objetivo = target_pid; // PID específico a esperar (o -1 para cualquier hijo)
  int estado_hijo;                 // Almacenará el estado de finalización
  int opciones = WNOHANG;          // WNOHANG indica ejecución no bloqueante (retorna 0 si el hijo sigue ejecutándose)
  
  pid_t pid_resultado = waitpid(pid_objetivo, &estado_hijo, opciones);
  ```

## [[Programación con Hilos (Pthreads)]]

- **[[pthread_create]]**: Inicia un nuevo hilo de ejecución que comparte el espacio de memoria dentro del proceso actual.
  ```c
  void* funcion_hilo(void* argumento) { 
      return NULL; 
  }
  
  pthread_t identificador_hilo;          // Almacenará el ID único asignado al hilo recién creado
  pthread_attr_t *atributos_hilo = NULL; // NULL para usar los atributos por defecto (joinable, tamaño de pila, etc.)
  void *argumento_hilo = NULL;           // Puntero a datos que recibirá la función del hilo (NULL si no recibe nada)
  
  pthread_create(&identificador_hilo, atributos_hilo, funcion_hilo, argumento_hilo);
  ```
- **[[pthread_join]]**: Espera a que un hilo termine su ejecución para poder liberar sus recursos en memoria.
  ```c
  pthread_t identificador_hilo = id_hilo; // ID del hilo que se desea esperar (debe ser un hilo "joinable")
  void **valor_retorno = NULL;            // Puntero para capturar lo que devuelva la función del hilo (NULL para ignorarlo)
  
  pthread_join(identificador_hilo, valor_retorno);
  ```

## [[Gestión de Señales]]

- **[[signal]]**: Interfaz clásica de UNIX para capturar señales y asignarles una función de manejo personalizada.
  ```c
  void manejador_senial(int sig) {
      /* lógica de manejo */
  }
  
  int numero_senial = SIGINT;                         // Señal objetivo (ej. SIGINT generada por Ctrl+C en consola)
  void (*funcion_manejadora)(int) = manejador_senial; // Puntero a la función de callback a ejecutar
  
  signal(numero_senial, funcion_manejadora);
  ```

## Memoria Compartida

- **[[mmap]]**: Proyecta archivos/dispositivos en memoria. Permite crear un mapeo de memoria compartida anónima sin estar respaldada por un fichero en disco.
  ```c
  void *direccion_base = NULL;               // NULL permite al SO elegir automáticamente una dirección de memoria virtual libre
  size_t tamano = sizeof(int);               // Tamaño en bytes del área de memoria a reservar
  int proteccion = PROT_READ | PROT_WRITE;   // Permisos en memoria: permite lectura y escritura simultánea
  int banderas = MAP_SHARED | MAP_ANONYMOUS; // MAP_SHARED: visible entre procesos. MAP_ANONYMOUS: mapeo en memoria RAM, sin archivo asociado
  int descriptor_fichero = -1;               // -1 porque al ser MAP_ANONYMOUS, no depende de ningún archivo abierto
  off_t desplazamiento = 0;                  // 0, ya que no hay archivo desde donde realizar un desplazamiento inicial
  
  int *memoria_compartida = (int *)mmap(direccion_base, tamano, proteccion, banderas, descriptor_fichero, desplazamiento);
  ```