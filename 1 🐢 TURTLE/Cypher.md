---
materia: Bases de Datos 2
categoria: universidad
---
# Cypher: Consultas de Patrones y Recorridos en Grafos

Cypher es el lenguaje declarativo de consultas para Neo4j, diseñado para expresar patrones de datos y relaciones mediante una sintaxis visual que imita el arte ASCII. A diferencia de SQL, donde las uniones (*joins*) se calculan al vuelo, Cypher permite recorrer caminos físicos persistidos en disco de forma eficiente.

---

## ¿Cómo consultamos patrones en el grafo?

La regla de oro en Cypher es que **los paréntesis representan nodos** y **los corchetes representan relaciones**.

```javascript
// EL ESQUELETO: MATCH (nodo1:Etiqueta1)-[relacion:TIPO_RELACION]->(nodo2:Etiqueta2)
//   ├─ (nodo1:Etiqueta1): Nodo origen con alias y etiqueta opcional.
//   ├─ -[relacion:TIPO_RELACION]->: Relación dirigida con alias y tipo.
//   └─ (nodo2:Etiqueta2): Nodo destino con alias y etiqueta.
```

### Ejemplo de consulta básico:
```cypher
MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad)
RETURN p.nombre, c.nombre
```

---

## ¿Cómo creamos o actualizamos datos de manera idempotente?

Para evitar duplicar nodos o relaciones, se utiliza `MERGE` en lugar de `CREATE`. `MERGE` comprueba si el patrón ya existe; si no existe, lo crea.

```javascript
// EL ESQUELETO: MERGE (nodo:Etiqueta { propiedad: valor })
//   ├─ ON CREATE SET: Cambios que se ejecutan si el nodo se crea por primera vez.
//   └─ ON MATCH SET: Cambios que se ejecutan si el nodo ya existía.
```

```cypher
MERGE (p:Persona { email: "usuario@ejemplo.com" })
ON CREATE SET p.creado = timestamp(), p.nombre = "Juan"
ON MATCH SET p.ultimoAcceso = timestamp()
RETURN p
```

---

## ¿Cómo agrupamos y agregamos información?

En Cypher, **la agrupación es implícita**. No existe la cláusula `GROUP BY`. Cualquier variable presente en la instrucción `RETURN` que no sea una función de agregación se convierte automáticamente en el criterio de agrupación.

```cypher
MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)
RETURN e.nombre, count(p) AS totalEmpleados
```
*Aquí se agrupa implícitamente por el nombre de la empresa (`e.nombre`) y se cuenta el número de personas asociadas.*

### Error típico con conteos
Si realizas un conteo en una relación donde hay múltiples caminos entre dos nodos, contarás el mismo nodo varias veces. 
La regla de oro: utiliza `DISTINCT` dentro de las funciones de agregación para evitar duplicados en caminos redundantes.
```cypher
MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)
RETURN count(DISTINCT b)
```

---

## ¿Cómo encadenamos consultas paso a paso?

La palabra clave `WITH` actúa como un tubo o paso intermedio (*piping*) que permite realizar transformaciones, agrupaciones o filtrados parciales antes de continuar con la siguiente parte de la consulta.

**¡OJO!** Las variables que no se declaren explícitamente en la cláusula `WITH` dejan de estar disponibles en el resto de la consulta.

```cypher
MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)
WITH a, count(b) AS numeroAmigos
WHERE numeroAmigos > 5
RETURN a.nombre, numeroAmigos
```
*Error típico: Intentar usar `b` en el `RETURN` final cuando no fue declarada en el `WITH`.*

---

## ¿Cómo navegamos caminos de longitud variable?

Para buscar conexiones indirectas (como grados de separación o jerarquías), Cypher permite especificar la longitud del camino en las relaciones:
- `[:AMIGO_DE*1..3]` — Recorre de 1 a 3 relaciones de amistad.
- `[:AMIGO_DE*]` — Recorre relaciones de amistad a cualquier profundidad (cuidado con la explosión combinatoria).

Para evitar ciclos infinitos o contar dos veces la misma relación en sentido contrario en relaciones bidireccionales, se puede usar la restricción de identificador:
```cypher
MATCH (a:Persona)-[:AMIGO_DE]-(b:Persona)
WHERE id(a) < id(b)
RETURN a.nombre, b.nombre
```
*Al filtrar por `id(a) < id(b)`, evitamos que una relación simétrica aparezca dos veces en el resultado (como A-B y B-A).*
