---
materia: Sistemas Operativos
---
# System Calls

Las **System Calls** (Llamadas al Sistema) son la interfaz fundamental entre el software de usuario y el núcleo (kernel) del Sistema Operativo.

## Funcionamiento
1. El proceso solicita un servicio (ej. leer un fichero).
2. Se produce una excepción de software (trap) que cambia la CPU de "Modo Usuario" a "Modo Kernel".
3. El kernel ejecuta la tarea privilegiada y devuelve el control.

## Ejemplos Críticos
- Gestión de Procesos: [[fork]], [[exec]], [[wait]].
- Entrada/Salida: [[read]], [[write]], [[close]].

La regla de oro: Las System Calls son "caras" en términos de rendimiento; minimiza su número usando buffers cuando sea posible.
