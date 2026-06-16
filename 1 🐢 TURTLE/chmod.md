---
materia: Sistemas Operativos
---
# chmod

`chmod` cambia los permisos de acceso a ficheros y directorios.

## Modo Octal
- **7**: rwx (4+2+1)
- **5**: r-x (4+0+1)
- **4**: r-- (4+0+0)

La regla de oro: Usa `chmod 700` para scripts privados y `755` para binarios públicos.
