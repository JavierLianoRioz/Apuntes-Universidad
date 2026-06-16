---
materia: Sistemas Operativos
categoria: universidad
---
# Entorno de Desarrollo UNIX

El **Entorno de Desarrollo UNIX** se basa en un ecosistema de herramientas modulares altamente interconectadas que siguen la filosofía de que "cada herramienta hace una sola cosa y la hace bien".

---

## ¿Cómo se compila y ejecuta código en UNIX?

En sistemas UNIX, el compilador estándar de facto es **GCC** (GNU Compiler Collection). El proceso de transformación de código fuente a ejecutable pasa por cuatro fases:

1.  **Preprocesamiento:** Expande macros e incluye cabeceras (ej: `#include`).
2.  **Compilación:** Traduce el código C a código ensamblador.
3.  **Ensamblado:** Convierte el código ensamblador a código objeto (binario máquina parcial, archivos `.o`).
4.  **Enlazado (Linker):** Une los archivos objeto con las funciones de la [[LibC]] u otras bibliotecas para generar el ejecutable binario final.

Para automatizar este proceso en proyectos medianos o grandes, se utiliza la herramienta **make** mediante un archivo de configuración llamado `Makefile`.

```javascript
// EL ESQUELETO: gcc -Wall -g origen.c -o ejecutable
//   ├─ -Wall: Habilita todos los avisos de advertencia del compilador (warnings).
//   ├─ -g: Añade información de depuración para gdb.
//   └─ -o: Especifica el nombre del archivo de salida.
```

---

## ¿Cómo gestionamos los permisos de archivos y ejecución?

UNIX es un sistema multiusuario desde su origen. Por ello, cada archivo y directorio tiene un propietario y un grupo asignados, con tres tipos de permisos:
- **r (Read):** Lectura del archivo o listado del directorio.
- **w (Write):** Modificación del archivo o creación/borrado dentro del directorio.
- **x (Execute):** Ejecución del archivo como programa o acceso para entrar a un directorio.

Para modificar estos permisos se utiliza el comando [[chmod]], aplicando la notación octal o simbólica.

**¡OJO!** Un error típico al compilar un programa es intentar ejecutarlo directamente mediante su nombre (ej: `mi_programa`) y recibir un error de comando no encontrado. En UNIX, por seguridad, el directorio actual (`.`) no está en la variable de entorno `PATH`, por lo que se debe ejecutar anteponiendo la ruta relativa: `./mi_programa`.

---

## ¿Qué papel juegan las variables de entorno?

Las variables de entorno son pares clave-valor que definen el comportamiento del shell y de los programas en ejecución:

- **`PATH`:** Lista de directorios donde el shell busca los ejecutables de los comandos que introduces.
- **`LD_LIBRARY_PATH`:** Directorios donde el cargador dinámico busca bibliotecas compartidas (`.so`) antes de ejecutar un binario.

La regla de oro: Cualquier herramienta del entorno de desarrollo de UNIX se puede integrar con otras redirigiendo sus canales estándar (`stdin`, `stdout`, `stderr`) mediante tuberías (*pipes*).
