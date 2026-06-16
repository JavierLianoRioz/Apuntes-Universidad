---
materia: Sistemas Operativos
categoria: universidad
---
# Sistemas Operativos

Los **Sistemas Operativos** son la capa de software fundamental que actúa como intermediaria entre el hardware de la máquina y el usuario o sus aplicaciones. Su propósito no es solo "hacer que la computadora funcione", sino gestionar los recursos limitados (CPU, Memoria, E/S) para ofrecer una abstracción coherente y segura del sistema.

## ¿Cómo pasamos de la arquitectura teórica a la realidad técnica?

La comprensión de un sistema operativo se divide entre la gestión lógica de recursos y su implementación física. Mientras que la teoría nos habla de algoritmos de planificación y modelos de memoria, la **Programación de Sistemas** es donde estos conceptos cobran vida.

En el ecosistema UNIX, esta conexión se materializa a través de la [[Programación de Sistemas (UNIX)]], donde el lenguaje C y las llamadas al sistema (*System Calls*) nos permiten manipular directamente los engranajes del software.

### ¿Qué pilares sostienen la interacción con el sistema?

Para dominar el entorno operativo, debemos navegar por varios dominios críticos:

1.  **[[Gestión de Procesos]]**: Entender cómo nace, vive y muere una unidad de ejecución.
2.  **[[Comunicación entre Procesos (IPC)]]**: Los mecanismos para que entidades aisladas colaboren.
3.  **[[Programación con Hilos (Pthreads)]]**: La división del trabajo dentro de un mismo espacio de memoria.
4.  **[[Gestión de Señales]]**: El sistema de interrupciones de software para eventos asíncronos.
5.  **[[Entrada-Salida de Bajo Nivel]]**: La verdad cruda detrás de los descriptores de fichero.
6.  **[[Entorno de Desarrollo UNIX]]**: Las herramientas de compilación y permisos que rigen la seguridad y ejecución.

La regla de oro: En UNIX, **todo es un fichero** (o se comporta como tal), y esta abstracción simplifica enormemente la interacción con dispositivos y comunicaciones.