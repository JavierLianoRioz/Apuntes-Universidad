---
materia: Sistemas Operativos
---
# signal

`signal()` es la interfaz clásica de UNIX para capturar señales.

## Limitaciones
- Comportamiento no portable (en algunos sistemas el manejador se desinstala tras el primer uso).
- Menor control que [[sigaction]].

La regla de oro: Úsala solo para ejemplos educativos simples; en producción usa siempre `sigaction`.
