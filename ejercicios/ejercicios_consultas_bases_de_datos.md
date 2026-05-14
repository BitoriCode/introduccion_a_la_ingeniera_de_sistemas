# Ejercicio práctico 2: Consultas SQL con SELECT

## Contexto

La plataforma **AprenderCo** ofrece cursos en línea sobre tecnología, diseño, negocios e idiomas. El equipo de contenido necesita consultar su catálogo para tomar decisiones sobre precios, recomendaciones y estrategia editorial.

Tu tarea es escribir las consultas SQL que respondan cada una de sus preguntas.

## Preparación

Copia y ejecuta el siguiente script en SQLite para cargar los datos:

```sql

INSERT INTO cursos (titulo, categoria, instructor, duracion_horas, precio, calificacion, nivel, idioma) VALUES
    ('Python para Principiantes',    'Programación', 'Andrea Suárez',   20,  89000, 4.8, 'Principiante', 'Español'),
    ('Diseño UX/UI con Figma',       'Diseño',       'Camilo Torres',   35, 120000, 4.5, 'Avanzado',     'Español'),
    ('Marketing Digital Básico',     'Marketing',    'Laura Méndez',    15,  75000, 4.2, 'Principiante', 'Español'),
    ('Excel Avanzado',               'Negocios',     'Jorge Ramírez',   25,  95000, 4.6, 'Avanzado',     'Español'),
    ('Inglés para Negocios',         'Idiomas',      'Sarah Johnson',   40, 150000, 4.9, 'Intermedio',   'Inglés'),
    ('Desarrollo Web con React',     'Programación', 'Andrés Cano',     50, 180000, 4.7, 'Avanzado',     'Español'),
    ('Fotografía Digital',           'Diseño',       'María Gómez',     18,  65000, 4.1, 'Principiante', 'Español'),
    ('SQL y Bases de Datos',         'Programación', 'Ricardo Peña',    30, 110000, 4.8, 'Intermedio',   'Español'),
    ('Emprendimiento Creativo',      'Negocios',     'Valentina Cruz',  20,  80000, 4.3, 'Principiante', 'Español'),
    ('Francés Básico',               'Idiomas',      'Marie Dupont',    30, 130000, 4.4, 'Principiante', 'Francés'),
    ('Inteligencia Artificial',      'Programación', 'Carlos Mora',     60, 220000, 4.9, 'Avanzado',     'Español'),
    ('Branding y Marca Personal',    'Marketing',    'Sofía Vargas',    22,  90000, 4.0, 'Intermedio',   'Español'),
    ('Gestión de Proyectos',         'Negocios',     'Felipe Ruiz',     28, 105000, 4.5, 'Intermedio',   'Español'),
    ('Ilustración Digital',          'Diseño',       'Paula Herrera',   45, 160000, 4.6, 'Avanzado',     'Español'),
    ('JavaScript Moderno',           'Programación', 'Andrés Cano',     40, 140000, 4.7, 'Intermedio',   'Español');
```

La tabla `cursos` tiene las siguientes columnas:

| Columna | Tipo | Descripción |
|---|---|---|
| `id_curso` | INTEGER | Identificador único |
| `titulo` | TEXT | Nombre del curso |
| `categoria` | TEXT | Programación, Diseño, Marketing, Negocios, Idiomas |
| `instructor` | TEXT | Nombre del instructor |
| `duracion_horas` | INTEGER | Duración total en horas |
| `precio` | REAL | Precio en pesos colombianos |
| `calificacion` | REAL | Promedio de valoraciones (1.0 – 5.0) |
| `nivel` | TEXT | Principiante, Intermedio, Avanzado |
| `idioma` | TEXT | Idioma en que se dicta el curso |

---

## Parte 1: SELECT básico

**1.** Muestra el título, instructor y categoría de todos los cursos del catálogo.
> Resultado esperado: 15 filas.

```sql

```

---

**2.** Muestra todos los datos de todos los cursos.
> Resultado esperado: 15 filas.

```sql

```

---

**3.** Muestra el título y el precio de todos los cursos usando los alias `"Nombre del curso"` y `"Precio"`. Ordénalos por precio de menor a mayor.

```sql

```

---

## Parte 2: WHERE — filtros simples

**4.** ¿Qué cursos pertenecen a la categoría `Programación`?
Muestra título, instructor y nivel.
> Resultado esperado: 5 filas.

```sql

```

---

**5.** ¿Qué cursos tienen un precio mayor a $130.000?
Muestra título, precio y categoría.
> Resultado esperado: 5 filas.

```sql

```

---

**6.** ¿Qué cursos tienen una calificación menor a 4.3?
Muestra título, calificación e instructor.
> Resultado esperado: 3 filas.

```sql

```

---

## Parte 3: AND, OR, NOT

**7.** ¿Qué cursos son de la categoría `Diseño` **y** de nivel `Avanzado`?
Muestra título, categoría y nivel.
> Resultado esperado: 2 filas.

```sql

```

---

**8.** ¿Qué cursos pertenecen a `Negocios` **o** a `Idiomas`?
Muestra título, categoría y precio.
> Resultado esperado: 5 filas.

```sql

```

---

**9.** ¿Qué cursos **no** están en idioma `Español`?
Muestra título, instructor e idioma.
> Resultado esperado: 2 filas.

```sql

```

---

## Parte 4: BETWEEN e IN

**10.** ¿Qué cursos tienen un precio entre $80.000 y $120.000 (ambos inclusive)?
Muestra título, categoría y precio.
> Resultado esperado: 7 filas.

```sql

```

---

**11.** ¿Qué cursos tienen una duración entre 20 y 35 horas (ambas inclusive)?
Muestra título, instructor y `duracion_horas`.
> Resultado esperado: 8 filas.

```sql

```

---

**12.** ¿Qué cursos son de categoría `Diseño` o `Marketing`?
Usa `IN`. Muestra título, categoría y nivel.
> Resultado esperado: 5 filas.

```sql

```

---

**13.** ¿Qué cursos **no** son de nivel `Principiante` **ni** `Avanzado`?
Usa `NOT IN`. Muestra título, nivel y precio.
> Resultado esperado: 5 filas.

```sql

```

---

## Parte 5: LIKE

**14.** ¿Qué cursos tienen la palabra `Digital` en el título?
Muestra título y categoría.
> Resultado esperado: 3 filas.

```sql

```

---

**15.** ¿Qué cursos son dictados por instructores cuyo nombre empieza con `A`?
Muestra título e instructor.
> Resultado esperado: 3 filas.

> **Pista:** El nombre del instructor incluye nombre y apellido en la misma columna.

```sql

```

---

**16.** ¿Qué cursos tienen la palabra `para` en el título?
Muestra título e instructor.
> Resultado esperado: 2 filas.

```sql

```

---

## Parte 6: ORDER BY y LIMIT

**17.** Lista todos los cursos ordenados por calificación de mayor a menor.
Muestra título, calificación y categoría.

```sql

```

---

**18.** Lista todos los cursos ordenados por categoría (A → Z) y, dentro de cada categoría, por precio de menor a mayor.
Muestra título, categoría y precio.

```sql

```

---

**19.** ¿Cuáles son los 3 cursos más caros del catálogo?
Muestra título, categoría y precio.

```sql

```

---

**20.** ¿Cuáles son los 5 cursos más cortos (menor duración en horas)?
Muestra título, `duracion_horas` y nivel.

```sql

```

---

## Parte 7: DISTINCT

**21.** ¿Qué categorías distintas ofrece la plataforma?
> Resultado esperado: 5 categorías.

```sql

```

---

**22.** ¿Qué niveles distintos existen en el catálogo?
> Resultado esperado: 3 niveles.

```sql

```

---

## Desafío final

**23.** Muestra el título, categoría, precio y nivel de los cursos que cumplan **todas** estas condiciones:
- Pertenecen a `Programación` **o** a `Diseño`.
- Son de nivel `Avanzado`.
- Tienen un precio mayor a $100.000.

Ordénalos por precio de mayor a menor.
> Resultado esperado: 4 filas.

```sql

```

---

**24.** ¿Cuáles son los 3 cursos de nivel `Intermedio` con mejor calificación?
Muestra título, nivel, calificación y precio.

```sql

```
