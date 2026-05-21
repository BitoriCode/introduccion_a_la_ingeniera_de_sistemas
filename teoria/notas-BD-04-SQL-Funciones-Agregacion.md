# Notas de Estudio — Módulo 4: Funciones de Agregación, GROUP BY y HAVING

> **Objetivo:** Al terminar de leer estas notas, podrás usar las funciones COUNT, SUM, AVG, MAX y MIN; agrupar resultados con GROUP BY; filtrar grupos con HAVING; y distinguir cuándo usar WHERE vs HAVING.

---

## Tabla de práctica

Usamos la tabla `estudiantes` ampliada con un estudiante que tiene promedio `NULL`:

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

Mateo (fila 9) está inscrito pero **no tiene promedio registrado**. Su `NULL` afecta a algunas funciones.

---

## 1. Funciones de agregación

Las funciones de agregación toman **un conjunto de filas** y devuelven **un único valor** de resumen.

### COUNT — contar filas

```sql
-- Total de estudiantes (cuenta todas las filas):
SELECT COUNT(*) AS total_estudiantes
FROM estudiantes;
```
→ `9`

```sql
-- Estudiantes que tienen promedio registrado (ignora NULL):
SELECT COUNT(promedio) AS con_promedio
FROM estudiantes;
```
→ `8` (Mateo tiene NULL y no se cuenta)

> **Diferencia clave:**
> - `COUNT(*)` → cuenta todas las filas, incluyendo las que tienen `NULL` en alguna columna.
> - `COUNT(columna)` → cuenta solo las filas donde esa columna **no es `NULL`**.

---

### SUM — suma

```sql
-- Suma de todos los promedios (ignora NULLs automáticamente):
SELECT SUM(promedio) AS suma_promedios
FROM estudiantes;
```
→ `33.9`

---

### AVG — promedio aritmético

```sql
-- Promedio general de todos los estudiantes:
SELECT AVG(promedio) AS promedio_general
FROM estudiantes;
```
→ `4.2375`

> `AVG` ignora los `NULL`. Divide la suma entre el **número de filas no nulas** (8, no 9). Mateo no cuenta ni en el numerador ni en el denominador.

---

### MAX — valor máximo

```sql
SELECT MAX(promedio) AS mejor_promedio
FROM estudiantes;
```
→ `4.8` (Juan)

---

### MIN — valor mínimo

```sql
SELECT MIN(promedio) AS menor_promedio
FROM estudiantes;
```
→ `2.9` (Sebastián)

---

### Varias funciones en la misma consulta

```sql
SELECT 
    COUNT(*)          AS total,
    COUNT(promedio)   AS con_promedio,
    AVG(promedio)     AS promedio_gral,
    MAX(promedio)     AS mayor,
    MIN(promedio)     AS menor,
    SUM(promedio)     AS suma
FROM estudiantes;
```

| total | con_promedio | promedio_gral | mayor | menor | suma |
|---|---|---|---|---|---|
| 9 | 8 | 4.2375 | 4.8 | 2.9 | 33.9 |

---

### Tabla resumen de funciones

| Función | Qué devuelve | ¿Ignora NULLs? |
|---|---|---|
| `COUNT(*)` | Total de filas | No |
| `COUNT(col)` | Filas donde col no es NULL | Sí |
| `SUM(col)` | Suma de los valores | Sí |
| `AVG(col)` | Media aritmética | Sí |
| `MAX(col)` | Valor más alto | Sí |
| `MIN(col)` | Valor más bajo | Sí |

---

## 2. Funciones de agregación combinadas con WHERE

`WHERE` se aplica **antes** del cálculo. Las funciones operan sobre el subconjunto de filas que pasan el filtro.

```sql
-- ¿Cuántos estudiantes hay en el semestre 5?
SELECT COUNT(*) AS en_semestre_5
FROM estudiantes
WHERE semestre = 5;
```
→ `3`

```sql
-- Promedio de los estudiantes de Bogotá:
SELECT AVG(promedio) AS promedio_bogota
FROM estudiantes
WHERE ciudad = 'Bogotá';
```
→ `4.0`  *(Camila 4.2 + Valentina 4.7 + Felipe 3.1 = 12.0 / 3 = 4.0. Mateo no tiene promedio, no afecta AVG)*

```sql
-- Mejor promedio entre los del semestre 3:
SELECT MAX(promedio) AS mejor_semestre_3
FROM estudiantes
WHERE semestre = 3;
```
→ `4.2` (Camila)

---

## 3. GROUP BY — agrupar resultados

`GROUP BY` divide las filas en **grupos** según los valores de una columna, y aplica la función de agregación **a cada grupo por separado**.

```sql
SELECT columna_de_grupo, FUNCION(columna)
FROM tabla
GROUP BY columna_de_grupo;
```

### Ejemplo: estudiantes por ciudad

```sql
SELECT ciudad, COUNT(*) AS cantidad
FROM estudiantes
GROUP BY ciudad
ORDER BY cantidad DESC;
```

| ciudad | cantidad |
|---|---|
| Bogotá | 4 |
| Medellín | 2 |
| Cali | 2 |
| Barranquilla | 1 |

SQL divide la tabla en 4 grupos (uno por cada ciudad distinta) y aplica `COUNT(*)` a cada uno.

---

### Ejemplo: promedio y cantidad por semestre

```sql
SELECT semestre, COUNT(*) AS estudiantes, AVG(promedio) AS promedio_semestre
FROM estudiantes
GROUP BY semestre
ORDER BY semestre;
```

| semestre | estudiantes | promedio_semestre |
|---|---|---|
| 1 | 2 | 4.3 |
| 2 | 1 | 3.1 |
| 3 | 3 | 3.55 |
| 5 | 3 | 4.366... |

> Semestre 3 tiene 3 estudiantes pero Mateo tiene NULL — `AVG` usa solo los valores no nulos (Camila 4.2 y Sebastián 2.9), ignorando a Mateo.

---

### Ejemplo: mejor y peor promedio por ciudad

```sql
SELECT ciudad, MAX(promedio) AS mejor, MIN(promedio) AS peor
FROM estudiantes
GROUP BY ciudad
ORDER BY mejor DESC;
```

| ciudad | mejor | peor |
|---|---|---|
| Cali | 4.8 | 2.9 |
| Bogotá | 4.7 | 3.1 |
| Medellín | 4.5 | 3.8 |
| Barranquilla | 3.9 | 3.9 |

---

### GROUP BY con múltiples columnas

```sql
-- Agrupar por ciudad Y semestre:
SELECT ciudad, semestre, COUNT(*) AS cantidad
FROM estudiantes
GROUP BY ciudad, semestre
ORDER BY ciudad, semestre;
```

Crea un grupo por cada combinación única de (ciudad, semestre).

---

### La regla de oro de GROUP BY

> Cuando usas `GROUP BY`, **solo pueden aparecer en el `SELECT`**:
> - Las columnas que están en el `GROUP BY`
> - Funciones de agregación (`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`)

```sql
-- ❌ INCORRECTO — nombre no está en GROUP BY:
SELECT ciudad, nombre, COUNT(*)
FROM estudiantes
GROUP BY ciudad;
-- Error: si hay 4 estudiantes en Bogotá, ¿cuál nombre mostrarías?

-- ✅ CORRECTO:
SELECT ciudad, COUNT(*)
FROM estudiantes
GROUP BY ciudad;
```

---

## 4. HAVING — filtrar grupos

`HAVING` filtra los resultados **después de agrupar**. Se aplica a los grupos, no a las filas individuales.

```sql
SELECT columna_de_grupo, FUNCION(columna)
FROM tabla
GROUP BY columna_de_grupo
HAVING condición_sobre_el_grupo;
```

### Ejemplo: ciudades con más de 1 estudiante

```sql
SELECT ciudad, COUNT(*) AS cantidad
FROM estudiantes
GROUP BY ciudad
HAVING COUNT(*) > 1;
```

| ciudad | cantidad |
|---|---|
| Bogotá | 4 |
| Medellín | 2 |
| Cali | 2 |

Barranquilla desaparece — solo tiene 1 estudiante y no supera el filtro.

---

### Ejemplo: semestres con promedio grupal mayor a 4.0

```sql
SELECT semestre, AVG(promedio) AS promedio_semestre
FROM estudiantes
GROUP BY semestre
HAVING AVG(promedio) > 4.0
ORDER BY promedio_semestre DESC;
```

| semestre | promedio_semestre |
|---|---|
| 5 | 4.366... |
| 1 | 4.3 |

Los semestres 2 y 3 no aparecen porque su promedio grupal es <= 4.0.

---

## 5. WHERE vs HAVING — la diferencia crítica

Esta es **la confusión más común** del módulo. La clave es entender en qué momento del procesamiento actúa cada uno:

| | `WHERE` | `HAVING` |
|---|---|---|
| **Actúa sobre** | Filas individuales | Grupos (resultado de GROUP BY) |
| **Cuándo se ejecuta** | Antes de agrupar | Después de agrupar |
| **Puede usar** | Columnas normales | Funciones de agregación |
| **Puede usar funciones de agregación** | ❌ No | ✅ Sí |

### Orden de ejecución de una consulta completa

```
1. FROM      → se accede a la tabla completa
2. WHERE     → se filtran las filas individuales
3. GROUP BY  → se agrupan las filas que pasaron el WHERE
4. HAVING    → se filtran los grupos resultantes
5. SELECT    → se calculan y proyectan las columnas
6. ORDER BY  → se ordena el resultado
7. LIMIT     → se recorta la cantidad de filas devueltas
```

### Ejemplo comparativo

**Pregunta A:** "¿Cuál es el promedio por ciudad, *considerando solo estudiantes con promedio >= 3.5*?"

```sql
-- WHERE filtra ANTES de agrupar — Sebastián (2.9) y Felipe (3.1) quedan fuera
SELECT ciudad, AVG(promedio) AS promedio_ciudad
FROM estudiantes
WHERE promedio >= 3.5
GROUP BY ciudad;
-- Promedio de Bogotá: (4.2 + 4.7) / 2 = 4.45 (sin Felipe ni Mateo)
```

**Pregunta B:** "¿Cuáles ciudades tienen *promedio grupal* >= 3.5?"

```sql
-- HAVING filtra DESPUÉS de agrupar — Sebastián y Felipe SÍ participan en el promedio de su ciudad
SELECT ciudad, AVG(promedio) AS promedio_ciudad
FROM estudiantes
GROUP BY ciudad
HAVING AVG(promedio) >= 3.5;
-- Promedio de Bogotá: (4.2 + 4.7 + 3.1) / 3 = 4.0 (Felipe participa)
```

Son preguntas **completamente diferentes** — leer cuidadosamente el enunciado.

---

## 6. Consulta completa con todas las cláusulas

```sql
SELECT   ciudad, COUNT(*) AS cantidad, ROUND(AVG(promedio), 2) AS prom
FROM     estudiantes
WHERE    semestre >= 2          -- solo estudiantes de semestre 2 en adelante
GROUP BY ciudad                 -- agrupar por ciudad
HAVING   COUNT(*) > 1           -- solo ciudades con más de 1 estudiante (post-filtro)
ORDER BY prom DESC              -- de mayor a menor promedio
LIMIT    3;                     -- máximo 3 ciudades
```

Paso a paso:
1. `FROM estudiantes` — accede a toda la tabla
2. `WHERE semestre >= 2` — descarta Valentina (s.1) y Laura (s.1)
3. `GROUP BY ciudad` — agrupa los 7 restantes por ciudad
4. `HAVING COUNT(*) > 1` — descarta ciudades con 1 solo representante post-filtro
5. `SELECT ...` — calcula los valores por grupo
6. `ORDER BY prom DESC` — ordena
7. `LIMIT 3` — devuelve máximo 3 filas

---

## 7. Resumen rápido (cheatsheet)

### Funciones de agregación

```sql
COUNT(*)       -- total de filas
COUNT(col)     -- filas donde col no es NULL
SUM(col)       -- suma de valores
AVG(col)       -- promedio (ignora NULL)
MAX(col)       -- valor más alto
MIN(col)       -- valor más bajo
ROUND(val, n)  -- redondea a n decimales (no es de agregación, pero útil)
```

### Estructura con GROUP BY y HAVING

```sql
SELECT columna_grupo, FUNCION(col)
FROM tabla
[WHERE filtro_filas]
GROUP BY columna_grupo
[HAVING filtro_grupos]
[ORDER BY col]
[LIMIT n];
```

### Reglas que no se pueden violar

| Regla | Descripción |
|---|---|
| En SELECT con GROUP BY | Solo columnas del GROUP BY + funciones de agregación |
| WHERE no puede usar funciones | `WHERE AVG(promedio) > 4` → Error |
| HAVING sí puede usar funciones | `HAVING AVG(promedio) > 4` → Correcto |
| Orden de cláusulas | WHERE antes de GROUP BY, HAVING después |

---

## 8. Tips para el examen

**Errores comunes:**

```sql
-- ❌ WHERE con función de agregación:
SELECT ciudad, AVG(promedio)
FROM estudiantes
WHERE AVG(promedio) > 4.0      -- ERROR: no se puede usar función en WHERE
GROUP BY ciudad;

-- ✅ Correcto: usar HAVING
SELECT ciudad, AVG(promedio)
FROM estudiantes
GROUP BY ciudad
HAVING AVG(promedio) > 4.0;
```

```sql
-- ❌ SELECT con columna no agrupada:
SELECT ciudad, nombre, COUNT(*)
FROM estudiantes
GROUP BY ciudad;               -- ERROR: nombre no está en GROUP BY

-- ✅ Correcto:
SELECT ciudad, COUNT(*)
FROM estudiantes
GROUP BY ciudad;
```

**Preguntas frecuentes de examen:**

- *¿Diferencia entre `COUNT(*)` y `COUNT(promedio)`?* → `COUNT(*)` cuenta todas las filas; `COUNT(promedio)` cuenta solo las que no tienen NULL en esa columna.
- *¿Para qué sirve `HAVING`?* → Para filtrar grupos después de aplicar `GROUP BY`.
- *¿Puedo usar `WHERE` para filtrar por `AVG`?* → **No**. `AVG` es una función de agregación y solo se puede usar en `HAVING` o en el `SELECT`.
- *¿En qué orden se ejecutan las cláusulas?* → FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT.
- *¿Cuándo usar WHERE y cuándo HAVING?* → WHERE filtra filas individuales antes de agrupar; HAVING filtra grupos después de agrupar.
