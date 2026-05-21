# Trabajo Final — Bases de Datos con SQL
## Concesionario AutoColombia

| | |
|---|---|
| **Módulos evaluados** | 3 · Consultas SELECT — 4 · Agregación y GROUP BY — 5 · Subconsultas |
| **Modalidad** | Individual |
| **Puntaje total** | 50 puntos |
| **Entrega** | Archivo `.pdf` con todas las consultas, y evidencias de los resultados |

---

## Contexto

El concesionario **AutoColombia** tiene sedes en varias ciudades del país y gestiona su inventario de vehículos usados en una base de datos SQLite. La tabla `vehiculos` registra la información de cada vehículo:

| Columna | Tipo | Descripción |
|---|---|---|
| `id_vehiculo` | INTEGER | Identificador único |
| `marca` | TEXT | Toyota, Chevrolet, Mazda, Renault, Kia, Nissan |
| `modelo` | TEXT | Nombre del modelo |
| `anio` | INTEGER | Año del vehículo |
| `tipo` | TEXT | Sedán, SUV, Hatchback, Pickup |
| `color` | TEXT | Color de la carrocería |
| `kilometraje` | INTEGER | Kilómetros recorridos |
| `precio` | REAL | Precio de venta en pesos colombianos |
| `ciudad` | TEXT | Ciudad donde se encuentra el vehículo |
| `estado` | TEXT | `disponible`, `reservado` o `vendido` |
| `transmision` | TEXT | `manual` o `automática` |

Antes de comenzar, ejecuta el siguiente bloque SQL completo en tu herramienta (SQLite Browser, DBeaver, etc.):

```sql
DROP TABLE IF EXISTS vehiculos;

CREATE TABLE vehiculos (
    id_vehiculo  INTEGER PRIMARY KEY AUTOINCREMENT,
    marca        TEXT    NOT NULL,
    modelo       TEXT    NOT NULL,
    anio         INTEGER NOT NULL,
    tipo         TEXT    NOT NULL,
    color        TEXT    NOT NULL,
    kilometraje  INTEGER NOT NULL,
    precio       REAL    NOT NULL,
    ciudad       TEXT    NOT NULL,
    estado       TEXT    NOT NULL,
    transmision  TEXT    NOT NULL
);

INSERT INTO vehiculos (marca, modelo, anio, tipo, color, kilometraje, precio, ciudad, estado, transmision) VALUES
    ('Toyota',    'Corolla',  2019, 'Sedán',     'Blanco',   45000,  62000000, 'Bogotá',       'disponible', 'automática'),
    ('Chevrolet', 'Spark',    2021, 'Hatchback', 'Rojo',     18000,  38000000, 'Medellín',     'disponible', 'manual'),
    ('Mazda',     'CX-30',    2022, 'SUV',       'Gris',     12000,  95000000, 'Bogotá',       'disponible', 'automática'),
    ('Renault',   'Logan',    2018, 'Sedán',     'Blanco',   72000,  35000000, 'Cali',         'vendido',    'manual'),
    ('Toyota',    'Hilux',    2020, 'Pickup',    'Negro',    55000, 115000000, 'Barranquilla', 'disponible', 'manual'),
    ('Chevrolet', 'Tracker',  2021, 'SUV',       'Azul',     30000,  82000000, 'Bogotá',       'reservado',  'automática'),
    ('Kia',       'Picanto',  2022, 'Hatchback', 'Amarillo',  8000,  42000000, 'Medellín',     'disponible', 'manual'),
    ('Mazda',     'Mazda 3',  2019, 'Sedán',     'Negro',    60000,  58000000, 'Cali',         'disponible', 'automática'),
    ('Nissan',    'Frontier', 2020, 'Pickup',    'Blanco',   40000,  98000000, 'Bogotá',       'vendido',    'manual'),
    ('Renault',   'Duster',   2021, 'SUV',       'Gris',     25000,  68000000, 'Pereira',      'disponible', 'manual'),
    ('Toyota',    'Fortuner', 2022, 'SUV',       'Negro',    15000, 145000000, 'Bogotá',       'disponible', 'automática'),
    ('Chevrolet', 'Onix',     2020, 'Sedán',     'Blanco',   38000,  48000000, 'Bucaramanga',  'disponible', 'manual'),
    ('Kia',       'Sportage', 2021, 'SUV',       'Azul',     22000,  89000000, 'Medellín',     'disponible', 'automática'),
    ('Mazda',     'BT-50',    2019, 'Pickup',    'Gris',     65000,  78000000, 'Cali',         'disponible', 'manual'),
    ('Renault',   'Kwid',     2022, 'Hatchback', 'Naranja',   5000,  34000000, 'Bogotá',       'disponible', 'manual'),
    ('Toyota',    'RAV4',     2020, 'SUV',       'Blanco',   35000, 118000000, 'Barranquilla', 'reservado',  'automática'),
    ('Chevrolet', 'Captiva',  2018, 'SUV',       'Rojo',     80000,  65000000, 'Bogotá',       'vendido',    'automática'),
    ('Kia',       'Sorento',  2022, 'SUV',       'Negro',    10000, 132000000, 'Medellín',     'disponible', 'automática'),
    ('Nissan',    'Kicks',    2021, 'SUV',       'Azul',     20000,  72000000, 'Cali',         'disponible', 'automática'),
    ('Renault',   'Sandero',  2019, 'Hatchback', 'Blanco',   55000,  32000000, 'Pereira',      'vendido',    'manual');
```

---

## Parte 1 — SELECT básico *(10 puntos, 2 pts c/u)*

**1.** Muestra la marca, modelo, año y precio de **todos** los vehículos del inventario.

```sql

```

---

**2.** Muestra todos los datos de todos los vehículos cuyo estado sea `'disponible'`.

```sql

```

---

**3.** Muestra la marca, modelo y precio de los vehículos disponibles en Bogotá, ordenados por precio de menor a mayor.

```sql

```

---

**4.** Muestra los 5 vehículos con **menor kilometraje** del inventario.
Incluye marca, modelo, kilometraje y ciudad.

```sql

```

---

**5.** Muestra marca, modelo y precio de todos los vehículos usando los alias `"Marca"`, `"Modelo"` y `"Precio de venta"`. Ordena los resultados por marca (A→Z) y dentro de cada marca por año (más reciente primero).

```sql

```

---

## Parte 2 — Filtros y operadores *(15 puntos, 3 pts c/u)*

**6.** ¿Qué vehículos **SUV** están disponibles y tienen transmisión **automática**?
Muestra marca, modelo, ciudad y precio.

```sql

```

---

**7.** ¿Qué vehículos tienen un precio entre $40.000.000 y $80.000.000 (ambos inclusive) **y** menos de 40.000 km?
Muestra marca, modelo, precio y kilometraje.

```sql

```

---

**8.** ¿Qué vehículos son de marca Toyota, Kia **o** Nissan?
Usa `IN`. Muestra marca, modelo, año y ciudad.

```sql

```

---

**9.** ¿Qué vehículos tienen un modelo cuyo nombre **contiene** la letra `'a'`?
Usa `LIKE`. Muestra marca, modelo y tipo.

```sql

```

---

**10.** ¿Qué vehículos **no** están en Bogotá **ni** en Medellín, y su precio es menor a $70.000.000?
Muestra marca, modelo, ciudad y precio, ordenados por ciudad.

```sql

```

---

## Parte 3 — Funciones de agregación y GROUP BY *(15 puntos, 3 pts c/u)*

**11.** ¿Cuántos vehículos hay en el inventario en total?
¿Y cuántos están en estado `'disponible'`?
> Muestra los dos valores en una sola consulta usando dos `COUNT` con alias distintos y `WHERE`.

```sql
-- Total de vehículos:

-- Vehículos disponibles:

```

---

**12.** ¿Cuál es el precio promedio, el precio más alto y el precio más bajo de todos los vehículos disponibles?
Usa alias descriptivos.

```sql

```

---

**13.** ¿Cuántos vehículos hay de cada **tipo** (Sedán, SUV, Hatchback, Pickup)?
Muestra el tipo y la cantidad, ordenados de mayor a menor cantidad.

```sql

```

---

**14.** ¿Cuál es el **precio promedio** por ciudad, solo para los vehículos disponibles?
Muestra ciudad y precio promedio (alias `"Precio promedio"`), ordenados por precio promedio de mayor a menor.

```sql

```

---

**15.** ¿Qué marcas tienen **más de 3 vehículos** en el inventario (sin importar el estado)?
Muestra la marca y la cantidad.

```sql

```

---

## Parte 4 — Subconsultas *(10 puntos, 5 pts c/u)*

**16.** Muestra la marca, modelo y precio de los vehículos cuyo precio es **mayor al precio promedio** de todos los vehículos del inventario.
Ordena los resultados por precio de mayor a menor.

```sql

```

---

**17.** ¿Qué otros vehículos están en la **misma ciudad** que la Toyota Fortuner?
Muestra marca, modelo y ciudad, excluyendo a la Fortuner del resultado.

> La ciudad de la Fortuner debe obtenerse con una subconsulta.

```sql

```

---

## Rúbrica de evaluación

| Criterio | Descripción | Puntaje |
|---|---|---|
| **Parte 1** | Consultas correctas con SELECT, ORDER BY y LIMIT | 10 pts |
| **Parte 2** | Uso correcto de WHERE, AND/OR/NOT, BETWEEN, IN, LIKE | 15 pts |
| **Parte 3** | Uso correcto de COUNT/AVG/MAX/MIN, GROUP BY y HAVING | 15 pts |
| **Parte 4** | Subconsultas con valor escalar y con referencia a otra fila | 10 pts |
| **Total** | | **50 pts** |

> **Criterios de descuento:**
> - Consulta que produce error de sintaxis: 0 pts en ese punto.
> - Consulta que produce resultado incorrecto: descuento proporcional.
> - Uso del valor numérico literal en lugar de subconsulta en la Parte 4: descuento del 50 % en ese punto.
