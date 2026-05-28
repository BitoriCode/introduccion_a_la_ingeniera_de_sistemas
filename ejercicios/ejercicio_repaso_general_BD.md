# Repaso para el Examen Final — Bases de Datos con SQL
## Clínica Veterinaria "Patitas Felices"

| | |
|---|---|
| **Temas evaluados** | SELECT · WHERE · ORDER BY · Agregación · GROUP BY · HAVING · Subconsultas · INSERT · UPDATE · DELETE |
| **Modalidad** | Individual |

---

## Contexto

La clínica veterinaria **Patitas Felices** tiene sedes en varias ciudades de Colombia y lleva el registro de todas las consultas médicas atendidas en su base de datos SQLite. La tabla `consultas` almacena la información de cada atención:

| Columna | Tipo | Descripción |
|---|---|---|
| `id_consulta` | INTEGER | Identificador único (PK) |
| `nombre_mascota` | TEXT | Nombre de la mascota |
| `especie` | TEXT | `Perro`, `Gato`, `Conejo`, `Ave`, `Reptil` |
| `raza` | TEXT | Raza de la mascota |
| `edad_anios` | INTEGER | Edad en años |
| `tipo_consulta` | TEXT | `Vacunación`, `Cirugía`, `Control`, `Urgencia`, `Desparasitación` |
| `veterinario` | TEXT | Nombre del veterinario |
| `ciudad` | TEXT | Ciudad de la sede |
| `costo` | REAL | Costo de la consulta en pesos colombianos |
| `duracion_min` | INTEGER | Duración de la consulta en minutos |
| `estado` | TEXT | `completada`, `pendiente`, `cancelada` |

---

## Datos iniciales — ejecuta esto primero en DB Browser / DBeaver

```sql
DROP TABLE IF EXISTS consultas;

CREATE TABLE consultas (
    id_consulta    INTEGER PRIMARY KEY AUTOINCREMENT,
    nombre_mascota TEXT    NOT NULL,
    especie        TEXT    NOT NULL,
    raza           TEXT    NOT NULL,
    edad_anios     INTEGER NOT NULL,
    tipo_consulta  TEXT    NOT NULL,
    veterinario    TEXT    NOT NULL,
    ciudad         TEXT    NOT NULL,
    costo          REAL    NOT NULL,
    duracion_min   INTEGER NOT NULL,
    estado         TEXT    NOT NULL
);

INSERT INTO consultas (nombre_mascota, especie, raza, edad_anios, tipo_consulta, veterinario, ciudad, costo, duracion_min, estado) VALUES
    ('Max',       'Perro',   'Labrador',         3,  'Vacunación',      'Dra. Ramírez',  'Bogotá',       45000,  20, 'completada'),
    ('Luna',      'Gato',    'Siamés',            1,  'Control',         'Dr. Morales',   'Medellín',     35000,  15, 'completada'),
    ('Boni',      'Perro',   'Bulldog',           5,  'Cirugía',         'Dra. Ramírez',  'Bogotá',      320000,  90, 'completada'),
    ('Pelusa',    'Conejo',  'Angora',            2,  'Desparasitación', 'Dr. Vargas',    'Cali',         28000,  10, 'completada'),
    ('Rocky',     'Perro',   'Rottweiler',        4,  'Urgencia',        'Dra. Torres',   'Barranquilla', 150000,  45, 'completada'),
    ('Misi',      'Gato',    'Persa',             6,  'Control',         'Dr. Morales',   'Medellín',     35000,  15, 'cancelada'),
    ('Kiwi',      'Ave',     'Loro',              2,  'Vacunación',      'Dr. Vargas',    'Cali',         55000,  25, 'completada'),
    ('Thor',      'Perro',   'Pastor Alemán',     2,  'Vacunación',      'Dra. Ramírez',  'Bogotá',       45000,  20, 'completada'),
    ('Nala',      'Gato',    'Maine Coon',        3,  'Cirugía',         'Dra. Torres',   'Barranquilla', 280000,  75, 'completada'),
    ('Coco',      'Ave',     'Canario',           1,  'Control',         'Dr. Vargas',    'Cali',         30000,  10, 'completada'),
    ('Rex',       'Perro',   'Dóberman',          7,  'Control',         'Dr. Morales',   'Medellín',     35000,  15, 'completada'),
    ('Lola',      'Perro',   'Poodle',            1,  'Desparasitación', 'Dra. Torres',   'Bogotá',       28000,  10, 'pendiente'),
    ('Simba',     'Gato',    'Bengalí',           4,  'Urgencia',        'Dra. Ramírez',  'Bogotá',      175000,  50, 'completada'),
    ('Pipa',      'Conejo',  'Holland Lop',       1,  'Vacunación',      'Dr. Vargas',    'Cali',         55000,  20, 'completada'),
    ('Bruno',     'Perro',   'Beagle',            3,  'Control',         'Dr. Morales',   'Medellín',     35000,  15, 'completada'),
    ('Yuki',      'Gato',    'Ragdoll',           2,  'Vacunación',      'Dra. Torres',   'Barranquilla', 45000,  20, 'completada'),
    ('Spike',     'Reptil',  'Dragón Barbudo',    3,  'Control',         'Dr. Vargas',    'Cali',         60000,  20, 'completada'),
    ('Toby',      'Perro',   'Golden Retriever',  6,  'Cirugía',         'Dra. Ramírez',  'Bogotá',      350000, 120, 'completada'),
    ('Canela',    'Gato',    'Común Europeo',     5,  'Desparasitación', 'Dr. Morales',   'Medellín',     28000,  10, 'completada'),
    ('Pitu',      'Ave',     'Guacamayo',         4,  'Urgencia',        'Dra. Torres',   'Barranquilla', 140000,  40, 'cancelada');
```

---

## Parte 1 — Consultas SELECT y WHERE (Módulo 3)

> Usa `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `DISTINCT`, `BETWEEN`, `IN`, `LIKE` y columnas calculadas.

**Ejercicio 1.**
Lista el `nombre_mascota`, la `especie` y el `costo` de todas las consultas cuyo estado sea `'completada'`. Ordena los resultados de mayor a menor costo.

---

**Ejercicio 2.**
Muestra el `nombre_mascota`, el `tipo_consulta` y la `ciudad` de las mascotas atendidas en `'Bogotá'` o `'Medellín'`. Usa el operador `IN`.

---

**Ejercicio 3.**
Lista todas las consultas cuyo costo esté entre $30 000 y $100 000 (inclusive). Muestra el `nombre_mascota`, la `especie`, el `tipo_consulta` y el `costo`.

---

**Ejercicio 4.**
Encuentra las mascotas cuyos nombres empiezan con la letra **"B"**. Muestra el `nombre_mascota`, la `raza` y el `veterinario`.

---

**Ejercicio 5.**
Muestra el `nombre_mascota`, la `especie` y el `costo` de todas las consultas. Agrega una columna calculada llamada `costo_con_iva` que sea el costo multiplicado por `1.19`. Ordena por `costo_con_iva` de menor a mayor.

---

**Ejercicio 6.**
¿Cuáles son las especies distintas que existen en la tabla? Usa `DISTINCT`.

---

**Ejercicio 7.**
Muestra las 3 consultas más caras (las de mayor costo). Muestra `nombre_mascota`, `tipo_consulta`, `veterinario` y `costo`.

---

## Parte 2 — Funciones de Agregación, GROUP BY y HAVING (Módulo 4)

> Usa `COUNT`, `SUM`, `AVG`, `MAX`, `MIN`, `GROUP BY` y `HAVING`.

**Ejercicio 8.**
¿Cuántas consultas hay en total en la tabla?

---

**Ejercicio 9.**
¿Cuál es el costo promedio, el costo máximo y el costo mínimo de todas las consultas con estado `'completada'`?

---

**Ejercicio 10.**
Cuenta cuántas consultas hay por cada `especie`. Muestra la `especie` y el total, ordenado de mayor a menor cantidad.

---

**Ejercicio 11.**
Para cada `ciudad`, calcula el costo total (`SUM`) de todas las consultas. Muestra solo las ciudades donde el costo total supere $200 000.

---

**Ejercicio 12.**
Para cada `veterinario`, calcula el promedio de duración (`duracion_min`) de sus consultas. Muestra solo los veterinarios cuyo promedio supere 25 minutos. Ordena de mayor a menor promedio.

---

**Ejercicio 13.**
¿Cuántas consultas hay por `tipo_consulta`? Muestra solo los tipos que tengan **2 o más** consultas completadas (estado = `'completada'`).

---

## Parte 3 — Subconsultas (Módulo 5)

> Usa subconsultas en `WHERE` (con `=` y con `IN`) y en `SELECT`.

**Ejercicio 14.**
Muestra el `nombre_mascota`, la `especie` y el `costo` de las consultas cuyo costo sea **mayor** que el costo promedio de todas las consultas. *(Usa una subconsulta en WHERE.)*

---

**Ejercicio 15.**
Muestra los datos de la consulta más larga (mayor `duracion_min`). Muestra `nombre_mascota`, `tipo_consulta`, `veterinario` y `duracion_min`. *(Usa una subconsulta con MAX.)*

---

**Ejercicio 16.**
Lista el `nombre_mascota` y la `especie` de todas las mascotas que han tenido algún tipo de consulta quirúrgica o de urgencia (tipo_consulta `IN ('Cirugía', 'Urgencia')`). *(Usa una subconsulta con IN.)*

---

**Ejercicio 17.**
Para cada fila de la tabla, muestra el `nombre_mascota`, el `costo` y una columna adicional llamada `diferencia_con_promedio` que indique cuánto se diferencia ese costo del costo promedio general. *(Usa una subconsulta escalar en SELECT.)*

---

## Parte 4 — Manipulación de Datos: INSERT, UPDATE, DELETE (Módulo 6)

**Ejercicio 18. — INSERT**
Ingresa una nueva consulta con los siguientes datos:
- Mascota: `'Kira'`, especie `'Perro'`, raza `'Husky Siberiano'`
- Edad: 2 años, tipo de consulta: `'Vacunación'`
- Veterinario: `'Dra. Ramírez'`, ciudad: `'Bogotá'`
- Costo: `45000`, duración: `20` minutos, estado: `'pendiente'`

---

**Ejercicio 19. — UPDATE**
La clínica decidió aumentar un 10% el costo de todas las consultas de tipo `'Cirugía'`. Escribe el `UPDATE` correspondiente.

---

**Ejercicio 20. — UPDATE con condición compuesta**
Cambia el estado a `'completada'` para todas las consultas que estén en `'pendiente'` **y** pertenezcan a la ciudad de `'Bogotá'`.

---

**Ejercicio 21. — DELETE**
Elimina del registro todas las consultas con estado `'cancelada'`. Antes de ejecutar el `DELETE`, escribe primero el `SELECT` que te permitiría ver qué registros serían eliminados.

---

## Desafío Final — Consulta combinada

**Ejercicio 22.**
Muestra, por ciudad, el número de consultas completadas y el costo promedio de esas consultas. Incluye solo las ciudades que tengan **al menos 3 consultas completadas**. Ordena los resultados de mayor a menor costo promedio. Muestra las columnas: `ciudad`, `total_consultas`, `costo_promedio`.

---  
