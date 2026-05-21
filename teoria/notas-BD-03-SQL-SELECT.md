# Notas de Estudio — Módulo 3: Consultas SQL con SELECT

> **Objetivo:** Al terminar de leer estas notas, podrás escribir consultas SQL completas usando SELECT, WHERE, operadores lógicos, BETWEEN, IN, LIKE, ORDER BY, LIMIT, DISTINCT y expresiones calculadas.

---

## Tabla de práctica

Todas las consultas de este módulo usan la tabla `estudiantes`:

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

---

## 1. SELECT y FROM — la consulta básica

`SELECT` indica **qué columnas** mostrar. `FROM` indica **de qué tabla** traer los datos.

```sql
-- Estructura mínima:
SELECT columna1, columna2
FROM nombre_tabla;
```

```sql
-- Seleccionar columnas específicas:
SELECT nombre, apellido
FROM estudiantes;
```

| nombre | apellido |
|---|---|
| Camila | Rodríguez |
| Andrés | Martínez |
| ... | ... |

```sql
-- Seleccionar TODAS las columnas con asterisco:
SELECT *
FROM estudiantes;
```

> **Regla:** El punto y coma `;` marca el final de cada sentencia SQL. SQL no distingue mayúsculas/minúsculas en las palabras clave (`SELECT` = `select` = `Select`). Por convención: palabras clave en **MAYÚSCULAS**, nombres de tablas/columnas en **minúsculas**.

---

## 2. Aliases con AS

`AS` permite cambiar el nombre que aparece en el encabezado del resultado. No modifica la tabla — solo cambia la presentación.

```sql
SELECT nombre AS "Nombre completo", promedio AS "Nota acumulada"
FROM estudiantes;
```

| Nombre completo | Nota acumulada |
|---|---|
| Camila | 4.2 |
| Andrés | 3.8 |

```sql
-- También se puede usar AS para columnas calculadas:
SELECT nombre, promedio * 20 AS "Promedio sobre 100"
FROM estudiantes;
```

---

## 3. WHERE — filtrar filas

`WHERE` aplica una condición. Solo se devuelven las filas donde la condición es `TRUE`.

```sql
SELECT columnas
FROM tabla
WHERE condición;
```

### Operadores de comparación

| Operador | Significado | Ejemplo |
|---|---|---|
| `=` | Igual a | `semestre = 3` |
| `<>` o `!=` | Diferente de | `ciudad <> 'Bogotá'` |
| `>` | Mayor que | `promedio > 4.0` |
| `<` | Menor que | `promedio < 3.0` |
| `>=` | Mayor o igual que | `semestre >= 3` |
| `<=` | Menor o igual que | `promedio <= 3.5` |

```sql
-- Estudiantes del semestre 3:
SELECT nombre, semestre FROM estudiantes WHERE semestre = 3;
```
→ Camila (3), Sebastián (3)

```sql
-- Estudiantes con promedio mayor a 4.0:
SELECT nombre, promedio FROM estudiantes WHERE promedio > 4.0;
```
→ Camila (4.2), Valentina (4.7), Daniela (4.5), Juan (4.8)

```sql
-- Estudiantes de Bogotá:
SELECT nombre, ciudad FROM estudiantes WHERE ciudad = 'Bogotá';
```

> **Importante:** Los textos (strings) van entre **comillas simples** `' '`. Los números van **sin comillas**. `WHERE ciudad = 'Bogotá'` es correcto; `WHERE semestre = '3'` funciona pero es mala práctica.

---

## 4. Operadores lógicos: AND, OR, NOT

### AND — deben cumplirse TODAS las condiciones

```sql
-- Estudiantes de Bogotá Y en semestre 3:
SELECT nombre, ciudad, semestre
FROM estudiantes
WHERE ciudad = 'Bogotá' AND semestre = 3;
```
→ Solo Camila (es la única de Bogotá en semestre 3)

### OR — debe cumplirse AL MENOS UNA condición

```sql
-- Estudiantes de Cali O de Barranquilla:
SELECT nombre, ciudad
FROM estudiantes
WHERE ciudad = 'Cali' OR ciudad = 'Barranquilla';
```
→ Sebastián (Cali), Laura (Barranquilla), Juan (Cali)

### NOT — niega la condición

```sql
-- Estudiantes que NO son de Bogotá:
SELECT nombre, ciudad
FROM estudiantes
WHERE NOT ciudad = 'Bogotá';
-- Equivalente a: WHERE ciudad <> 'Bogotá'
```

### Combinando AND y OR — usar paréntesis

Sin paréntesis, `AND` tiene mayor precedencia que `OR` (como la multiplicación sobre la suma).

```sql
-- ⚠️ Sin paréntesis — puede dar resultados inesperados:
WHERE ciudad = 'Bogotá' OR ciudad = 'Medellín' AND promedio >= 4.0
-- Se evalúa como: ciudad = 'Bogotá' OR (ciudad = 'Medellín' AND promedio >= 4.0)
-- → Trae todos los de Bogotá (sin importar promedio) + los de Medellín con promedio >= 4.0

-- ✅ Con paréntesis — intención clara:
WHERE (ciudad = 'Bogotá' OR ciudad = 'Medellín') AND promedio >= 4.0
-- → Solo los de Bogotá o Medellín que además tengan promedio >= 4.0
```

---

## 5. BETWEEN — rangos

`BETWEEN` filtra por un rango **inclusivo** en ambos extremos (equivale a `>= AND <=`).

```sql
-- Estudiantes con promedio entre 3.5 y 4.5 (ambos extremos incluidos):
SELECT nombre, promedio
FROM estudiantes
WHERE promedio BETWEEN 3.5 AND 4.5;
```
→ Camila (4.2), Andrés (3.8), Daniela (4.5), Laura (3.9)

```sql
-- Equivalente con >= y <=:
WHERE promedio >= 3.5 AND promedio <= 4.5
```

```sql
-- NOT BETWEEN — fuera del rango:
SELECT nombre, promedio FROM estudiantes WHERE promedio NOT BETWEEN 3.5 AND 4.5;
```
→ Valentina (4.7), Sebastián (2.9), Juan (4.8)

> **BETWEEN también funciona con texto y fechas:**
> ```sql
> WHERE ciudad BETWEEN 'A' AND 'M'   -- ciudades cuyo nombre empieza entre A y M (alfabético)
> WHERE fecha_ingreso BETWEEN '2025-01-01' AND '2025-12-31'
> ```

---

## 6. IN — lista de valores

`IN` es un atajo para múltiples condiciones `OR` sobre la misma columna.

```sql
-- Sin IN (incómodo y propenso a errores):
WHERE ciudad = 'Bogotá' OR ciudad = 'Cali' OR ciudad = 'Medellín'

-- Con IN (limpio y legible):
SELECT nombre, ciudad
FROM estudiantes
WHERE ciudad IN ('Bogotá', 'Cali', 'Medellín');
```
→ Camila, Valentina, Felipe (Bogotá), Sebastián, Juan (Cali), Andrés, Daniela (Medellín)

```sql
-- NOT IN — todos menos los de la lista:
SELECT nombre, ciudad
FROM estudiantes
WHERE ciudad NOT IN ('Bogotá', 'Medellín');
```
→ Sebastián (Cali), Laura (Barranquilla), Juan (Cali)

> **Trampa con NULL y NOT IN:** Si la lista incluye `NULL`, `NOT IN` puede no devolver lo esperado. Evitar `NULL` dentro de una lista `IN`.

---

## 7. LIKE — patrones de texto

`LIKE` busca textos que coincidan con un patrón. Usa dos comodines especiales:

| Comodín | Significado |
|---|---|
| `%` | Cero o más caracteres cualquiera |
| `_` | Exactamente un carácter cualquiera |

```sql
-- Nombres que empiezan con 'Ca':
SELECT nombre FROM estudiantes WHERE nombre LIKE 'Ca%';
-- → Camila

-- Nombres que terminan en 'a':
SELECT nombre FROM estudiantes WHERE nombre LIKE '%a';
-- → Camila, Valentina, Daniela, Laura

-- Nombres que contienen 'an' en cualquier posición:
SELECT nombre FROM estudiantes WHERE nombre LIKE '%an%';
-- → Valentina, Sebastián

-- Nombres de exactamente 4 caracteres:
SELECT nombre FROM estudiantes WHERE nombre LIKE '____';  -- 4 guiones bajos
-- → Juan

-- Ciudades que empiezan con 'B' y tienen cualquier cosa después:
SELECT nombre, ciudad FROM estudiantes WHERE ciudad LIKE 'B%';
-- → Bogotá, Barranquilla
```

```sql
-- NOT LIKE — que NO coincidan con el patrón:
SELECT nombre FROM estudiantes WHERE nombre NOT LIKE '%a';
-- → Andrés, Sebastián, Felipe, Juan
```

> **Sensibilidad a mayúsculas:** En SQLite, `LIKE` es insensible a mayúsculas para letras ASCII. `LIKE 'camila'` encuentra `'Camila'`. Para acentos y ñ, el comportamiento puede variar.

---

## 8. IS NULL / IS NOT NULL

`NULL` significa "valor desconocido o ausente". **No se puede comparar con `=`** — se debe usar `IS NULL` o `IS NOT NULL`.

```sql
-- ❌ Esto NUNCA devuelve resultados (NULL no es igual a nada, ni a sí mismo):
SELECT * FROM estudiantes WHERE promedio = NULL;

-- ✅ Correcto:
SELECT nombre FROM estudiantes WHERE promedio IS NULL;
SELECT nombre FROM estudiantes WHERE promedio IS NOT NULL;
```

---

## 9. ORDER BY — ordenar resultados

`ORDER BY` ordena el resultado. Por defecto es ascendente (`ASC`).

```sql
-- Ordenar por promedio de mayor a menor:
SELECT nombre, promedio
FROM estudiantes
ORDER BY promedio DESC;
```

| nombre | promedio |
|---|---|
| Juan | 4.8 |
| Valentina | 4.7 |
| Daniela | 4.5 |
| Camila | 4.2 |
| Laura | 3.9 |
| Andrés | 3.8 |
| Felipe | 3.1 |
| Sebastián | 2.9 |

```sql
-- Ordenar por múltiples columnas: primero por ciudad, luego por promedio:
SELECT nombre, ciudad, promedio
FROM estudiantes
ORDER BY ciudad ASC, promedio DESC;
```

Los de Barranquilla primero, luego Bogotá (ordenados por promedio), luego Cali, luego Medellín.

---

## 10. LIMIT y OFFSET — paginación

`LIMIT` restringe cuántas filas devuelve la consulta.

```sql
-- Los 3 estudiantes con mejor promedio:
SELECT nombre, promedio
FROM estudiantes
ORDER BY promedio DESC
LIMIT 3;
```
→ Juan (4.8), Valentina (4.7), Daniela (4.5)

```sql
-- OFFSET: saltar las primeras N filas (útil para paginación):
-- Página 2 de resultados (posiciones 4-6):
SELECT nombre, promedio
FROM estudiantes
ORDER BY promedio DESC
LIMIT 3 OFFSET 3;
```
→ Camila (4.2), Laura (3.9), Andrés (3.8)

---

## 11. DISTINCT — eliminar duplicados

`DISTINCT` elimina los valores repetidos del resultado.

```sql
-- ¿En qué ciudades hay estudiantes? (sin repetir):
SELECT DISTINCT ciudad
FROM estudiantes;
```
→ Bogotá, Medellín, Cali, Barranquilla

```sql
-- ¿Qué semestres están activos?
SELECT DISTINCT semestre
FROM estudiantes
ORDER BY semestre;
```
→ 1, 2, 3, 5

---

## 12. Expresiones calculadas en SELECT

Se pueden hacer operaciones matemáticas directamente en el `SELECT`:

```sql
-- Convertir promedio de escala 0-5 a escala 0-100:
SELECT nombre, promedio, ROUND(promedio * 20, 1) AS promedio_100
FROM estudiantes
ORDER BY promedio DESC;
```

| nombre | promedio | promedio_100 |
|---|---|---|
| Juan | 4.8 | 96.0 |
| Valentina | 4.7 | 94.0 |
| Daniela | 4.5 | 90.0 |

---

## 13. Orden correcto de las cláusulas

Las cláusulas de una consulta `SELECT` **deben ir en este orden** (o SQL dará error de sintaxis):

```sql
SELECT   columnas o expresiones        -- 1. qué mostrar
FROM     tabla                         -- 2. de dónde
WHERE    condición de filas            -- 3. qué filas incluir
ORDER BY columna ASC|DESC              -- 4. en qué orden
LIMIT    número                        -- 5. cuántas filas máximo
OFFSET   número                        -- 6. desde qué posición
```

**Ejemplo completo:**

```sql
SELECT nombre, ciudad, promedio
FROM estudiantes
WHERE promedio IS NOT NULL
ORDER BY promedio DESC
LIMIT 5;
```

---

## 14. Resumen rápido (cheatsheet)

### Cláusulas fundamentales

| Cláusula | Propósito | Ejemplo |
|---|---|---|
| `SELECT col` | Elegir columnas | `SELECT nombre, promedio` |
| `SELECT *` | Todas las columnas | `SELECT *` |
| `FROM tabla` | Origen de los datos | `FROM estudiantes` |
| `WHERE cond` | Filtrar filas | `WHERE promedio > 4.0` |
| `ORDER BY col DESC` | Ordenar resultado | `ORDER BY promedio DESC` |
| `LIMIT n` | Limitar cantidad | `LIMIT 10` |
| `OFFSET n` | Saltar primeras n filas | `OFFSET 5` |
| `DISTINCT` | Sin duplicados | `SELECT DISTINCT ciudad` |
| `AS alias` | Renombrar columna | `promedio AS "Nota"` |

### Operadores para WHERE

| Tipo | Operadores |
|---|---|
| Comparación | `=`, `<>`, `!=`, `>`, `<`, `>=`, `<=` |
| Rango | `BETWEEN valor1 AND valor2` |
| Lista | `IN (val1, val2, ...)` / `NOT IN (...)` |
| Patrón texto | `LIKE 'patrón%'` / `NOT LIKE ...` |
| Nulo | `IS NULL` / `IS NOT NULL` |
| Lógicos | `AND`, `OR`, `NOT` |

### Comodines de LIKE

| Comodín | Matches | Ejemplo |
|---|---|---|
| `%` | Cero o más caracteres | `'Ca%'` → Camila, Carlos, Ca |
| `_` | Exactamente un carácter | `'Ca_'` → Cat, Cal (3 letras que empiecen con Ca) |

---

## 15. Tips para el examen

**Errores comunes de sintaxis:**

```sql
-- ❌ Orden incorrecto:
FROM estudiantes SELECT nombre WHERE semestre = 3;

-- ✅ Correcto:
SELECT nombre FROM estudiantes WHERE semestre = 3;
```

```sql
-- ❌ Texto sin comillas:
WHERE ciudad = Bogotá        -- Error

-- ✅ Correcto:
WHERE ciudad = 'Bogotá'
```

```sql
-- ❌ Comparar NULL con =:
WHERE promedio = NULL        -- NUNCA devuelve resultados

-- ✅ Correcto:
WHERE promedio IS NULL
```

```sql
-- ❌ BETWEEN con el mayor primero:
WHERE promedio BETWEEN 4.5 AND 3.5    -- No devuelve nada

-- ✅ El menor primero:
WHERE promedio BETWEEN 3.5 AND 4.5
```

**Preguntas frecuentes de examen:**

- *¿Qué diferencia hay entre `=` y `LIKE`?* → `=` es igualdad exacta; `LIKE` permite patrones con comodines (`%`, `_`).
- *¿`BETWEEN 3 AND 5` incluye los extremos?* → **Sí**, es equivalente a `>= 3 AND <= 5`.
- *¿Para qué sirve `DISTINCT`?* → Para eliminar filas duplicadas del resultado.
- *¿Cuál es el orden correcto de cláusulas?* → SELECT → FROM → WHERE → ORDER BY → LIMIT → OFFSET.
- *¿Cómo se ordena de mayor a menor?* → `ORDER BY columna DESC`.
