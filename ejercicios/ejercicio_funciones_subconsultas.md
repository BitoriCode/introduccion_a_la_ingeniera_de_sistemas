# Ejercicio práctico: Agregación y Subconsultas — Clínica Veterinaria PatasFelices

## Contexto

La clínica veterinaria **PatasFelices** tiene tres sedes en la ciudad y quiere analizar su actividad médica del primer bimestre. Para ello cuenta con la tabla `consultas`, que registra cada atención realizada: quién la atendió, en qué sede, qué tipo de mascota fue, qué tipo de consulta se realizó, cuánto costó y en qué mes.

Tu tarea es escribir las consultas SQL que respondan a las preguntas del área administrativa.

---

## Preparación: crear la tabla

Ejecuta este código en SQLite antes de empezar:

```sql
CREATE TABLE consultas (
    id_consulta    INTEGER PRIMARY KEY,
    veterinario    TEXT,
    sede           TEXT,
    tipo_mascota   TEXT,
    tipo_consulta  TEXT,
    costo          INTEGER,
    mes            INTEGER
);

INSERT INTO consultas VALUES (1,  'Laura',  'Norte',  'Perro',   'Vacuna',   45000, 1);
INSERT INTO consultas VALUES (2,  'Marcos', 'Centro', 'Gato',    'Cirugía', 180000, 1);
INSERT INTO consultas VALUES (3,  'Laura',  'Sur',    'Hamster', 'Vacuna',   40000, 1);
INSERT INTO consultas VALUES (4,  'Sara',   'Sur',    'Perro',   'Consulta', 30000, 1);
INSERT INTO consultas VALUES (5,  'Marcos', 'Norte',  'Perro',   'Consulta', 35000, 2);
INSERT INTO consultas VALUES (6,  'Laura',  'Norte',  'Perro',   'Cirugía', 160000, 2);
INSERT INTO consultas VALUES (7,  'Sara',   'Centro', 'Gato',    'Vacuna',   38000, 2);
INSERT INTO consultas VALUES (8,  'Marcos', 'Centro', 'Conejo',  'Consulta', 28000, 1);
INSERT INTO consultas VALUES (9,  'Laura',  'Norte',  'Conejo',  'Vacuna',   35000, 2);
INSERT INTO consultas VALUES (10, 'Sara',   'Sur',    'Perro',   'Cirugía', 200000, 1);
INSERT INTO consultas VALUES (11, 'Marcos', 'Centro', 'Gato',    'Vacuna',   42000, 2);
INSERT INTO consultas VALUES (12, 'Sara',   'Sur',    'Conejo',  'Consulta', 25000, 2);
INSERT INTO consultas VALUES (13, 'Laura',  'Norte',  'Perro',   'Consulta', 32000, 1);
INSERT INTO consultas VALUES (14, 'Marcos', 'Centro', 'Perro',   'Cirugía', 175000, 2);
INSERT INTO consultas VALUES (15, 'Sara',   'Sur',    'Gato',    'Consulta', 27000, 1);
INSERT INTO consultas VALUES (16, 'Marcos', 'Centro', 'Gato',    'Consulta', 30000, 2);
```

---

## Parte 1: Funciones de agregación básicas

**1.** ¿Cuántas consultas hay en total?

```sql

```

> Resultado esperado: 16

---

**2.** ¿Cuál fue la consulta más costosa y cuál la más barata?

```sql

```

> Resultado esperado: máximo = 200000 | mínimo = 25000

---

**3.** ¿Cuánto dinero facturó en total la clínica durante el bimestre?

```sql

```

> Resultado esperado: 1122000

---

**4.** ¿Cuál es el costo promedio de una consulta?

```sql

```

> Resultado esperado: 70125.0

---

**5.** ¿Cuántas consultas se realizaron en el mes 1?

```sql

```

> Resultado esperado: 8

---

**6.** ¿Cuánto dinero generaron en total las consultas de tipo `Cirugía`?

```sql

```

> Resultado esperado: 715000

---

**7.** ¿Cuál es el costo promedio de las consultas atendidas en la sede `Norte`?

```sql

```

> Resultado esperado: 61400.0

---

## Parte 2: GROUP BY

**8.** ¿Cuántas consultas atendió cada veterinario? Ordenar de mayor a menor cantidad.

```sql

```

> Resultado esperado:
>
> | veterinario | total_consultas |
> |-------------|-----------------|
> | Marcos      | 6               |
> | Laura       | 5               |
> | Sara        | 5               |

---

**9.** ¿Cuánto facturó en total cada veterinario? Ordenar de mayor a menor.

```sql

```

> Resultado esperado:
>
> | veterinario | total_facturado |
> |-------------|-----------------|
> | Marcos      | 490000          |
> | Sara        | 320000          |
> | Laura       | 312000          |

---

**10.** ¿Cuál es el costo promedio por tipo de consulta? Ordenar de mayor a menor promedio.

```sql

```

> Resultado esperado:
>
> | tipo_consulta | promedio_costo |
> |---------------|----------------|
> | Cirugía       | 178750.0       |
> | Vacuna        | 40000.0        |
> | Consulta      | 29571.42...    |

---

**11.** ¿Cuántas consultas se realizaron en cada sede y cuánto representaron en ingresos? Ordenar por ingresos de mayor a menor.

```sql

```

> Resultado esperado:
>
> | sede   | num_consultas | total_ingresos |
> |--------|---------------|----------------|
> | Centro | 6             | 493000         |
> | Sur    | 5             | 322000         |
> | Norte  | 5             | 307000         |

---

## Parte 3: HAVING

**12.** Mostrar solo los veterinarios cuyo total facturado supere los $400.000.

```sql

```

> Resultado esperado: Marcos (490000)

---

**13.** Mostrar solo las sedes que registraron más de 5 consultas.

```sql

```

> Resultado esperado: Centro (6)

---

**14.** Mostrar los tipos de mascota cuyo costo promedio de consulta sea superior a $50.000.

```sql

```

> Resultado esperado:
>
> | tipo_mascota | promedio_costo |
> |--------------|----------------|
> | Perro        | 96714.28...    |
> | Gato         | 63400.0        |

---

## Parte 4: Subconsultas — valor escalar

> **Recuerda:** Una subconsulta va entre paréntesis y se ejecuta primero. Cuando devuelve un único valor, puedes usarla con los operadores `=`, `>`, `<`, `>=`, `<=`.

**15.** Listar las consultas cuyo costo es superior al costo promedio general. Mostrar veterinario, tipo de mascota, tipo de consulta y costo.

```sql

```

> Resultado esperado: 4 filas (las 4 cirugías: Gato 180000, Perro 160000, Perro 200000, Perro 175000)

---

**16.** Mostrar los datos completos de la consulta más costosa.

```sql

```

> Resultado esperado: fila 10 — Sara | Sur | Perro | Cirugía | 200000 | mes 1

---

**17.** Mostrar los datos completos de la consulta más barata.

```sql

```

> Resultado esperado: fila 12 — Sara | Sur | Conejo | Consulta | 25000 | mes 2

---

**18.** ¿Qué veterinario generó el mayor ingreso total? Muestra su nombre y el total facturado.

> **Pista:** Necesitas calcular el total por veterinario (subconsulta interna) y luego quedarte con el mayor de esos totales.

```sql

```

> Resultado esperado: Marcos | 490000

---

## Parte 5: Subconsultas con IN y NOT IN

> **Recuerda:** Cuando la subconsulta puede devolver **varias filas**, usa `IN` o `NOT IN` en lugar de `=`.

**19.** Listar todas las consultas realizadas en las sedes donde trabaja Marcos. Mostrar veterinario, sede, tipo_mascota y costo.

> **Pista:** Primero identifica qué sedes tiene Marcos con `SELECT DISTINCT sede FROM consultas WHERE veterinario = 'Marcos'`, luego usa ese resultado con `IN`.

```sql

```

> Resultado esperado: 11 filas (todas las consultas de las sedes Centro y Norte)

---

**20.** ¿Qué tipos de mascota **no** ha atendido nunca Marcos? Mostrar cada tipo una sola vez.

```sql

```

> Resultado esperado: Hamster

---

**21.** Mostrar todas las consultas del tipo de mascota que tiene el mayor número de registros en la clínica. Mostrar veterinario, sede, tipo_mascota, tipo_consulta y costo, ordenado por costo descendente.

> **Pista:** Primero encuentra qué tipo de mascota aparece más veces usando `GROUP BY` y `ORDER BY COUNT(*) DESC LIMIT 1`. Luego usa ese valor con `=` en la consulta principal.

```sql

```

> Resultado esperado: 7 filas (todas las consultas de Perro), ordenadas de mayor a menor costo.
>
> | veterinario | sede   | tipo_mascota | tipo_consulta | costo  |
> |-------------|--------|--------------|---------------|--------|
> | Sara        | Sur    | Perro        | Cirugía       | 200000 |
> | Laura       | Norte  | Perro        | Cirugía       | 160000 |
> | Marcos      | Centro | Perro        | Cirugía       | 175000 |
> | Laura       | Norte  | Perro        | Vacuna        | 45000  |
> | Marcos      | Norte  | Perro        | Consulta      | 35000  |
> | Laura       | Norte  | Perro        | Consulta      | 32000  |
> | Sara        | Sur    | Perro        | Consulta      | 30000  |

---

## Resumen de conceptos practicados

| Concepto               | Ejercicios |
|------------------------|------------|
| `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` | 1 – 7  |
| `GROUP BY`             | 8 – 11     |
| `HAVING`               | 12 – 14    |
| Subconsulta escalar (`=`, `>`)       | 15 – 18    |
| Subconsulta con `IN` / `NOT IN`      | 19 – 21    |
