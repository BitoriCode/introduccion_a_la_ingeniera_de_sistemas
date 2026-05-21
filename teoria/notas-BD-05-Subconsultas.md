# Notas de Estudio — Módulo 5: Subconsultas

> **Objetivo:** Al terminar de leer estas notas, podrás escribir subconsultas en la cláusula WHERE (con `=` y con `IN`), subconsultas escalares en el SELECT, y distinguir entre subconsultas correlacionadas y no correlacionadas.

---

## Tabla de práctica

Seguimos con la tabla `estudiantes`:

| id_estudiante | nombre | apellido | ciudad | semestre | promedio |
|---|---|---|---|---|---|
| 1 | Camila | Rodríguez | Bogotá | 3 | 4.2 |
| 2 | Andrés | Martínez | Medellín | 5 | 3.8 |
| 3 | Valentina | López | Bogotá | 1 | 4.7 |
| 4 | Sebastián | García | Cali | 3 | 2.9 |
| 5 | Daniela | Torres | Medellín | 5 | 4.5 |
| 6 | Felipe | Ramírez | Bogotá | 2 | 3.1 |
| 7 | Laura | Sánchez | Barranquilla | 1 | 3.9 |
| 8 | Juan | Díaz | Cali | 5 | 4.8 |
| 9 | Mateo | Herrera | Bogotá | 3 | NULL |

---

## 1. ¿Qué es una subconsulta?

Una **subconsulta** (*subquery* o consulta anidada) es una sentencia `SELECT` escrita **dentro de otra sentencia SQL**. La subconsulta se ejecuta **primero**, y su resultado es usado por la consulta exterior.

```sql
SELECT columnas
FROM tabla
WHERE columna OPERADOR (
    SELECT ...          ← subconsulta: se ejecuta primero
    FROM ...
    WHERE ...
);
```

**Regla:** La subconsulta **siempre va entre paréntesis**.

### ¿Por qué usar subconsultas?

A veces necesitamos dos pasos de razonamiento:

1. Pregunta auxiliar: *"¿Cuál es el promedio general?"* → `4.2375`
2. Pregunta real: *"¿Quiénes están por encima de ese valor?"*

Sin subconsultas tendríamos que hacer la consulta 1, anotar el resultado y usarlo manualmente en la consulta 2. Con subconsultas, automatizamos ese proceso en una sola sentencia.

---

## 2. Subconsulta en WHERE con valor único

Cuando la subconsulta devuelve **exactamente un valor** (un número, un texto), se usa con operadores de comparación: `=`, `<>`, `>`, `<`, `>=`, `<=`.

### Ejemplo 1: Estudiantes por encima del promedio general

```sql
-- Sin subconsulta (en dos pasos):
-- Paso 1: ¿cuál es el promedio general?
SELECT AVG(promedio) FROM estudiantes;   -- → 4.2375

-- Paso 2: ¿quiénes están por encima?
SELECT nombre, promedio FROM estudiantes WHERE promedio > 4.2375;
```

```sql
-- Con subconsulta (en un solo paso):
SELECT nombre, promedio
FROM estudiantes
WHERE promedio > (SELECT AVG(promedio) FROM estudiantes);
```

| nombre | promedio |
|---|---|
| Valentina | 4.7 |
| Daniela | 4.5 |
| Juan | 4.8 |

SQL ejecuta primero `SELECT AVG(promedio) FROM estudiantes` → obtiene `4.2375` → luego filtra con `WHERE promedio > 4.2375`.

---

### Ejemplo 2: El estudiante con el promedio más alto

```sql
SELECT nombre, promedio
FROM estudiantes
WHERE promedio = (SELECT MAX(promedio) FROM estudiantes);
```

| nombre | promedio |
|---|---|
| Juan | 4.8 |

---

### Ejemplo 3: Estudiantes del mismo semestre que Camila

```sql
SELECT nombre, semestre
FROM estudiantes
WHERE semestre = (
    SELECT semestre
    FROM estudiantes
    WHERE nombre = 'Camila' AND apellido = 'Rodríguez'
)
AND nombre <> 'Camila';
```

| nombre | semestre |
|---|---|
| Sebastián | 3 |
| Mateo | 3 |

---

### Tabla de operadores para subconsultas de valor único

| Operador | Uso | Condición |
|---|---|---|
| `= (subquery)` | Igual al valor | La subconsulta debe devolver **exactamente 1 fila** |
| `<> (subquery)` | Diferente al valor | La subconsulta debe devolver **exactamente 1 fila** |
| `> (subquery)` | Mayor que el valor | La subconsulta debe devolver **exactamente 1 fila** |
| `< (subquery)` | Menor que el valor | La subconsulta debe devolver **exactamente 1 fila** |
| `>= (subquery)` | Mayor o igual | La subconsulta debe devolver **exactamente 1 fila** |
| `<= (subquery)` | Menor o igual | La subconsulta debe devolver **exactamente 1 fila** |

> **Error común:** Si una subconsulta con `=` devuelve más de una fila, SQL lanza un error. Usar `IN` cuando la subconsulta puede devolver múltiples resultados.

---

## 3. Subconsulta en WHERE con IN

Cuando la subconsulta puede devolver **múltiples valores** (una lista), se usa `IN` o `NOT IN`.

```sql
WHERE columna IN (
    SELECT columna
    FROM ...
)
```

### Ejemplo 1: Estudiantes en semestres con promedio grupal > 4.0

```sql
-- Paso 1: ¿qué semestres tienen promedio grupal > 4.0?
SELECT semestre
FROM estudiantes
GROUP BY semestre
HAVING AVG(promedio) > 4.0;
-- → semestres 1 y 5
```

```sql
-- Consulta completa:
SELECT nombre, semestre, promedio
FROM estudiantes
WHERE semestre IN (
    SELECT semestre
    FROM estudiantes
    GROUP BY semestre
    HAVING AVG(promedio) > 4.0
);
```

| nombre | semestre | promedio |
|---|---|---|
| Andrés | 5 | 3.8 |
| Valentina | 1 | 4.7 |
| Daniela | 5 | 4.5 |
| Laura | 1 | 3.9 |
| Juan | 5 | 4.8 |

Nota: Andrés tiene promedio 3.8 (por debajo del general) pero pertenece al **semestre 5**, cuyo promedio grupal sí supera 4.0.

---

### Ejemplo 2: Estudiantes de la misma ciudad que Laura

```sql
SELECT nombre, ciudad
FROM estudiantes
WHERE ciudad IN (
    SELECT ciudad
    FROM estudiantes
    WHERE nombre = 'Laura' AND apellido = 'Sánchez'
)
AND nombre <> 'Laura';
```

*(Laura es de Barranquilla, que tiene solo un estudiante → resultado vacío. Si hubiera más, aparecerían aquí.)*

---

### Ejemplo 3: NOT IN — excluir un conjunto

```sql
-- Estudiantes que NO están en los semestres más avanzados (3 y 5):
SELECT nombre, semestre
FROM estudiantes
WHERE semestre NOT IN (
    SELECT semestre FROM estudiantes WHERE semestre >= 3
);
```

| nombre | semestre |
|---|---|
| Valentina | 1 |
| Felipe | 2 |
| Laura | 1 |

---

## 4. Subconsulta en SELECT (subconsulta escalar)

Una subconsulta puede ubicarse en la lista de columnas del `SELECT`. Debe devolver **exactamente un valor** y ese valor se muestra en cada fila del resultado.

### Ejemplo 1: Promedio de cada estudiante vs promedio general

```sql
SELECT 
    nombre,
    promedio,
    (SELECT AVG(promedio) FROM estudiantes) AS promedio_general
FROM estudiantes
WHERE promedio IS NOT NULL;
```

| nombre | promedio | promedio_general |
|---|---|---|
| Camila | 4.2 | 4.2375 |
| Andrés | 3.8 | 4.2375 |
| Valentina | 4.7 | 4.2375 |
| Sebastián | 2.9 | 4.2375 |
| Daniela | 4.5 | 4.2375 |
| Felipe | 3.1 | 4.2375 |
| Laura | 3.9 | 4.2375 |
| Juan | 4.8 | 4.2375 |

La subconsulta en el SELECT se ejecuta una sola vez y el mismo valor (`4.2375`) aparece en todas las filas.

---

### Ejemplo 2: Diferencia respecto al promedio general

```sql
SELECT 
    nombre,
    promedio,
    ROUND(promedio - (SELECT AVG(promedio) FROM estudiantes), 2) AS diferencia
FROM estudiantes
WHERE promedio IS NOT NULL
ORDER BY diferencia DESC;
```

| nombre | promedio | diferencia |
|---|---|---|
| Juan | 4.8 | 0.56 |
| Valentina | 4.7 | 0.46 |
| Daniela | 4.5 | 0.26 |
| Camila | 4.2 | -0.04 |
| Laura | 3.9 | -0.34 |
| Andrés | 3.8 | -0.44 |
| Felipe | 3.1 | -1.14 |
| Sebastián | 2.9 | -1.34 |

---

## 5. Subconsultas no correlacionadas vs correlacionadas

### Subconsulta no correlacionada

La subconsulta **no usa datos de la consulta exterior** — es completamente independiente y se ejecuta una sola vez.

```sql
-- La subconsulta AVG(promedio) no necesita saber qué fila está procesando la exterior
SELECT nombre, promedio
FROM estudiantes
WHERE promedio > (SELECT AVG(promedio) FROM estudiantes);
--                ↑ independiente — se ejecuta una sola vez
```

Flujo:
1. Se ejecuta `SELECT AVG(promedio) FROM estudiantes` → resultado: `4.2375`
2. Se usa ese número fijo para filtrar todas las filas de la consulta exterior

**Todas las subconsultas del curso son no correlacionadas.**

---

### Subconsulta correlacionada (concepto)

La subconsulta **hace referencia a la fila actual** de la consulta exterior. Se ejecuta **una vez por cada fila**.

```sql
-- Ejemplo conceptual (avanzado — fuera del alcance del examen):
-- "Estudiantes cuyo promedio supera el promedio de su misma ciudad"
SELECT e1.nombre, e1.ciudad, e1.promedio
FROM estudiantes e1
WHERE e1.promedio > (
    SELECT AVG(e2.promedio)
    FROM estudiantes e2
    WHERE e2.ciudad = e1.ciudad   -- ← referencia a e1: la consulta exterior
);
```

> **En este curso:** Las subconsultas correlacionadas son un tema avanzado. Solo se necesita conocer el concepto para diferenciarlo.

---

## 6. Reglas y buenas prácticas

### ¿Qué debe devolver la subconsulta según el contexto?

| Dónde está la subconsulta | Debe devolver |
|---|---|
| `WHERE col = (subquery)` | Exactamente 1 valor (1 fila, 1 columna) |
| `WHERE col > (subquery)` | Exactamente 1 valor (1 fila, 1 columna) |
| `WHERE col IN (subquery)` | 1 columna, cualquier número de filas |
| `SELECT (subquery)` | Exactamente 1 valor (1 fila, 1 columna) |

### Estrategia: probar la subconsulta por separado

Antes de escribir la consulta completa, ejecutar la subconsulta sola para verificar que devuelve lo esperado:

```sql
-- Paso 1: verificar la subconsulta
SELECT AVG(promedio) FROM estudiantes;
-- → 4.2375 ✓ un solo valor, perfecto para usar con =, >, etc.

-- Paso 2: integrar en la consulta completa
SELECT nombre, promedio
FROM estudiantes
WHERE promedio > (SELECT AVG(promedio) FROM estudiantes);
```

### Indentar para mayor legibilidad

```sql
-- ❌ Difícil de leer:
SELECT nombre FROM estudiantes WHERE semestre IN (SELECT semestre FROM estudiantes GROUP BY semestre HAVING AVG(promedio) > 4.0);

-- ✅ Fácil de leer:
SELECT nombre
FROM estudiantes
WHERE semestre IN (
    SELECT semestre
    FROM estudiantes
    GROUP BY semestre
    HAVING AVG(promedio) > 4.0
);
```

---

## 7. Comparación de las tres posiciones de una subconsulta

```sql
-- Posición 1: en WHERE con valor único
SELECT nombre FROM estudiantes
WHERE promedio = (SELECT MAX(promedio) FROM estudiantes);

-- Posición 2: en WHERE con IN
SELECT nombre FROM estudiantes
WHERE semestre IN (SELECT semestre FROM estudiantes GROUP BY semestre HAVING COUNT(*) >= 3);

-- Posición 3: en SELECT (escalar)
SELECT nombre, (SELECT MAX(promedio) FROM estudiantes) AS record
FROM estudiantes;
```

---

## 8. Resumen rápido (cheatsheet)

| Tipo | Sintaxis | La subconsulta devuelve |
|---|---|---|
| Valor único con `=` | `WHERE col = (SELECT ...)` | 1 fila, 1 columna |
| Valor único con `>`, `<` | `WHERE col > (SELECT ...)` | 1 fila, 1 columna |
| Lista con `IN` | `WHERE col IN (SELECT ...)` | N filas, 1 columna |
| Lista con `NOT IN` | `WHERE col NOT IN (SELECT ...)` | N filas, 1 columna |
| Escalar en SELECT | `SELECT (SELECT ...) AS alias` | 1 fila, 1 columna |

### Diferencias clave

| Aspecto | No correlacionada | Correlacionada |
|---|---|---|
| Dependencia | Independiente de la exterior | Referencia a la fila actual de la exterior |
| Ejecuciones | Una sola vez | Una vez por cada fila de la exterior |
| Complejidad | Básica (este curso) | Avanzada (fuera del alcance) |

---

## 9. Tips para el examen

**Errores comunes:**

```sql
-- ❌ Subconsulta con = que devuelve más de un valor → Error en SQL:
SELECT nombre FROM estudiantes
WHERE ciudad = (SELECT ciudad FROM estudiantes);
-- Esta subconsulta devuelve 8 ciudades (una por fila), no 1

-- ✅ Correcto si solo debe devolver una ciudad:
WHERE ciudad = (SELECT ciudad FROM estudiantes WHERE nombre = 'Camila')
-- O usar IN si pueden ser varias:
WHERE ciudad IN (SELECT DISTINCT ciudad FROM estudiantes)
```

```sql
-- ❌ Olvidar los paréntesis alrededor de la subconsulta:
SELECT nombre FROM estudiantes WHERE promedio > SELECT AVG(promedio) FROM estudiantes;
-- Error de sintaxis

-- ✅ Los paréntesis son obligatorios:
SELECT nombre FROM estudiantes WHERE promedio > (SELECT AVG(promedio) FROM estudiantes);
```

**Preguntas frecuentes de examen:**

- *¿Qué es una subconsulta?* → Una sentencia SELECT escrita dentro de otra consulta SQL, entre paréntesis.
- *¿Cuándo usar `=` y cuándo usar `IN` con subconsultas?* → `=` cuando la subconsulta devuelve exactamente 1 valor; `IN` cuando puede devolver múltiples valores.
- *¿La subconsulta se ejecuta antes o después que la consulta exterior?* → **Antes** (en subconsultas no correlacionadas).
- *¿Diferencia entre correlacionada y no correlacionada?* → La no correlacionada es independiente y se ejecuta una sola vez; la correlacionada usa datos de la fila actual de la consulta exterior y se ejecuta una vez por fila.
- *¿Una subconsulta escalar en SELECT puede devolver múltiples filas?* → No. Si devuelve más de una fila, SQL lanza un error.
