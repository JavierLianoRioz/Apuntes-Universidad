---
materia: Sistemas Operativos
---
# Entrada-Salida de Bajo Nivel

En UNIX, la entrada y salida se gestiona mediante la abstracción de los **Descriptores de Fichero** (File Descriptors). A diferencia de los flujos de alto nivel (`FILE*` en C), los descriptores son simples enteros que indexan una tabla abierta por el kernel para cada proceso.

## ¿Cuáles son los descriptores estándar?

Todo proceso nace con tres descriptores abiertos por defecto:

- **0 (stdin)**: Entrada estándar (teclado).
- **1 (stdout)**: Salida estándar (pantalla).
- **2 (stderr)**: Error estándar (pantalla, para mensajes de diagnóstico).

## ¿Cómo operamos con ellos?

Utilizamos llamadas directas al sistema que no usan buffering intermedio en el espacio de usuario:

- **[[read]]**: Lee bytes desde un descriptor.
- **[[write]]**: Escribe bytes en un descriptor.
- **[[close]]**: Libera el descriptor.

¡OJO! Al usar `read()` y `write()`, es vital manejar el valor de retorno (`ssize_t`) para detectar errores o lecturas parciales. Nunca asumas que se han leído o escrito todos los bytes solicitados de una sola vez.

La regla de oro: Usa `sizeof()` para determinar el tamaño de las estructuras al leer o escribir, asegurando la portabilidad y evitando desbordamientos de buffer.