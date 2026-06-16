---
materia: Sistemas Operativos
---
# Gestión de Señales

Las **Señales** son interrupciones de software enviadas a un proceso para notificarle de un evento asíncrono. Pueden ser enviadas por el kernel (ej. fallo de segmentación), por el hardware o por otros procesos.

## ¿Cómo reaccionamos a un evento externo?

Un proceso puede decidir ignorar una señal, dejar que se ejecute la acción por defecto o capturarla mediante un **Manejador de Señales** (*Signal Handler*).

- **[[sigaction]]**: La forma moderna y robusta de instalar manejadores. Permite un control preciso sobre qué señales bloquear durante la ejecución del manejador.
- **[[signal]]**: Interfaz clásica más sencilla pero con comportamientos menos predecibles entre diferentes sistemas UNIX.

### Señales comunes que debes conocer

- **SIGINT**: Enviada desde el teclado (Ctrl+C). Termina el proceso.
- **SIGKILL**: Fuerza la terminación inmediata. No puede ser capturada ni ignorada.
- **SIGUSR1 / SIGUSR2**: Reservadas para uso personalizado por el programador.
- **SIGCHLD**: Enviada al padre cuando un hijo cambia de estado (termina o se detiene).

La regla de oro: Dentro de un manejador de señales, solo debes llamar a funciones "async-signal-safe" para evitar deadlocks y corrupción de datos.