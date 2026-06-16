---
materia: Bases de Datos 2
---

# 📑 CHULETA FINAL: Supervivencia BD2 (MongoDB & Neo4j)

Guía de repaso rápido para el minuto antes de entrar al examen. Estructura de máxima densidad.

---

## 🍃 MONGODB: El Reino de las Llaves `{ }`

### 1. El Esqueleto de Consulta (`find`)
```js
db.col.find( {filtros}, {proyección} )
```
- **Filtros Pro:** `{ edad: { $gt: 25 } }`, `{ "dir.ciudad": "Madrid" }`.
- **Proyección:** `{ nombre: 1, _id: 0 }`.
- **¡OJO!**: En el filtro **NO** usas `$nombre`, pero en la proyección/renombrado **SÍ** usa `"$nombre"`.

### 2. El Pipeline de Agregación (`aggregate`)
**Regla de oro:** Siempre dentro de un array `db.col.aggregate([ ... ])`.

| Etapa | Moldes y Trucos |
| :--- | :--- |
| **`$match`** | `{ $match: { estado: "activo" } }` (Igual que un find). |
| **`$group`** | `{ $group: { _id: "$categoria", total: { $sum: "$monto" } } }` |
| **`$unwind`** | `{ $unwind: "$array" }` (Desmonta arrays para operar campo a campo). |
| **`$lookup`** | `{ $lookup: { from: "col2", localField: "id", foreignField: "_id", as: "unido" } }` |
| **`$project`** | `{ $project: { _id: 0, nuevo: "$_id", dato: 1 } }` (Para limpiar la salida). |

### 3. Rendimiento e Índices
- **Crear:** `db.col.createIndex({ campo: 1, edad: -1 })`.
- **Verificar:** `.explain("executionStats")`.
- **Éxito:** Busca `IXSCAN` (Índice). **Fallo:** `COLLSCAN` (Lento).

---

## 🕸️ NEO4J: El Arte del Dibujo `( )-[ ]->( )`

### 1. El Esqueleto de Patrón
```cypher
(p:Persona {nombre: "Ana"})-[r:AMIGO_DE]->(m:Persona)
```
- **Nodos:** `(variable:Etiqueta {propiedad: "valor"})`.
- **Relaciones:** `-[variable:TIPO {propiedad: valor}]->`.

### 2. Navegación de Caminos (`Paths`)
- **Longitud:** `*1..3` (entre 1 y 3 saltos), `*2` (exactamente 2).
- **Dirección:** Si no sabes quién es el origen, usa `-( )-` (sin flecha).
- **Filtros Pro:** `WHERE ALL(r IN relationships(p) WHERE r.intensidad > 5)`.

### 3. La Barrera del `WITH` (Aduana)
- **Regla de oro:** El `WITH` borra todo lo que no menciones.
- **Uso:** `MATCH ... WITH e, count(p) AS total WHERE total > 1 RETURN e.nombre`.
- **Collect:** Si quieres que una variable sobreviva como lista: `WITH e, collect(p.nombre) AS nombres`.

---

## 🚨 ALERTAS ROJAS (No falles en esto)

1.  **Comillas:** En Mongo, las rutas anidadas `"direccion.ciudad"` **siempre** con comillas.
2.  **$ en Group:** En el `$group`, el campo agrupador **siempre** lleva `$` delante: `_id: "$campo"`.
3.  **Distinct en Cypher:** Úsalo siempre en los `count` para no contar caminos duplicados: `count(DISTINCT p)`.
4.  **`$set` en Update:** Si olvidas el `$set`, **borrarás** el resto del documento.
5.  **id(a) < id(b):** Úsalo en Cypher para evitar que te salgan los mismos dos amigos dos veces (A-B y B-A).

---
[[MongoDB]] | [[Cypher]] | [[Simulacro_Examen_BD2]]
