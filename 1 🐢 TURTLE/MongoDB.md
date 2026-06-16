---
materia: Bases de Datos 2
---

# MongoDB: Guía Maestra de Ejecución

Manual de "Fricción Cero" diseñado para dominar la sintaxis técnica y evitar los errores más comunes en papel.

---

## ¿Cómo localizamos información con precisión? (`find`)

El comando `find` es la herramienta de lectura base. Se descompone en dos bloques de llaves obligatorios.

```javascript
// EL ESQUELETO: db.coleccion.find( {filtros}, {proyección} )
//   ├─ filtros:    Criterios de búsqueda (WHERE en SQL).
//   └─ proyección: Qué campos mostrar (1) u ocultar (0).


```

### ¿Cómo usamos los operadores de comparación?
Para filtrar por rangos, el operador debe ir **dentro** del valor del campo:
- `{ edad: { $gt: 25 } }` — Mayores de 25.
- `{ edad: { $lte: 18 } }` — Menores o iguales a 18.
- `{ ciudad: { $in: ["Madrid", "BCN"] } }` — Que estén en esa lista.

---

## ¿Cómo modificamos documentos sin destruirlos? (`updateOne`)

Actualizar requiere precisión para no sobrescribir el documento completo.

```javascript
// EL ESQUELETO: db.coleccion.updateOne( {filtro}, { $operador: { cambios } } )
```

### ¿Cuáles son los operadores de mutación vitales?
- **`$set`**: Cambia o añade un valor. `{ $set: { estado: "activo" } }`.
- **`$inc`**: Suma o resta valores numéricos. `{ $inc: { puntos: 5 } }`.
- **`$push`**: Añade un elemento a un array. `{ $push: { etiquetas: "nuevo" } }`.

---

## ¿Cómo procesamos datos en masa? (`aggregate`)

El `aggregate` es una cinta transportadora. El error más común es olvidar que **siempre va dentro de un array `[ ]`**.

```javascript
// EL ESQUELETO: db.coleccion.aggregate([ {etapa1}, {etapa2} ])
//   ├─ [ ]: Indica que es una lista de pasos secuenciales.
//   └─ { $: }: Cada paso debe empezar por un operador de etapa ($match, $group...).
```

### La regla de oro del `$group`
Es la etapa más compleja. Requiere un `_id` obligatorio para definir la "agrupación".
```javascript
{ 
  $group: { 
    _id: "$campo_agrupador", 
    resultado: { $operador: "$campo_a_calcular" } 
  } 
}
```
### Casos de Uso Comunes del Pipeline

#### 1. Filtrar, Agrupar y Sumar
Calcula cuánto se ha vendido en total solo en la categoría "Tecnologia".
```javascript
db.ventas.aggregate([
  { $match: { categoria: "Tecnologia" } }, // 1. Filtramos
  { $group: { _id: "$categoria", total: { $sum: "$monto" } } } // 2. Sumamos
])
```

#### 2. Agrupar, Ordenar y Limitar
Encuentra las 3 categorías que más ingresos han generado.
```javascript
db.ventas.aggregate([
  { $group: { _id: "$categoria", total: { $sum: "$monto" } } },
  { $sort: { total: -1 } }, // -1 para orden Descendente (mayor a menor)
  { $limit: 3 }             // Nos quedamos con el Top 3
])
```

#### 3. El uso del `$project` (Limpieza visual)
Calcula el promedio y cambia el nombre del campo de salida.
```javascript
db.ventas.aggregate([
  { $group: { _id: "$categoria", media: { $avg: "$monto" } } },
  { 
    $project: { 
      _id: 0,                 // Ocultamos el ID original
      nombre_cat: "$_id",     // Renombramos el _id a nombre_cat
      promedio_ventas: "$media" 
    } 
  }
])
```

---

## ¿Cómo analizamos el rendimiento? (`explain`)

Indispensable para saber si la consulta es eficiente.
```javascript
db.coleccion.find({ ... }).explain("executionStats")
```
- **`COLLSCAN`**: Error de diseño. Escanea toda la colección (lento).
- **`IXSCAN`**: Éxito. Está usando un índice (rápido).

---

## Referencias
1. [[Cypher]] — Guía de Grafos.
2. [[Simulacro_Examen_BD2]] — Práctica real.
3. [[Bases de datos 2]] — Índice de asignatura.
