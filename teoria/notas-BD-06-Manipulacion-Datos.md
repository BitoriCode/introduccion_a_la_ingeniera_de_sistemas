# Notas de Estudio — Módulo 6: Manipulación de Datos (INSERT, UPDATE, DELETE)

> **Objetivo:** Al terminar de leer estas notas, podrás insertar nuevos registros con INSERT, modificar datos existentes con UPDATE, eliminar registros con DELETE, y aplicar las buenas prácticas de seguridad para no perder datos accidentalmente.

---

## Tabla de práctica

Usamos la misma tabla `estudiantes` del curso:

```sql
CREATE TABLE estudiantes (
    id_estudiante INTEGER  PRIMARY KEY AUTOINCREMENT,
    nombre        TEXT     NOT NULL,
    apellido      TEXT     NOT NULL,
    ciudad        TEXT     NOT NULL,
    semestre      INTEGER  NOT NULL,
    promedio      REAL
);
```

Estado inicial de la tabla:

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

## 1. INSERT INTO — insertar registros

`INSERT INTO` agrega una o más filas nuevas a una tabla.

### Sintaxis básica — especificando columnas

```sql
INSERT INTO nombre_tabla (columna1, columna2, columna3)
VALUES (valor1, valor2, valor3);
```

Esta es la forma **recomendada**: se declaran explícitamente las columnas.

```sql
-- Insertar un nuevo estudiante:
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre, promedio)
VALUES ('María', 'Gómez', 'Bucaramanga', 1, 3.7);
```

Resultado: se agrega la fila con `id_estudiante = 9` (AUTO_INCREMENT lo asigna automáticamente).

---

### INSERT sin listar columnas

Si se omiten los nombres de las columnas, **los valores deben proporcionarse en el mismo orden** que están definidas en la tabla. El `id` autoincremental se omite o se pone `NULL`:

```sql
-- Equivalente al INSERT anterior (id=NULL para que se autogenere):
INSERT INTO estudiantes
VALUES (NULL, 'María', 'Gómez', 'Bucaramanga', 1, 3.7);
```

> **Desventaja:** Si alguien agrega o reordena columnas en la tabla, este INSERT puede insertar datos en columnas incorrectas. Es mejor siempre listar las columnas.

---

### INSERT sin especificar todas las columnas

Se pueden omitir columnas que tienen `DEFAULT` o permiten `NULL`:

```sql
-- promedio es REAL (puede ser NULL) → se puede omitir:
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre)
VALUES ('Carlos', 'Reyes', 'Manizales', 2);
-- promedio quedará como NULL hasta que se registre
```

---

### INSERT múltiple — varios registros en un solo INSERT

```sql
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre, promedio)
VALUES 
    ('Paola',   'Vargas',  'Bogotá',    4, 4.0),
    ('Tomás',   'Nieto',   'Medellín',  3, 3.5),
    ('Isabela', 'Ramos',   'Cali',      2, 4.3),
    ('Julián',  'Moreno',  'Bogotá',    5, 3.9);
```

Se insertan 4 filas en una sola operación. Es más eficiente que hacer cuatro INSERTs separados.

---

### Reglas que aplican al hacer INSERT

Si la tabla tiene restricciones, el INSERT fallará si las viola:

```sql
-- ❌ Falla: nombre tiene NOT NULL
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre)
VALUES (NULL, 'García', 'Cali', 1);

-- ❌ Falla: id_estudiante ya existe (violación de PRIMARY KEY)
INSERT INTO estudiantes (id_estudiante, nombre, apellido, ciudad, semestre)
VALUES (1, 'Otra', 'Persona', 'Bogotá', 1);

-- ❌ Falla: si hay un CHECK (promedio BETWEEN 0 AND 5)
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre, promedio)
VALUES ('Test', 'Test', 'Bogotá', 1, 6.0);
```

---

## 2. UPDATE — modificar registros existentes

`UPDATE` modifica los valores de una o más columnas en las filas que cumplan la condición del `WHERE`.

```sql
UPDATE nombre_tabla
SET columna1 = nuevo_valor1,
    columna2 = nuevo_valor2
WHERE condición;
```

### Ejemplo 1: Actualizar el promedio de un estudiante

```sql
UPDATE estudiantes
SET promedio = 4.1
WHERE id_estudiante = 2;   -- Andrés Martínez
```

Antes: Andrés tenía `promedio = 3.8`. Después: `promedio = 4.1`.

---

### Ejemplo 2: Actualizar la ciudad de Laura

```sql
UPDATE estudiantes
SET ciudad = 'Cartagena'
WHERE nombre = 'Laura' AND apellido = 'Sánchez';
```

---

### Ejemplo 3: Actualizar múltiples columnas a la vez

```sql
UPDATE estudiantes
SET ciudad = 'Medellín',
    semestre = 4
WHERE id_estudiante = 4;   -- Sebastián García
```

---

### Ejemplo 4: UPDATE con expresión calculada

```sql
-- Subir el promedio de todos los de semestre 1 en 0.1 puntos:
UPDATE estudiantes
SET promedio = promedio + 0.1
WHERE semestre = 1;
```

El nuevo valor puede referenciar el valor actual de la columna.

---

### ⚠️ EL ERROR MÁS GRAVE: UPDATE sin WHERE

```sql
-- ❌ PELIGRO EXTREMO — actualiza TODAS las filas de la tabla:
UPDATE estudiantes
SET ciudad = 'Bogotá';
-- Después de esto, TODOS los estudiantes quedan con ciudad = 'Bogotá'
```

**Regla de oro: NUNCA hacer UPDATE sin WHERE** a menos que intencionalmente se quieran modificar todas las filas (caso muy raro).

> **Buena práctica antes de un UPDATE:** Hacer primero el SELECT con la misma condición para verificar qué filas se van a afectar:
> ```sql
> -- Paso 1: verificar qué filas cambiarán
> SELECT * FROM estudiantes WHERE semestre = 1;
> -- → Valentina y Laura ✓
>
> -- Paso 2: ejecutar el UPDATE con la misma condición
> UPDATE estudiantes SET promedio = promedio + 0.1 WHERE semestre = 1;
> ```

---

## 3. DELETE — eliminar registros

`DELETE FROM` elimina las filas que cumplan la condición del `WHERE`.

```sql
DELETE FROM nombre_tabla
WHERE condición;
```

### Ejemplo 1: Eliminar un estudiante específico

```sql
DELETE FROM estudiantes
WHERE id_estudiante = 9;
```

La fila con id 9 desaparece de la tabla.

---

### Ejemplo 2: Eliminar por condición

```sql
-- Eliminar todos los estudiantes sin promedio registrado:
DELETE FROM estudiantes
WHERE promedio IS NULL;
```

---

### Ejemplo 3: Eliminar varios registros por lista

```sql
-- Eliminar estudiantes de los semestres 1 y 2:
DELETE FROM estudiantes
WHERE semestre IN (1, 2);
```

---

### ⚠️ EL ERROR MÁS GRAVE: DELETE sin WHERE

```sql
-- ❌ PELIGRO EXTREMO — elimina TODAS las filas de la tabla:
DELETE FROM estudiantes;
-- La tabla queda completamente vacía. Los datos se pierden.
```

**Regla de oro: NUNCA hacer DELETE sin WHERE** a menos que se quiera vaciar la tabla intencionalmente.

---

### DELETE vs DROP TABLE

| Operación | Qué hace |
|---|---|
| `DELETE FROM tabla WHERE ...` | Elimina filas específicas. La tabla sigue existiendo. |
| `DELETE FROM tabla` | Elimina **todas** las filas. La tabla sigue existiendo (vacía). |
| `DROP TABLE tabla` | Elimina la tabla **completamente** (estructura + datos). |

```sql
-- Tabla sigue existiendo pero vacía:
DELETE FROM estudiantes;

-- La tabla deja de existir:
DROP TABLE estudiantes;
```

---

## 4. Introducción a transacciones

Una **transacción** es un conjunto de operaciones que se ejecutan como una unidad: o **todas se completan**, o **ninguna se aplica**. Esto es fundamental para operaciones críticas.

### Las tres operaciones de control

```sql
BEGIN;       -- o BEGIN TRANSACTION — inicia la transacción
COMMIT;      -- confirma todos los cambios (los hace permanentes)
ROLLBACK;    -- cancela todos los cambios (vuelve al estado anterior)
```

### Ejemplo práctico

```sql
BEGIN;

-- Operación 1: insertar nuevo estudiante
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre)
VALUES ('Diego', 'Ospina', 'Cali', 1);

-- Operación 2: actualizar un promedio
UPDATE estudiantes
SET promedio = 4.6
WHERE id_estudiante = 5;

-- Si todo salió bien → confirmar
COMMIT;

-- Si algo falló o nos arrepentimos → cancelar
-- ROLLBACK;
```

Si ejecutamos `ROLLBACK` en lugar de `COMMIT`, ni el INSERT ni el UPDATE se aplicarán — como si no hubieran ocurrido.

### ¿Cuándo usar transacciones?

- Cuando un conjunto de operaciones deben ejecutarse todas o ninguna (p.ej., transferencia bancaria: restar de una cuenta Y sumar a otra).
- Antes de ejecutar UPDATEs o DELETEs masivos arriesgados — si algo sale mal, se hace ROLLBACK.
- En sistemas con múltiples usuarios escribiendo al mismo tiempo.

> **Nota:** SQLite soporta transacciones. En SQLite Browser, cada ejecución es una transacción automática. Para control manual se usa `BEGIN` / `COMMIT` / `ROLLBACK` explícitamente.

---

## 5. Resumen rápido (cheatsheet)

### INSERT

```sql
-- Una fila (con nombres de columnas — recomendado):
INSERT INTO tabla (col1, col2, col3)
VALUES (val1, val2, val3);

-- Múltiples filas:
INSERT INTO tabla (col1, col2)
VALUES (v1a, v2a),
       (v1b, v2b),
       (v1c, v2c);
```

### UPDATE

```sql
-- Siempre con WHERE:
UPDATE tabla
SET col1 = nuevo_valor,
    col2 = otro_valor
WHERE condición;

-- Con expresión calculada:
UPDATE tabla SET precio = precio * 1.10 WHERE categoria = 'Premium';
```

### DELETE

```sql
-- Siempre con WHERE:
DELETE FROM tabla WHERE condición;
```

### Transacciones

```sql
BEGIN;
  -- operaciones aquí
COMMIT;    -- confirmar
-- o ROLLBACK; para cancelar
```

### Las tres diferencias críticas

| Operación | Afecta | La estructura de la tabla |
|---|---|---|
| `DELETE FROM t WHERE c` | Filas específicas | Se mantiene |
| `DELETE FROM t` | Todas las filas | Se mantiene (tabla vacía) |
| `DROP TABLE t` | Toda la tabla | Se elimina |

---

## 6. Flujo de verificación antes de modificar datos

Antes de ejecutar cualquier `UPDATE` o `DELETE`, seguir este proceso:

```
1. SELECT con la misma condición → verificar qué filas se afectan
2. Contar las filas: COUNT(*) → ¿es la cantidad esperada?
3. Ejecutar UPDATE o DELETE
4. SELECT de verificación → confirmar que el cambio fue correcto
```

```sql
-- Ejemplo completo del flujo:

-- Paso 1: ¿qué estudiantes van a cambiar?
SELECT * FROM estudiantes WHERE ciudad = 'Cali';
-- → Sebastián y Juan (2 filas) ✓

-- Paso 2: ejecutar el UPDATE
UPDATE estudiantes
SET ciudad = 'Cali del Valle'
WHERE ciudad = 'Cali';

-- Paso 3: verificar
SELECT * FROM estudiantes WHERE ciudad = 'Cali del Valle';
-- → Sebastián y Juan con la nueva ciudad ✓
```

---

## 7. Tips para el examen

**Errores comunes:**

```sql
-- ❌ UPDATE sin WHERE (desastre):
UPDATE estudiantes SET semestre = 6;
-- → Todos los estudiantes quedan en semestre 6

-- ✅ Siempre especificar a quién afecta:
UPDATE estudiantes SET semestre = 6 WHERE id_estudiante = 8;
```

```sql
-- ❌ DELETE sin WHERE:
DELETE FROM estudiantes;
-- → La tabla queda vacía

-- ✅ Con condición:
DELETE FROM estudiantes WHERE id_estudiante = 4;
```

```sql
-- ❌ INSERT con más valores que columnas:
INSERT INTO estudiantes (nombre, apellido) VALUES ('Ana', 'Torres', 'Bogotá');
-- → Error: demasiados valores

-- ✅ Los valores deben corresponder en cantidad y orden a las columnas listadas:
INSERT INTO estudiantes (nombre, apellido, ciudad, semestre)
VALUES ('Ana', 'Torres', 'Bogotá', 1);
```

**Preguntas frecuentes de examen:**

- *¿Qué hace `DELETE FROM tabla` sin WHERE?* → Elimina **todas** las filas de la tabla (la tabla queda vacía pero sigue existiendo).
- *¿Diferencia entre `DELETE FROM tabla` y `DROP TABLE tabla`?* → `DELETE` elimina los datos pero conserva la estructura; `DROP TABLE` elimina la tabla completamente.
- *¿Se puede hacer `INSERT` de múltiples filas en un solo comando?* → **Sí**, listando múltiples `VALUES (...)` separados por coma.
- *¿Qué hace `ROLLBACK`?* → Cancela todos los cambios hechos dentro de la transacción actual y vuelve al estado anterior al `BEGIN`.
- *¿Por qué es mejor especificar las columnas en un INSERT?* → Para que el código sea resistente a cambios en la estructura de la tabla y quede explícitamente claro qué valor va en qué columna.
