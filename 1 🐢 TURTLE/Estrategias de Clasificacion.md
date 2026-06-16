---
materia: Ingeniería de Software
revisado: true
---
# Estrategias de Clasificación

Identificar las clases y objetos adecuados es la tarea más difícil del diseño orientado a objetos. Para ello, nos apoyamos en diversas estrategias que permiten extraer el modelo de negocio a partir de la realidad.

---

## ¿Cómo identificamos los elementos básicos del sistema?
No existe una fórmula única, pero sí métodos estructurados para evitar la arbitrariedad en el diseño.

### 1. Descripción Informal (Método de Abbott)
Propone analizar la descripción textual del problema:
- **Sustantivos**: Candidatos a ser **Clases** u **Objetos**.
- **Verbos**: Candidatos a ser **Operaciones** (Métodos).
- *Limitación:* El lenguaje natural es impreciso y no escala bien para problemas complejos.

### 2. Análisis Clásico
Se basa en buscar objetos en fuentes predefinidas del dominio:
- **Cosas Tangibles**: Libros, coches, sensores.
- **Conceptos/Ideas**: Préstamo, Venta, Reserva.
- **Roles**: Cliente, Bibliotecario, Administrador.
- **Organizaciones**: Departamento, Empresa.
- **Lugares**: Almacén, Oficina.
- **Eventos**: Devolución, Vencimiento, Pago.

### 3. Análisis del Comportamiento (Responsabilidades)
Se centra en lo que el objeto **hace** más que en lo que **es**. Se divide en:
- **Responsabilidad de Conocer**: Datos que el objeto encapsula o puede calcular.
- **Responsabilidad de Hacer**: Acciones que inicia o coordina (Patrón Experto en Información).

---

## ¿Qué trampas debemos evitar al clasificar?
El error más común es trasladar la mentalidad procedural al mundo de objetos.

### El Antipatrón: Descomposición Funcional
Ocurre cuando convertimos cada "paso" de un proceso en una clase separada.
- **Síntoma:** Clases con nombres de verbos (ej. `CalcularPrecio`, `ValidarDatos`) y un solo método `ejecutar()`.
- **Consecuencia:** Código rígido, difícil de reutilizar y con un acoplamiento artificial.

**La regla de oro:** Una clase debe representar una **entidad** con identidad y responsabilidades, no simplemente una función disfrazada.

---

## Referencias
1. **Mmasias**. *idsw2: Estrategias de clasificación*. [[8 📚 BIBLIOTECA/2 🌐 REPOSITORIOS/idsw2/temario/01-diseño/01-estrategiasClasificacion.md|Temario Clasificación]].
