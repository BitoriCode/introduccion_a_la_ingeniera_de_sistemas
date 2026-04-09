# Ejercicios de HTML.

## Indicaciones generales

Estos **10 ejercicios** están pensados para practicar durante la primera sesión del curso. Todos se resuelven únicamente con **HTML**, sin JavaScript ni estilos. El objetivo es que se familiaricen con las etiquetas, la estructura de los documentos y las buenas prácticas que vimos en clase.

> **Recomendación:** Para cada ejercicio, creen un archivo `.html` independiente. Pueden organizarlos en una carpeta llamada `ejercicios-html/`. Abran cada archivo en el navegador para ir viendo el resultado.

> **Recuerden:** Todos los archivos deben comenzar con la estructura básica de HTML5 (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`).

---

## Ejercicio 1: Mi primera página

**Dificultad:** Baja

**Enunciado:** Crear un archivo `ejercicio1.html` que contenga la estructura básica de HTML5 con un título en la pestaña del navegador que diga "Mi primera página" y dentro del `<body>` un encabezado `<h1>` que diga "¡Hola mundo!" y un párrafo debajo que diga "Esta es mi primera página web."

**Requisitos:**
- Usar `<!DOCTYPE html>` al inicio.
- El atributo `lang` del `<html>` debe ser `"es"`.
- Incluir `<meta charset="UTF-8">`.
- Incluir `<title>` con el texto indicado.
- Un `<h1>` y un `<p>` dentro del `<body>`.

**Pistas:**
- Revisen la sección "Estructura básica de un documento HTML" de las notas de clase.
- No olviden cerrar todas las etiquetas que lo requieran.

---

## Ejercicio 2: Encabezados y párrafos

**Dificultad:** Baja

**Enunciado:** Crear una página que muestre los seis niveles de encabezado (`<h1>` a `<h6>`), cada uno seguido de un párrafo corto que explique para qué se usa ese nivel.

**Requisitos:**
- Usar los seis niveles de encabezado en orden.
- Debajo de cada encabezado, un `<p>` con una breve explicación (pueden inventarla con sus palabras).
- Incluir al menos una palabra en **negrita** (`<strong>`) y una en *cursiva* (`<em>`) a lo largo de los párrafos.
- Agregar una línea horizontal (`<hr>`) entre cada sección.

**Pistas:**
- `<strong>` da importancia semántica (negrita), `<em>` da énfasis (cursiva).
- `<hr>` es una etiqueta auto-cerrada.

---

## Ejercicio 3: Lista de materias

**Dificultad:** Baja

**Enunciado:** Crear una página que muestre el horario de un estudiante usando listas.

**Requisitos:**
- Un `<h1>` con el texto "Mi horario de clases".
- Una **lista ordenada** (`<ol>`) con los días de la semana (lunes a viernes).
- Dentro de cada `<li>` de día, una **lista desordenada** (`<ul>`) anidada con las materias de ese día (inventen al menos 2 materias por día).
- Al final, un párrafo que diga cuántas materias tienen en total.

**Pistas:**
- Las listas se pueden anidar: dentro de un `<li>` pueden poner otro `<ul>` o `<ol>`.
- Asegúrense de cerrar bien cada nivel de lista.

---

## Ejercicio 4: Enlaces y navegación

**Dificultad:** Baja

**Enunciado:** Crear una página que funcione como una colección de enlaces útiles para un estudiante de ingeniería.

**Requisitos:**
- Un `<h1>` con el texto "Enlaces útiles".
- Al menos **6 enlaces** (`<a>`) organizados en una lista desordenada, cada uno apuntando a una URL real (por ejemplo: Google, Wikipedia, YouTube, MDN Web Docs, la página de su universidad, etc.).
- Al menos 2 de los enlaces deben abrirse en una **nueva pestaña** (`target="_blank"` con `rel="noopener noreferrer"`).
- Incluir un enlace interno que lleve a una sección más abajo en la misma página (usando `id` y `href="#id"`).
- Al final de la página, una sección con `id` correspondiente que diga "Aquí termina la página".

**Pistas:**
- Para el enlace interno: pongan un `id` en el elemento destino (ejemplo: `<h2 id="final">`) y enlacen con `<a href="#final">Ir al final</a>`.
- No olviden `rel="noopener noreferrer"` cuando usen `target="_blank"`.

---

## Ejercicio 5: Tabla de notas

**Dificultad:** Media

**Enunciado:** Crear una página que muestre las notas de un estudiante en formato de tabla.

**Requisitos:**
- Un `<h1>` con el texto "Reporte de notas".
- Una tabla con las siguientes columnas: **Materia**, **Nota 1**, **Nota 2**, **Nota 3**, **Definitiva**.
- Al menos **5 filas** de datos con nombres de materias inventadas y notas numéricas.
- Usar `<thead>` para los encabezados y `<tbody>` para los datos.
- Los encabezados de columna deben estar en `<th>`.
- Agregar un `<caption>` a la tabla con el texto "Notas del semestre 2026-1".

**Pistas:**
- La etiqueta `<caption>` va justo después de abrir `<table>` y antes de `<thead>`.
- Cada fila se define con `<tr>`, y las celdas de datos con `<td>`.

---

## Ejercicio 6: Formulario de inscripción

**Dificultad:** Media

**Enunciado:** Crear una página con un formulario de inscripción a un evento universitario.

**Requisitos:**
- Un `<h1>` con el texto "Inscripción a la Semana de la Ingeniería".
- El formulario debe contener:
  - Campo de **nombre completo** (texto).
  - Campo de **correo electrónico** (tipo email).
  - Campo de **número de celular** (tipo tel).
  - Un **select** para elegir la carrera (al menos 4 opciones).
  - **Radio buttons** para seleccionar la jornada: "Mañana" o "Tarde".
  - Un **checkbox** que diga "Acepto los términos y condiciones".
  - Un **textarea** para comentarios adicionales.
  - Un botón de **enviar**.
- Todos los campos deben tener su respectivo `<label>` con el atributo `for`.
- Los campos obligatorios deben tener el atributo `required`.

**Pistas:**
- Para los radio buttons, usen el mismo `name` en ambos para que solo se pueda seleccionar uno.
- El atributo `for` del `<label>` debe coincidir con el `id` del campo.
- `<textarea>` tiene atributos `rows` y `cols` para definir su tamaño.

---

## Ejercicio 7: Galería de imágenes con descripciones

**Dificultad:** Media

**Enunciado:** Crear una página que simule una galería con al menos 4 imágenes (pueden usar imágenes placeholder), cada una con su título y descripción.

**Requisitos:**
- Un `<h1>` con el texto "Mi galería".
- Para cada imagen, crear una sección con:
  - La etiqueta `<figure>` como contenedor.
  - Una `<img>` con `src` (pueden usar `https://via.placeholder.com/300x200` o cualquier imagen), `alt` descriptivo y `width`.
  - Un `<figcaption>` con el título o descripción de la imagen.
- Al menos 4 imágenes.
- Cada imagen debe tener un texto alternativo (`alt`) diferente y descriptivo.

**Pistas:**
- `<figure>` es una etiqueta semántica que agrupa una imagen con su leyenda.
- `<figcaption>` va dentro de `<figure>`, generalmente después de `<img>`.
- El atributo `alt` es obligatorio en las imágenes por temas de accesibilidad.

---

## Ejercicio 8: Página de perfil personal

**Dificultad:** Media

**Enunciado:** Crear una página completa que funcione como un perfil personal, usando etiquetas semánticas para organizarla.

**Requisitos:**
- Usar `<header>` con un `<h1>` (su nombre) y una `<nav>` con al menos 3 enlaces internos (ejemplo: "Sobre mí", "Habilidades", "Contacto").
- Usar `<main>` para el contenido principal con tres `<section>`:
  - **Sobre mí:** Un párrafo de presentación y una imagen (puede ser placeholder).
  - **Habilidades:** Una lista desordenada con al menos 5 habilidades.
  - **Contacto:** Un formulario simple con campos para nombre, correo y mensaje, más un botón de enviar.
- Cada `<section>` debe tener un `id` que corresponda con los enlaces de la navegación.
- Usar `<footer>` con un párrafo que diga el año y su nombre.

**Pistas:**
- Los enlaces de navegación deben usar `href="#id-de-la-seccion"`.
- Recuerden que solo debe haber **un** `<main>` por página.
- La etiqueta `&copy;` genera el símbolo de copyright (©).

---

## Ejercicio 9: Artículo con estructura completa

**Dificultad:** Media - Alta

**Enunciado:** Crear una página que simule un artículo de blog o noticia, con estructura semántica completa y contenido variado.

**Requisitos:**
- `<header>` con el nombre del "blog" y una `<nav>` con enlaces (pueden ser ficticios con `href="#"`).
- Dentro de `<main>`, un `<article>` que contenga:
  - Un `<h2>` como título del artículo.
  - Un párrafo con la fecha de publicación y el nombre del autor (usen `<time>` para la fecha con el atributo `datetime`).
  - Al menos 3 párrafos de contenido (pueden ser sobre cualquier tema: tecnología, ciencia, deporte, etc.).
  - Una imagen relacionada con `<figure>` y `<figcaption>`.
  - Una cita textual usando `<blockquote>` con el atributo `cite`.
  - Una lista ordenada o desordenada dentro del contenido.
- Un `<aside>` al mismo nivel que el `<article>` (dentro de `<main>`) con:
  - Un `<h3>` que diga "Artículos relacionados".
  - Una lista de 3 enlaces ficticios.
- `<footer>` con información de copyright.

**Pistas:**
- La etiqueta `<time datetime="2026-04-09">9 de abril de 2026</time>` permite que los navegadores entiendan la fecha.
- `<blockquote>` es para citas textuales largas. Para citas cortas dentro de un párrafo, existe `<q>`.
- `<article>` representa contenido independiente que tendría sentido por sí solo.

---

## Ejercicio 10: Página web completa de un proyecto

**Dificultad:** Alta

**Enunciado:** Crear una página web completa que presente un proyecto universitario ficticio. Deben combinar la mayoría de etiquetas que aprendimos en clase.

**Requisitos:**
- **Header:** Nombre del proyecto en `<h1>`, navegación con enlaces internos a cada sección de la página.
- **Sección "Descripción":** Al menos 2 párrafos explicando de qué se trata el proyecto. Incluir texto en negrita y cursiva donde tenga sentido.
- **Sección "Equipo":** Una tabla con los integrantes del equipo con columnas: Nombre, Rol, Correo. Al menos 4 filas. Usar `<thead>` y `<tbody>`.
- **Sección "Cronograma":** Una lista ordenada con las fases del proyecto (al menos 5 fases). Cada fase debe tener una breve descripción en un párrafo.
- **Sección "Recursos":** Una lista desordenada con al menos 5 enlaces a recursos externos (pueden ser reales o ficticios). Al menos 2 deben abrirse en nueva pestaña.
- **Sección "Contacto":** Un formulario con campos para nombre, correo electrónico, asunto (select con opciones como "Consulta", "Sugerencia", "Otro"), mensaje (textarea) y botón de enviar. Todos con sus `<label>` y validación `required`.
- **Footer:** Nombre de la universidad, año, y un enlace que vuelva al inicio de la página.
- **Requisitos generales:** Toda la página debe usar etiquetas semánticas (`<header>`, `<main>`, `<section>`, `<footer>`, `<nav>`). Cada sección debe tener un `id` para la navegación interna.

**Pistas:**
- Piensen primero en la estructura general antes de empezar a escribir. Pueden hacer un esquema en papel o en un comentario HTML (`<!-- estructura -->`).
- Para el enlace "volver al inicio" del footer, pongan un `id` en el `<header>` o en el `<body>` y enlacen con `href="#id"`.
- Usen `<br>` solo cuando necesiten un salto de línea dentro de un mismo bloque, no para separar secciones.
- Validen que todos los `id` sean únicos en la página.

---

## Criterios de evaluación sugeridos

| Criterio | Descripción |
|---|---|
| **Estructura correcta** | El documento tiene la estructura básica de HTML5 completa (`DOCTYPE`, `html`, `head`, `body`). |
| **Uso adecuado de etiquetas** | Cada etiqueta se usa según su propósito semántico (no usar `<table>` para diseño, por ejemplo). |
| **Atributos requeridos** | Las imágenes tienen `alt`, los formularios tienen `label` y `for`, los enlaces externos tienen `rel` apropiado. |
| **Organización** | El código está bien indentado y es fácil de leer. |
| **Completitud** | Se cumplen todos los requisitos del enunciado. |

---

Tómense su tiempo con cada ejercicio. Los primeros son rápidos y sirven para calentar, pero los últimos requieren más planeación. Si terminan antes de tiempo, pueden mejorar los ejercicios anteriores o intentar agregar más contenido al ejercicio 10.

Mucha suerte y recuerden: la mejor forma de aprender HTML es escribiendo HTML.
