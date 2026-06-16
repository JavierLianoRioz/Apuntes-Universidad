# Neo4j Cypher

> [!QUESTION] Ejercicio 1 (Facil) - write_query
> Obtén todas las personas que trabajan en alguna empresa y muestra el nombre de la persona y de la empresa.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN p.nombre, e.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `[['Ana', 'TechCorp'], ['Luis', 'TechCorp'], ['Marta', 'DataSoft'], ['Carlos', 'DataSoft']]`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 2 (Facil) - write_query
> Lista todas las personas que viven en Madrid.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad {nombre:'Madrid'}) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `['Ana', 'Luis', 'Elena']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 3 (Facil) - fix_query
> Corrige la consulta para devolver correctamente nombres de personas.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) RETURN nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['MATCH', 'RETURN']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 4 (Facil) - modify_query
> Modifica la consulta para limitar a 2 resultados.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) RETURN p.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) RETURN p.nombre LIMIT 2
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['LIMIT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 5 (Medio) - write_query
> Obtén las empresas junto con el número de empleados.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN e.nombre, count(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `[['TechCorp', 2], ['DataSoft', 2]]`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 6 (Medio) - write_query
> Encuentra personas que participan en proyectos y trabajan en empresa.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa), (p)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `['Ana', 'Luis', 'Marta']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 7 (Medio) - fix_query
> Corrige la consulta para usar WHERE correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) WHERE nombre='Ana' RETURN p
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) WHERE p.nombre='Ana' RETURN p
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WHERE']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 8 (Medio) - modify_query
> Modifica la consulta para ordenar por nombre.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) RETURN p.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) RETURN p.nombre ORDER BY p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ORDER BY']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 9 (Medio) - write_query
> Encuentra personas con al menos 2 amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) WITH p, count(a) as amigos WHERE amigos >= 2 RETURN p.nombre, amigos
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 10 (Dificil) - write_query
> Encuentra caminos de longitud hasta 2 entre personas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..2]->(b:Persona) RETURN p
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['*1..2']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 11 (Dificil) - write_query
> Encuentra personas conectadas a proyectos a través de amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN a.nombre, pr.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `[['Ana', 'Apollo'], ['Luis', 'Zeus']]`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 12 (Dificil) - fix_query
> Corrige la consulta para usar length correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a)-[:AMIGO_DE*]->(b) RETURN length
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a)-[:AMIGO_DE*]->(b) RETURN length(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['length']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 13 (Dificil) - modify_query
> Modifica la consulta para devolver solo la longitud del path.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN p
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN length(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['length']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 14 (Medio) - write_query
> Encuentra personas que no participan en proyectos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)
> > OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr)
> > WHERE pr IS NULL
> > RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `['Carlos', 'Elena']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 15 (Dificil) - write_query
> Encuentra personas que actúan como puente en relaciones de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:AMIGO_DE]->(c:Persona) RETURN b, count(*)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 16 (Medio) - write_query
> Obtén todas las personas junto con la ciudad en la que viven.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN p.nombre, c.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `[['Ana', 'Madrid'], ['Luis', 'Madrid'], ['Elena', 'Madrid'], ['Marta', 'Barcelona'], ['Carlos', 'Barcelona']]`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 17 (Medio) - write_query
> Cuenta cuántas personas viven en cada ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN c.nombre, count(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `[['Madrid', 3], ['Barcelona', 2]]`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 18 (Medio) - modify_query
> Modifica la consulta para devolver solo las ciudades con más de 2 personas.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN c.nombre, count(p)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) WITH c, count(p) as total WHERE total > 2 RETURN c.nombre, total
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH', 'WHERE']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 19 (Medio) - fix_query
> Corrige la consulta para que agrupe correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN p.nombre, count(e)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN e.nombre, count(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 20 (Medio) - write_query
> Obtén personas junto con el número de tecnologías que usan.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) RETURN p.nombre, count(t)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 21 (Medio) - write_query
> Encuentra personas que usan la tecnología Neo4j.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'}) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `resultado`
> > - Expected: `['Ana', 'Marta']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 22 (Medio) - write_query
> Encuentra personas que trabajan en la misma empresa.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p1:Persona)-[:TRABAJA_EN]->(e:Empresa)<-[:TRABAJA_EN]-(p2:Persona) WHERE p1 <> p2 RETURN p1.nombre, p2.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 23 (Medio) - modify_query
> Modifica la consulta para evitar duplicados en pares de personas.
> 
> **Query Base:**
> ```cypher
> MATCH (p1:Persona)-[:TRABAJA_EN]->(e)<-[:TRABAJA_EN]-(p2:Persona) RETURN p1.nombre, p2.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p1:Persona)-[:TRABAJA_EN]->(e)<-[:TRABAJA_EN]-(p2:Persona) WHERE id(p1) < id(p2) RETURN p1.nombre, p2.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['id']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 24 (Medio) - write_query
> Obtén proyectos junto con el total de horas invertidas por personas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[r:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, sum(r.horas)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['sum']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 25 (Medio) - fix_query
> Corrige la consulta para usar propiedades de relación.
> 
> **Query Base:**
> ```cypher
> MATCH (p)-[:PARTICIPA_EN]->(pr) RETURN pr.nombre, sum(horas)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p)-[r:PARTICIPA_EN]->(pr) RETURN pr.nombre, sum(r.horas)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['r.horas']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 26 (Dificil) - write_query
> Encuentra personas conectadas por cadenas de amistad de hasta longitud 3.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN a.nombre, b.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['*1..3']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 27 (Dificil) - write_query
> Devuelve los paths de amistad junto con su longitud.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN p, length(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['length']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 28 (Dificil) - modify_query
> Modifica la consulta para devolver solo paths de longitud mayor a 1.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN p
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) WHERE length(p) > 1 RETURN p
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['length']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 29 (Dificil) - write_query
> Obtén los nodos intermedios en paths de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*2..3]->(b:Persona) RETURN nodes(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['nodes']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 30 (Dificil) - write_query
> Obtén las relaciones de un path.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN relationships(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['relationships']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 31 (Medio) - write_query
> Obtén personas junto con la universidad en la que estudiaron.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad) RETURN p.nombre, u.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ESTUDIO_EN']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 32 (Medio) - write_query
> Encuentra universidades con más de un estudiante.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad) WITH u, count(p) as total WHERE total > 1 RETURN u.nombre, total
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 33 (Medio) - fix_query
> Corrige la consulta para usar WITH correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) WITH p MATCH (p)-[:VIVE_EN]->(c) RETURN c
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c) RETURN c
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 34 (Medio) - modify_query
> Modifica la consulta para devolver solo ciudades únicas.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN c.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN DISTINCT c.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 35 (Dificil) - write_query
> Encuentra personas que trabajan con alguien que usa Neo4j.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'}) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['TRABAJA_CON']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 36 (Dificil) - write_query
> Encuentra personas que viven en una ciudad distinta a la de sus amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona),(p)-[:VIVE_EN]->(c1),(a)-[:VIVE_EN]->(c2) WHERE c1 <> c2 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 37 (Dificil) - write_query
> Encuentra personas que gestionan proyectos en los que no participan.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:GESTIONA]->(pr:Proyecto) WHERE NOT (p)-[:PARTICIPA_EN]->(pr) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['NOT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 38 (Medio) - write_query
> Obtén personas junto con el número de amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) RETURN p.nombre, count(a)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 39 (Medio) - modify_query
> Modifica la consulta para mostrar solo personas con más de un amigo.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) RETURN p.nombre, count(a)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) WITH p, count(a) as total WHERE total > 1 RETURN p.nombre, total
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 40 (Dificil) - write_query
> Encuentra caminos entre personas donde todas las relaciones tienen propiedad since > 2018.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*]->(b:Persona) WHERE ALL(r IN relationships(p) WHERE r.since > 2018) RETURN p
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ALL']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 41 (Medio) - write_query
> Obtén personas junto con el número de proyectos en los que participan.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN p.nombre, count(pr)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 42 (Medio) - modify_query
> Modifica la consulta para incluir también personas sin proyectos.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN p.nombre, count(pr)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN p.nombre, count(pr)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['OPTIONAL MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 43 (Medio) - write_query
> Encuentra personas que participan en más de un proyecto.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) WITH p, count(pr) as total WHERE total > 1 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH', 'WHERE']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 44 (Medio) - write_query
> Obtén proyectos junto con el número de personas distintas que participan en ellos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, count(DISTINCT p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 45 (Medio) - fix_query
> Corrige la consulta para evitar duplicados en el conteo.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, count(p)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, count(DISTINCT p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 46 (Dificil) - write_query
> Encuentra personas que trabajan en empresas donde al menos uno de sus compañeros usa Neo4j.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa)<-[:TRABAJA_EN]-(o:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia {nombre:'Neo4j'}) RETURN DISTINCT p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 47 (Dificil) - write_query
> Encuentra personas que tienen amigos que trabajan en una empresa distinta a la suya.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e1:Empresa),(p)-[:AMIGO_DE]->(a:Persona)-[:TRABAJA_EN]->(e2:Empresa) WHERE e1 <> e2 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 48 (Dificil) - write_query
> Encuentra pares de personas que viven en la misma ciudad y trabajan juntas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p1:Persona)-[:TRABAJA_CON]->(p2:Persona),(p1)-[:VIVE_EN]->(c),(p2)-[:VIVE_EN]->(c) RETURN p1.nombre, p2.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['VIVE_EN']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 49 (Dificil) - modify_query
> Modifica la consulta para evitar pares duplicados.
> 
> **Query Base:**
> ```cypher
> MATCH (p1:Persona)-[:TRABAJA_CON]->(p2:Persona) RETURN p1.nombre, p2.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p1:Persona)-[:TRABAJA_CON]->(p2:Persona) WHERE id(p1) < id(p2) RETURN p1.nombre, p2.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['id']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 50 (Dificil) - write_query
> Encuentra personas que están conectadas por amistad a alguien que participa en más de un proyecto.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) WITH a, count(pr) as total, p WHERE total > 1 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 51 (Dificil) - write_query
> Encuentra personas que usan exactamente una tecnología.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) WITH p, count(t) as total WHERE total = 1 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 52 (Dificil) - write_query
> Encuentra personas que no tienen amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) WHERE NOT (p)-[:AMIGO_DE]->() RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['NOT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 53 (Dificil) - fix_query
> Corrige la consulta para usar OPTIONAL MATCH correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) MATCH (p)-[:PARTICIPA_EN]->(pr) RETURN p, pr
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr) RETURN p, pr
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['OPTIONAL MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 54 (Dificil) - write_query
> Encuentra caminos de amistad donde todos los nodos intermedios viven en la misma ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*2..3]->(b:Persona) WHERE ALL(n IN nodes(p)[1..-1] WHERE (n)-[:VIVE_EN]->(:Ciudad)) RETURN p
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ALL']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 55 (Dificil) - write_query
> Encuentra personas que aparecen en más de un path de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) UNWIND nodes(p) as n WITH n, count(*) as total WHERE total > 1 RETURN n, total
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['UNWIND']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 56 (Medio) - write_query
> Obtén personas junto con todas las tecnologías que usan.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) RETURN p.nombre, collect(t.nombre)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 57 (Medio) - modify_query
> Modifica la consulta para devolver solo personas que usan más de una tecnología.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) RETURN p.nombre, collect(t.nombre)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) WITH p, collect(t) as techs WHERE size(techs) > 1 RETURN p.nombre, techs
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['size']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 58 (Dificil) - write_query
> Encuentra tecnologías usadas por personas que trabajan en TechCorp.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'TechCorp'}),(p)-[:USA_TECNOLOGIA]->(t:Tecnologia) RETURN DISTINCT t.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 59 (Dificil) - write_query
> Encuentra personas que trabajan en todas las empresas presentes en el grafo.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (e:Empresa) WITH count(e) as total MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) WITH p, count(DISTINCT e) as c, total WHERE c = total RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 60 (Dificil) - write_query
> Encuentra personas que comparten todas sus tecnologías con al menos otra persona.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(t:Tecnologia) WITH p, collect(t) as techs MATCH (o:Persona)-[:USA_TECNOLOGIA]->(t2:Tecnologia) WITH p, techs, o, collect(t2) as techs2 WHERE techs = techs2 AND p <> o RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 61 (Dificil) - fix_query
> Corrige la consulta para usar correctamente UNWIND.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a)-[:AMIGO_DE*]->(b) RETURN UNWIND nodes(p)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a)-[:AMIGO_DE*]->(b) UNWIND nodes(p) as n RETURN n
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['UNWIND']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 62 (Dificil) - modify_query
> Modifica la consulta para contar cuántas veces aparece cada nodo en paths.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a)-[:AMIGO_DE*]->(b) UNWIND nodes(p) as n RETURN n
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a)-[:AMIGO_DE*]->(b) UNWIND nodes(p) as n RETURN n, count(*)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 63 (Dificil) - write_query
> Encuentra personas que están conectadas a todas las demás mediante algún path.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) MATCH (p)-[:AMIGO_DE*]->(o:Persona) WITH p, count(DISTINCT o) as total MATCH (x:Persona) WITH p, total, count(x) as all WHERE total = all - 1 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 64 (Dificil) - write_query
> Encuentra personas que conectan diferentes ciudades a través de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE]->(b:Persona)-[:AMIGO_DE]->(c:Persona),(a)-[:VIVE_EN]->(c1),(c)-[:VIVE_EN]->(c2) WHERE c1 <> c2 RETURN b.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 65 (Dificil) - write_query
> Encuentra el nodo más frecuente en paths de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*]->(b:Persona) UNWIND nodes(p) as n RETURN n, count(*) as total ORDER BY total DESC LIMIT 1
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ORDER BY', 'LIMIT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 66 (Medio) - write_query
> Obtén todas las personas junto con la empresa en la que trabajan y la ciudad en la que viven.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa),(p)-[:VIVE_EN]->(c:Ciudad) RETURN p.nombre, e.nombre, c.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 67 (Medio) - write_query
> Cuenta cuántas personas trabajan en cada empresa y viven en Madrid.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa),(p)-[:VIVE_EN]->(:Ciudad {nombre:'Madrid'}) RETURN e.nombre, count(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 68 (Medio) - modify_query
> Modifica la consulta para ordenar los resultados por número de empleados descendente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN e.nombre, count(p)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e:Empresa) RETURN e.nombre, count(p) as total ORDER BY total DESC
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ORDER BY']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 69 (Medio) - write_query
> Obtén personas que viven en la misma ciudad que sus compañeros de trabajo.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona),(p)-[:VIVE_EN]->(c),(o)-[:VIVE_EN]->(c) RETURN DISTINCT p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 70 (Medio) - fix_query
> Corrige la consulta para usar correctamente ORDER BY.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona) RETURN p.nombre ORDER p.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) RETURN p.nombre ORDER BY p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ORDER BY']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 71 (Medio) - write_query
> Encuentra proyectos gestionados por personas que trabajan en DataSoft.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'DataSoft'}),(p)-[:GESTIONA]->(pr:Proyecto) RETURN pr.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['GESTIONA']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 72 (Medio) - write_query
> Obtén personas junto con el número de amigos y el número de proyectos en los que participan.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona) OPTIONAL MATCH (p)-[:AMIGO_DE]->(a) WITH p, count(a) as amigos OPTIONAL MATCH (p)-[:PARTICIPA_EN]->(pr) RETURN p.nombre, amigos, count(pr)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 73 (Medio) - modify_query
> Modifica la consulta para mostrar solo personas con al menos un amigo.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:AMIGO_DE]->(a) RETURN p.nombre, count(a)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a) WITH p, count(a) as total WHERE total > 0 RETURN p.nombre, total
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WHERE']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 74 (Dificil) - write_query
> Encuentra personas cuyos amigos participan en proyectos distintos a los suyos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr1),(p)-[:AMIGO_DE]->(a:Persona)-[:PARTICIPA_EN]->(pr2) WHERE pr1 <> pr2 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 75 (Dificil) - write_query
> Encuentra personas que trabajan con alguien que vive en otra ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona),(p)-[:VIVE_EN]->(c1),(o)-[:VIVE_EN]->(c2) WHERE c1 <> c2 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['<>']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 76 (Dificil) - write_query
> Encuentra personas que comparten al menos una tecnología.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) MATCH (p)-[:USA_TECNOLOGIA]->(t:Tecnologia),(a)-[:USA_TECNOLOGIA]->(t) RETURN DISTINCT p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 77 (Dificil) - fix_query
> Corrige la consulta para aplicar correctamente múltiples MATCH.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:TRABAJA_EN]->(e) MATCH (p)-[:VIVE_EN]->(c) RETURN p,e,c
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e),(p)-[:VIVE_EN]->(c) RETURN p,e,c
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 78 (Dificil) - modify_query
> Modifica la consulta para devolver solo nombres únicos de personas.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona) RETURN p.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_CON]->(o:Persona) RETURN DISTINCT p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 79 (Medio) - write_query
> Obtén personas junto con el número total de relaciones que tienen.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)--() RETURN p.nombre, count(*)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['--']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 80 (Medio) - write_query
> Encuentra personas conectadas a al menos un proyecto a través de cualquier relación.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-->(:Proyecto) RETURN DISTINCT p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['--']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 81 (Dificil) - write_query
> Encuentra personas que están a distancia exactamente 2 en la red de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE*2..2]->(b:Persona) RETURN a.nombre, b.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['*2..2']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 82 (Dificil) - modify_query
> Modifica la consulta para excluir relaciones directas.
> 
> **Query Base:**
> ```cypher
> MATCH (a:Persona)-[:AMIGO_DE*1..2]->(b:Persona) RETURN a,b
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (a:Persona)-[:AMIGO_DE*2..2]->(b:Persona) RETURN a,b
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['*2..2']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 83 (Medio) - write_query
> Encuentra ciudades donde viven personas que trabajan en TechCorp.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(:Empresa {nombre:'TechCorp'}),(p)-[:VIVE_EN]->(c:Ciudad) RETURN DISTINCT c.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 84 (Medio) - write_query
> Obtén universidades junto con el número de personas que estudiaron en ellas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:ESTUDIO_EN]->(u:Universidad) RETURN u.nombre, count(p)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 85 (Medio) - fix_query
> Corrige la consulta para usar DISTINCT correctamente.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN c.nombre
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN DISTINCT c.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 86 (Dificil) - write_query
> Encuentra personas cuyos amigos viven todos en la misma ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona),(a)-[:VIVE_EN]->(c:Ciudad) WITH p, collect(DISTINCT c) as ciudades WHERE size(ciudades)=1 RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect', 'size']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 87 (Dificil) - write_query
> Encuentra personas que trabajan en empresas donde todos los empleados viven en la misma ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (e:Empresa)<-[:TRABAJA_EN]-(p:Persona),(p)-[:VIVE_EN]->(c:Ciudad) WITH e, collect(DISTINCT c) as ciudades WHERE size(ciudades)=1 MATCH (e)<-[:TRABAJA_EN]-(p2:Persona) RETURN p2.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect', 'size']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 88 (Dificil) - write_query
> Encuentra personas que tienen al menos un amigo en cada ciudad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (c:Ciudad) WITH collect(c) as ciudades MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:VIVE_EN]->(c2:Ciudad) WITH p, collect(DISTINCT c2) as ciudades2, ciudades WHERE ciudades2 = ciudades RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 89 (Dificil) - modify_query
> Modifica la consulta para limitar a los 3 resultados con más amigos.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) RETURN p.nombre, count(a)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona) RETURN p.nombre, count(a) as total ORDER BY total DESC LIMIT 3
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['LIMIT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 90 (Dificil) - write_query
> Encuentra personas que están conectadas por amistad a alguien que trabaja en todas las empresas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (e:Empresa) WITH count(e) as total MATCH (a:Persona)-[:TRABAJA_EN]->(e:Empresa) WITH a, count(DISTINCT e) as c, total WHERE c = total MATCH (p:Persona)-[:AMIGO_DE]->(a) RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['WITH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 91 (Dificil) - write_query
> Encuentra personas que tienen más amigos que la media.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a) WITH p, count(a) as total WITH collect(total) as totales, p, total WITH p, total, reduce(s=0, x IN totales | s + x) / size(totales) as media WHERE total > media RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['avg']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 92 (Dificil) - write_query
> Encuentra personas que están conectadas con otras mediante más de un camino distinto.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) WITH a,b,count(p) as total WHERE total > 1 RETURN a.nombre, b.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['count']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 93 (Dificil) - write_query
> Encuentra personas cuyos amigos trabajan en todas las empresas.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (e:Empresa) WITH collect(e) as empresas MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:TRABAJA_EN]->(e2:Empresa) WITH p, collect(DISTINCT e2) as empresas2, empresas WHERE empresas2 = empresas RETURN p.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 94 (Dificil) - write_query
> Encuentra personas que están en todos los caminos entre dos nodos específicos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona {nombre:'Ana'})-[:AMIGO_DE*]->(b:Persona {nombre:'Carlos'}) UNWIND nodes(p) as n RETURN n, count(*) as total ORDER BY total DESC
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['UNWIND']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 95 (Dificil) - modify_query
> Modifica la consulta para devolver solo los nodos más frecuentes.
> 
> **Query Base:**
> ```cypher
> MATCH p=(a)-[:AMIGO_DE*]->(b) UNWIND nodes(p) as n RETURN n, count(*)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a)-[:AMIGO_DE*]->(b) UNWIND nodes(p) as n RETURN n, count(*) as total ORDER BY total DESC LIMIT 1
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['LIMIT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 96 (Medio) - write_query
> Obtén personas junto con todas las ciudades en las que tienen amigos.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:AMIGO_DE]->(a:Persona)-[:VIVE_EN]->(c:Ciudad) RETURN p.nombre, collect(DISTINCT c.nombre)
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['collect']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 97 (Medio) - write_query
> Encuentra empresas donde trabajan personas que usan Python.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:USA_TECNOLOGIA]->(:Tecnologia {nombre:'Python'}),(p)-[:TRABAJA_EN]->(e:Empresa) RETURN DISTINCT e.nombre
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['DISTINCT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 98 (Medio) - fix_query
> Corrige la consulta para usar correctamente múltiples relaciones.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:TRABAJA_EN]->(e)-[:VIVE_EN]->(c) RETURN p,e,c
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:TRABAJA_EN]->(e),(p)-[:VIVE_EN]->(c) RETURN p,e,c
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['MATCH']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 99 (Medio) - modify_query
> Modifica la consulta para devolver solo los 2 proyectos con más participantes.
> 
> **Query Base:**
> ```cypher
> MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, count(p)
> ```
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH (p:Persona)-[:PARTICIPA_EN]->(pr:Proyecto) RETURN pr.nombre, count(p) as total ORDER BY total DESC LIMIT 2
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['LIMIT']`
> > - Wildcard: `True`

> [!QUESTION] Ejercicio 100 (Dificil) - write_query
> Encuentra personas que maximizan el número de conexiones indirectas en la red de amistad.
> > [!SUCCESS] Solución
> > **Query:**
> > ```cypher
> > MATCH p=(a:Persona)-[:AMIGO_DE*1..3]->(b:Persona) RETURN a.nombre, count(DISTINCT b) as total ORDER BY total DESC LIMIT 1
> > ```
> > 
> > **Validación:**
> > - Tipo: `estructura`
> > - Expected: `['ORDER BY', 'LIMIT']`
> > - Wildcard: `True`

# Bases Vectoriales y FAISS

> [!QUESTION] Ejercicio 1 (Facil) - modify_dataset
> Agregue al vocabulario los textos 'tigre salvaje asiático' y 'león africano grande'. Luego ejecute una búsqueda usando la query 'felino'. Analice cómo cambian los resultados.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción correcta de textos
> > - Reconstrucción válida del índice
> > - Uso correcto de búsqueda
> > - Interpretación semántica básica

> [!QUESTION] Ejercicio 2 (Facil) - analyze_results
> Ejecute búsquedas usando las queries 'vehículo rápido' y 'coche deportivo'. Compare los resultados obtenidos y explique cuál query parece más específica.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Ejecución correcta de búsquedas
> > - Comparación de rankings
> > - Interpretación contextual

> [!QUESTION] Ejercicio 3 (Facil) - modify_dataset
> Agregue al vocabulario los textos 'banco de inversión internacional' y 'banco para descansar'. Luego busque la palabra 'banco' y explique los casos de ambigüedad encontrados.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción correcta
> > - Detección de ambigüedad
> > - Interpretación semántica

> [!QUESTION] Ejercicio 4 (Facil) - compare_queries
> Ejecute búsquedas usando 'pizza', 'pizza italiana' y 'pizza italiana tradicional'. Explique cómo cambia el ranking al agregar más contexto.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación correcta
> > - Análisis contextual
> > - Interpretación del embedding

> [!QUESTION] Ejercicio 5 (Facil) - modify_function
> Modifique la función buscar() para que también devuelva el índice original del texto encontrado.
> 
> **Código Base:**
> ```python
> resultados.append({'texto': base[i], 'distancia': distancia, 'score': score})
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto del índice
> > - Modificación funcional
> > - Estructura válida del resultado

> [!QUESTION] Ejercicio 6 (Facil) - analyze_results
> Ejecute búsquedas usando la query 'animal'. Explique por qué algunos resultados parecen menos precisos.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Análisis de resultados
> > - Interpretación de ambigüedad
> > - Relación con contexto

> [!QUESTION] Ejercicio 7 (Facil) - modify_dataset
> Inserte en el vocabulario textos relacionados con astronomía y luego ejecute búsquedas sobre animales. Explique cómo afecta esto al sistema.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción válida
> > - Análisis de contaminación semántica
> > - Interpretación del ranking

> [!QUESTION] Ejercicio 8 (Facil) - complete_function
> Complete la función calcular_score() usando la fórmula 1 / (1 + distancia).
> 
> **Código Base:**
> ```python
> def calcular_score(distancia):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Implementación correcta
> > - Uso válido de distancia
> > - Retorno funcional

> [!QUESTION] Ejercicio 9 (Facil) - compare_queries
> Compare resultados entre las queries 'tecnología' y 'computadora portátil moderna'. Explique cuál produce resultados más específicos.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación válida
> > - Interpretación contextual
> > - Relación entre especificidad y embedding

> [!QUESTION] Ejercicio 10 (Facil) - modify_dataset
> Agregue tres tipos distintos de comida al vocabulario y ejecute búsquedas usando la palabra 'comida'. Explique cómo aparecen agrupaciones semánticas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción correcta
> > - Uso válido de búsquedas
> > - Interpretación de similitud

> [!QUESTION] Ejercicio 11 (Facil) - analyze_results
> Ejecute búsquedas usando la query 'objeto'. Explique por qué el sistema devuelve resultados débiles o ambiguos.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Interpretación de baja especificidad
> > - Relación con embeddings
> > - Análisis contextual

> [!QUESTION] Ejercicio 12 (Facil) - modify_function
> Modifique la función buscar() para que imprima también la distancia encontrada por FAISS.
> 
> **Código Base:**
> ```python
> resultados.append({'texto': base[i], 'score': score})
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de distancia
> > - Modificación funcional
> > - Resultado válido

> [!QUESTION] Ejercicio 13 (Facil) - compare_queries
> Compare búsquedas usando 'ratón' y 'ratón inalámbrico computadora'. Explique diferencias semánticas observadas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación correcta
> > - Análisis de ambigüedad
> > - Interpretación contextual

> [!QUESTION] Ejercicio 14 (Facil) - modify_dataset
> Agregue palabras relacionadas con deportes y luego busque 'vehículo rápido'. Analice si aparecen resultados inesperados.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción correcta
> > - Análisis de contaminación
> > - Interpretación del ranking

> [!QUESTION] Ejercicio 15 (Facil) - complete_function
> Complete una función que reciba una query y ejecute embedding(query).
> 
> **Código Base:**
> ```python
> def generar_query(query):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de embedding
> > - Implementación funcional
> > - Retorno válido

> [!QUESTION] Ejercicio 16 (Facil) - analyze_results
> Ejecute búsquedas usando 'galaxia' y explique por qué aparecen ciertos resultados cercanos aunque no sean exactos.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Interpretación geométrica
> > - Relación entre proximidad y significado
> > - Análisis semántico

> [!QUESTION] Ejercicio 17 (Facil) - modify_dataset
> Agregue textos relacionados con videojuegos y luego ejecute búsquedas usando 'tecnología'. Explique el comportamiento del sistema.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción correcta
> > - Relación entre dominios
> > - Interpretación semántica

> [!QUESTION] Ejercicio 18 (Facil) - modify_function
> Modifique la función buscar_filtrado() para usar un umbral mínimo de 0.5.
> 
> **Código Base:**
> ```python
> if r['score'] >= umbral:
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de umbral
> > - Filtrado válido
> > - Modificación funcional

> [!QUESTION] Ejercicio 19 (Facil) - compare_queries
> Compare resultados entre las queries 'felino' y 'felino salvaje africano'. Explique cómo cambia el contexto.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación contextual
> > - Interpretación semántica
> > - Análisis de especificidad

> [!QUESTION] Ejercicio 20 (Facil) - analyze_results
> Ejecute búsquedas usando 'computadora'. Explique por qué algunos resultados tecnológicos tienen scores más altos que otros.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Interpretación de score
> > - Relación semántica
> > - Análisis del ranking

> [!QUESTION] Ejercicio 21 (Medio) - modify_function
> Modifique la función buscar() para que los resultados se devuelvan ordenados por score descendente.
> 
> **Código Base:**
> ```python
> return resultados
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Ordenamiento correcto
> > - Uso válido de score
> > - No alterar búsqueda FAISS

> [!QUESTION] Ejercicio 22 (Medio) - extend_system
> Implemente una función que permita agregar nuevos textos al vocabulario y reconstruir automáticamente el índice FAISS.
> 
> **Código Base:**
> ```python
> def agregar(self, texto):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción dinámica correcta
> > - Reconstrucción válida del índice
> > - Actualización funcional del sistema

> [!QUESTION] Ejercicio 23 (Medio) - analyze_results
> Ejecute búsquedas usando las queries 'automóvil', 'coche', 'vehículo' y 'carro'. Compare diferencias de ranking y similitud.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación semántica
> > - Interpretación lingüística
> > - Análisis contextual

> [!QUESTION] Ejercicio 24 (Medio) - modify_function
> Modifique la función buscar_filtrado() para permitir que el usuario envíe el valor de k dinámicamente.
> 
> **Código Base:**
> ```python
> def buscar_filtrado(query, base, index, umbral=0.3, k=5):
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso dinámico de k
> > - Filtrado funcional
> > - Modificación correcta de parámetros

> [!QUESTION] Ejercicio 25 (Medio) - compare_queries
> Compare resultados entre una query de una palabra y una frase larga relacionada. Explique cómo cambia el embedding.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación contextual
> > - Interpretación de embeddings
> > - Relación entre contexto y ranking

> [!QUESTION] Ejercicio 26 (Medio) - extend_system
> Implemente una función que exporte los resultados de búsqueda a un diccionario JSON con texto, score y distancia.
> 
> **Código Base:**
> ```python
> def exportar_resultados(resultados):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Exportación correcta
> > - Formato JSON válido
> > - Persistencia estructurada

> [!QUESTION] Ejercicio 27 (Medio) - analyze_results
> Inserte varios textos muy similares y analice cómo cambia el ranking cuando existen múltiples embeddings cercanos.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción válida
> > - Interpretación de saturación semántica
> > - Análisis de ambigüedad

> [!QUESTION] Ejercicio 28 (Medio) - modify_dataset
> Agregue frases extremadamente largas al vocabulario y compare los resultados contra frases cortas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción válida
> > - Análisis contextual
> > - Interpretación de embeddings largos

> [!QUESTION] Ejercicio 29 (Medio) - modify_function
> Cambie la fórmula de score por una nueva función distinta a 1/(1+distancia) y compare resultados.
> 
> **Código Base:**
> ```python
> score = 1 / (1 + distancia)
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Modificación funcional
> > - Comparación de comportamiento
> > - Interpretación matemática básica

> [!QUESTION] Ejercicio 30 (Medio) - compare_queries
> Compare búsquedas usando 'animal peligroso', 'felino peligroso' y 'felino salvaje africano peligroso'.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación contextual
> > - Interpretación de especificidad
> > - Análisis semántico

> [!QUESTION] Ejercicio 31 (Medio) - extend_system
> Implemente una función que registre cada búsqueda junto con su timestamp y score máximo.
> 
> **Código Base:**
> ```python
> def registrar_busqueda(query, score):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Logging correcto
> > - Persistencia funcional
> > - Uso válido de score

> [!QUESTION] Ejercicio 32 (Medio) - analyze_results
> Ejecute búsquedas con errores ortográficos intencionales y explique cómo responde el sistema.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Pruebas válidas
> > - Análisis de robustez
> > - Interpretación de limitaciones

> [!QUESTION] Ejercicio 33 (Medio) - modify_function
> Modifique la función buscar() para mostrar únicamente resultados cuyo score sea mayor a 0.4.
> 
> **Código Base:**
> ```python
> for j, i in enumerate(indices[0]):
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Filtrado correcto
> > - Uso válido de score
> > - No romper la búsqueda

> [!QUESTION] Ejercicio 34 (Medio) - extend_system
> Implemente una función que permita buscar únicamente dentro de una categoría específica como animales o tecnología.
> 
> **Código Base:**
> ```python
> def buscar_categoria(query, categoria):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Filtrado correcto por categoría
> > - Separación de dominios
> > - Implementación funcional

> [!QUESTION] Ejercicio 35 (Medio) - compare_queries
> Compare resultados usando IndexFlatL2 e IndexFlatIP. Explique diferencias observadas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Cambio correcto de índice
> > - Comparación válida
> > - Interpretación geométrica

> [!QUESTION] Ejercicio 36 (Medio) - modify_dataset
> Agregue textos de múltiples dominios como política, cocina y videojuegos. Analice contaminación semántica.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Inserción válida
> > - Análisis de contaminación
> > - Interpretación contextual

> [!QUESTION] Ejercicio 37 (Medio) - extend_system
> Implemente una función que calcule similitud entre dos textos usando embeddings sin utilizar FAISS.
> 
> **Código Base:**
> ```python
> def similitud(texto1, texto2):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de embeddings
> > - Cálculo válido de similitud
> > - Interpretación funcional

> [!QUESTION] Ejercicio 38 (Medio) - analyze_results
> Analice casos donde scores altos producen resultados incorrectos o inesperados.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Identificación de anomalías
> > - Interpretación geométrica
> > - Análisis de limitaciones

> [!QUESTION] Ejercicio 39 (Medio) - modify_function
> Modifique la función buscar() para devolver también la categoría del texto encontrado.
> 
> **Código Base:**
> ```python
> resultados.append({'texto': base[i]})
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Integración correcta de categorías
> > - Modificación funcional
> > - Resultados estructurados

> [!QUESTION] Ejercicio 40 (Medio) - compare_queries
> Compare el comportamiento del sistema usando bases pequeñas especializadas frente a bases grandes mezcladas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación válida
> > - Análisis de especialización
> > - Interpretación de ruido semántico

> [!QUESTION] Ejercicio 41 (Dificil) - extend_system
> Implemente una función llamada buscar_multidominio() que permita recibir una query y retornar resultados agrupados por categoría ('animales', 'vehículos', 'tecnología'). El sistema debe filtrar resultados con score menor a 0.4.
> 
> **Código Base:**
> ```python
> def buscar_multidominio(query):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Agrupación correcta por categoría
> > - Filtrado válido
> > - Uso correcto de score
> > - Estructura funcional

> [!QUESTION] Ejercicio 42 (Dificil) - extend_system
> Implemente persistencia completa del índice FAISS utilizando escritura y lectura desde disco.
> 
> **Código Base:**
> ```python
> faiss.write_index(index, 'indice.faiss')
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Persistencia funcional
> > - Carga correcta del índice
> > - Reutilización válida del sistema

> [!QUESTION] Ejercicio 43 (Dificil) - modify_function
> Modifique el sistema para detectar posibles queries fuera de dominio utilizando score promedio mínimo.
> 
> **Código Base:**
> ```python
> def detectar_fuera_dominio(query):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de score
> > - Detección funcional
> > - Interpretación de umbrales

> [!QUESTION] Ejercicio 44 (Dificil) - extend_system
> Implemente una función que elimine textos del vocabulario y reconstruya completamente el índice FAISS.
> 
> **Código Base:**
> ```python
> def eliminar(texto):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Eliminación correcta
> > - Reconstrucción válida
> > - Consistencia del índice

> [!QUESTION] Ejercicio 45 (Dificil) - analyze_results
> Analice por qué dos textos semánticamente distintos pueden terminar geométricamente cercanos dentro del espacio vectorial.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Interpretación geométrica
> > - Comprensión de embeddings
> > - Análisis de limitaciones semánticas

> [!QUESTION] Ejercicio 46 (Dificil) - extend_system
> Construya un mini recomendador semántico que sugiera textos similares a partir del historial de búsquedas realizadas.
> 
> **Código Base:**
> ```python
> historial = []
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Uso correcto de historial
> > - Recomendación funcional
> > - Aplicación de similitud semántica

> [!QUESTION] Ejercicio 47 (Dificil) - modify_function
> Modifique buscar_filtrado() para calcular dinámicamente el umbral usando el score promedio de los resultados.
> 
> **Código Base:**
> ```python
> def buscar_filtrado(query, base, index, umbral=0.3, k=5):
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Cálculo dinámico correcto
> > - Uso válido de promedio
> > - Filtrado funcional

> [!QUESTION] Ejercicio 48 (Dificil) - extend_system
> Implemente una función que compare múltiples queries simultáneamente y devuelva los textos más relevantes para todas ellas.
> 
> **Código Base:**
> ```python
> def comparar_queries(queries):
>     # completar
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Procesamiento múltiple
> > - Agregación correcta
> > - Interpretación de relevancia

> [!QUESTION] Ejercicio 49 (Dificil) - analyze_results
> Compare el comportamiento del sistema usando textos extremadamente cortos frente a descripciones largas y detalladas.
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Comparación contextual
> > - Interpretación de embeddings
> > - Análisis de recuperación semántica

> [!QUESTION] Ejercicio 50 (Dificil) - extend_system
> Construya un mini sistema semántico completo que incluya embeddings, índice FAISS, score, filtrado, logging y persistencia básica. Luego explique fortalezas, limitaciones y posibles usos empresariales.
> 
> **Código Base:**
> ```python
> class BuscadorSemantico:
>     # extender sistema
> ```
> > [!SUCCESS] Solución
> > **Criterios de Evaluación:**
> > - Integración completa
> > - Uso correcto de FAISS
> > - Persistencia funcional
> > - Logging válido
> > - Análisis crítico del sistema
