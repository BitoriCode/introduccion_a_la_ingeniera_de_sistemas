# Referencia rápida de etiquetas HTML

> **¿Para qué es este documento?** Es tu guía de consulta. Cuando estés programando y no recuerdes cómo se usa una etiqueta o qué atributos tiene, venís acá y lo buscás. Está organizado por categorías para que lo encuentres rápido.

---

## 1. Estructura del documento

Estas etiquetas definen el esqueleto de **todo** archivo HTML. Sin ellas, el navegador no sabe qué hacer con tu página.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<!DOCTYPE html>` | Declara que el documento es HTML5 | No |
| `<html>` | Elemento raíz que envuelve todo el documento | Sí |
| `<head>` | Contiene metadatos (info que no se ve en la página) | Sí |
| `<body>` | Contiene todo el contenido visible de la página | Sí |

### Atributos comunes

| Etiqueta | Atributo | Descripción | Ejemplo |
|---|---|---|---|
| `<html>` | `lang` | Idioma de la página | `<html lang="es">` |

### Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <!-- Metadatos van acá -->
</head>
<body>
    <!-- Contenido visible va acá -->
</body>
</html>
```

---

## 2. Metadatos (van dentro de `<head>`)

Estas etiquetas le dan información al navegador sobre la página, pero el usuario no las ve directamente.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<meta>` | Define metadatos como codificación, viewport, etc. | No |
| `<title>` | Título que aparece en la pestaña del navegador | Sí |
| `<link>` | Conecta archivos externos (CSS, íconos, etc.) | No |

### Atributos comunes

| Etiqueta | Atributo | Descripción | Ejemplo |
|---|---|---|---|
| `<meta>` | `charset` | Codificación de caracteres | `<meta charset="UTF-8">` |
| `<meta>` | `name` | Tipo de metadato | `<meta name="viewport">` |
| `<meta>` | `content` | Valor del metadato | `content="width=device-width, initial-scale=1.0"` |
| `<title>` | *(ninguno especial)* | Solo contiene texto | `<title>Mi página</title>` |
| `<link>` | `rel` | Relación con el documento | `rel="stylesheet"` |
| `<link>` | `href` | Ruta al archivo externo | `href="estilos.css"` |

### Ejemplo completo

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi sitio web</title>
    <link rel="stylesheet" href="estilos.css">
</head>
```

---

## 3. Encabezados

Los encabezados definen los títulos y subtítulos de la página. Van de `<h1>` (el más importante) a `<h6>` (el menos).

| Etiqueta | Nivel | Uso típico |
|---|---|---|
| `<h1>` | 1 (máximo) | Título principal de la página — **solo uno** por página |
| `<h2>` | 2 | Secciones principales |
| `<h3>` | 3 | Subsecciones |
| `<h4>` | 4 | Divisiones menores |
| `<h5>` | 5 | Poco usado, detalles |
| `<h6>` | 6 (mínimo) | Poco usado, detalles menores |

### Ejemplo

```html
<h1>Festival de Comida Callejera</h1>
<h2>Puestos participantes</h2>
<h3>Zona de hamburguesas</h3>
```

> **Regla clave:** No salten niveles. No pongan un `<h4>` después de un `<h1>` sin pasar por `<h2>` y `<h3>`. Piénsenlo como un índice de un libro.

---

## 4. Texto y formato

Etiquetas para escribir y dar formato al texto dentro de la página.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<p>` | Párrafo de texto | Sí |
| `<strong>` | Texto en **negrita** con importancia semántica | Sí |
| `<em>` | Texto en *cursiva* con énfasis | Sí |
| `<br>` | Salto de línea dentro de un párrafo | No |
| `<hr>` | Línea horizontal separadora | No |
| `<span>` | Contenedor en línea (no rompe el flujo del texto) | Sí |

### Ejemplo

```html
<p>Este es un párrafo normal.</p>

<p>Podemos resaltar algo <strong>importante</strong> o dar <em>énfasis</em> a una idea.</p>

<p>Primera línea<br>Segunda línea (mismo párrafo)</p>

<hr>

<p>El precio es <span>$50.000</span> pesos colombianos.</p>
```

> **¿Cuándo usar `<strong>` vs `<em>`?** `<strong>` = "esto es importante, préstale atención". `<em>` = "esto tiene un tono diferente, un énfasis". No son solo negrita y cursiva: tienen significado para los lectores de pantalla.

---

## 5. Listas

Para mostrar elementos agrupados, ya sea con viñetas o con números.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<ul>` | Lista **desordenada** (viñetas: •) | Sí |
| `<ol>` | Lista **ordenada** (números: 1, 2, 3...) | Sí |
| `<li>` | Cada elemento de la lista | Sí |

### Atributos comunes

| Etiqueta | Atributo | Descripción | Ejemplo |
|---|---|---|---|
| `<ol>` | `type` | Tipo de numeración | `type="A"` (A, B, C), `type="I"` (I, II, III) |
| `<ol>` | `start` | Número de inicio | `<ol start="5">` (empieza en 5) |
| `<ol>` | `reversed` | Cuenta hacia atrás | `<ol reversed>` |

### Ejemplo: lista desordenada

```html
<ul>
    <li>Bandeja paisa</li>
    <li>Ajiaco</li>
    <li>Sancocho</li>
</ul>
```

### Ejemplo: lista ordenada

```html
<ol>
    <li>Prender el computador</li>
    <li>Abrir el editor de código</li>
    <li>Crear un archivo .html</li>
</ol>
```

### Ejemplo: listas anidadas

```html
<ul>
    <li>Comida colombiana
        <ul>
            <li>Arepa</li>
            <li>Empanada</li>
        </ul>
    </li>
    <li>Comida mexicana
        <ul>
            <li>Taco</li>
            <li>Burrito</li>
        </ul>
    </li>
</ul>
```

> **¿Cuándo usar `<ul>` vs `<ol>`?** Si el orden importa (pasos, rankings, instrucciones) → `<ol>`. Si no importa (ingredientes, características, opciones) → `<ul>`.

---

## 6. Enlaces (Links)

Permiten navegar a otras páginas, secciones o sitios web.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<a>` | Crea un enlace (hipervínculo) | Sí |

### Atributos

| Atributo | Descripción | Ejemplo |
|---|---|---|
| `href` | URL o ruta de destino (**obligatorio**) | `href="https://google.com"` |
| `target` | Dónde abrir el enlace | `target="_blank"` (nueva pestaña) |
| `rel` | Relación con la página destino | `rel="noopener noreferrer"` |

### Tipos de enlaces y ejemplos

**Enlace externo** (a otro sitio):
```html
<a href="https://www.google.com">Ir a Google</a>
```

**Enlace externo en nueva pestaña** (siempre con `rel` por seguridad):
```html
<a href="https://www.google.com" target="_blank" rel="noopener noreferrer">
    Ir a Google (nueva pestaña)
</a>
```

**Enlace interno** (a otra página de tu sitio):
```html
<a href="contacto.html">Ir a Contacto</a>
```

**Enlace a una sección** de la misma página (usando `id`):
```html
<!-- El enlace -->
<a href="#precios">Ver precios</a>

<!-- Más abajo en la página, el destino -->
<section id="precios">
    <h2>Precios</h2>
</section>
```

**Enlace de correo electrónico:**
```html
<a href="mailto:info@festival.com">Escríbenos</a>
```

**Enlace de teléfono:**
```html
<a href="tel:+573001234567">Llámanos</a>
```

---

## 7. Imágenes

Para mostrar imágenes en la página.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<img>` | Inserta una imagen | No (auto-cerrada) |
| `<figure>` | Contenedor semántico para imagen + leyenda | Sí |
| `<figcaption>` | Leyenda o descripción de una figura | Sí |

### Atributos de `<img>`

| Atributo | Descripción | ¿Obligatorio? | Ejemplo |
|---|---|---|---|
| `src` | Ruta o URL de la imagen | Sí | `src="fotos/logo.png"` |
| `alt` | Texto alternativo (accesibilidad) | Sí | `alt="Logo del festival"` |
| `width` | Ancho en píxeles | No | `width="400"` |
| `height` | Alto en píxeles | No | `height="300"` |

### Ejemplo básico

```html
<img src="fotos/festival.jpg" alt="Gente disfrutando en el festival" width="600">
```

### Ejemplo con `<figure>` y `<figcaption>`

```html
<figure>
    <img src="fotos/arepa.jpg" alt="Arepa de choclo con quesito" width="400">
    <figcaption>Arepa de choclo: uno de los platos más pedidos del festival.</figcaption>
</figure>
```

> **Siempre pongan `alt`.** Es obligatorio por accesibilidad. Los lectores de pantalla leen ese texto para personas con discapacidad visual. Además, si la imagen no carga, el navegador muestra el `alt`.

---

## 8. Tablas

Para mostrar datos organizados en filas y columnas.

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<table>` | Contenedor de la tabla | Sí |
| `<caption>` | Título descriptivo de la tabla | Sí |
| `<thead>` | Agrupa las filas de encabezado | Sí |
| `<tbody>` | Agrupa las filas de datos | Sí |
| `<tfoot>` | Agrupa las filas de pie de tabla | Sí |
| `<tr>` | Una fila (*table row*) | Sí |
| `<th>` | Celda de encabezado (*table header*) | Sí |
| `<td>` | Celda de dato (*table data*) | Sí |

### Atributos comunes

| Etiqueta | Atributo | Descripción | Ejemplo |
|---|---|---|---|
| `<td>`, `<th>` | `colspan` | Celda que ocupa varias columnas | `<td colspan="2">` |
| `<td>`, `<th>` | `rowspan` | Celda que ocupa varias filas | `<td rowspan="3">` |
| `<th>` | `scope` | Indica si el encabezado es de fila o columna | `scope="col"` o `scope="row"` |

### Ejemplo completo

```html
<table>
    <caption>Notas del semestre</caption>
    <thead>
        <tr>
            <th>Materia</th>
            <th>Nota 1</th>
            <th>Nota 2</th>
            <th>Definitiva</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Programación</td>
            <td>4.5</td>
            <td>3.8</td>
            <td>4.15</td>
        </tr>
        <tr>
            <td>Cálculo</td>
            <td>3.0</td>
            <td>3.5</td>
            <td>3.25</td>
        </tr>
    </tbody>
</table>
```

### Ejemplo con `colspan` (celda que ocupa varias columnas)

```html
<table>
    <tr>
        <th colspan="3">Horario del lunes</th>
    </tr>
    <tr>
        <td>7:00 AM</td>
        <td>Cálculo</td>
        <td>Salón 301</td>
    </tr>
</table>
```

> **Las tablas son para datos, no para diseño.** Si necesitan organizar visualmente la página, usen CSS. Las tablas son para información tabular: horarios, notas, precios, comparaciones.

---

## 9. Formularios

Permiten al usuario enviar información. Son la base de la interacción en la web.

### Etiquetas de formulario

| Etiqueta | ¿Qué hace? | ¿Se cierra? |
|---|---|---|
| `<form>` | Contenedor del formulario | Sí |
| `<input>` | Campo de entrada de datos | No |
| `<label>` | Etiqueta descriptiva para un campo | Sí |
| `<select>` | Menú desplegable | Sí |
| `<option>` | Cada opción dentro de un `<select>` | Sí |
| `<textarea>` | Campo de texto multilínea | Sí |
| `<button>` | Botón (enviar, resetear, etc.) | Sí |
| `<fieldset>` | Agrupa campos relacionados | Sí |
| `<legend>` | Título de un `<fieldset>` | Sí |

### Atributos de `<form>`

| Atributo | Descripción | Ejemplo |
|---|---|---|
| `action` | URL a donde se envían los datos | `action="/procesar"` |
| `method` | Método HTTP de envío | `method="POST"` o `method="GET"` |

### Atributos de `<input>` (los más usados)

| Atributo | Descripción | Ejemplo |
|---|---|---|
| `type` | Tipo de campo (ver tabla siguiente) | `type="email"` |
| `id` | Identificador único | `id="correo"` |
| `name` | Nombre del dato que se envía | `name="correo"` |
| `placeholder` | Texto de ayuda gris | `placeholder="tu@correo.com"` |
| `value` | Valor inicial o valor enviado | `value="opcion1"` |
| `required` | Campo obligatorio | `required` |
| `disabled` | Campo deshabilitado | `disabled` |
| `readonly` | Solo lectura (no editable) | `readonly` |
| `min` / `max` | Valor mínimo y máximo (para `number`, `date`) | `min="1" max="10"` |
| `minlength` / `maxlength` | Longitud mínima y máxima de texto | `maxlength="100"` |

### Tipos de `<input>`

| `type` | Descripción | Lo que muestra |
|---|---|---|
| `text` | Texto libre | Campo de texto normal |
| `email` | Correo electrónico | Valida formato de email |
| `password` | Contraseña | Oculta los caracteres (•••) |
| `number` | Número | Campo numérico con flechas ↑↓ |
| `tel` | Teléfono | En celulares abre teclado numérico |
| `date` | Fecha | Selector de fecha del navegador |
| `time` | Hora | Selector de hora |
| `url` | Dirección web | Valida formato de URL |
| `search` | Búsqueda | Como `text` pero con ícono de lupa |
| `radio` | Opción única (botón redondo) | Solo uno del grupo puede seleccionarse |
| `checkbox` | Casilla de verificación | Puede seleccionarse independientemente |
| `file` | Subir archivos | Botón para seleccionar archivo |
| `range` | Control deslizante | Barra con slider |
| `color` | Selector de color | Abre un color picker |
| `hidden` | Campo oculto | No se ve, pero envía datos |
| `submit` | Botón de envío | Envía el formulario |
| `reset` | Botón de reinicio | Limpia todos los campos |

### Atributos de `<select>` y `<option>`

| Etiqueta | Atributo | Descripción | Ejemplo |
|---|---|---|---|
| `<select>` | `id`, `name` | Identificación del campo | `id="ciudad" name="ciudad"` |
| `<select>` | `required` | Selección obligatoria | `required` |
| `<select>` | `multiple` | Permite selección múltiple | `multiple` |
| `<option>` | `value` | Valor que se envía al servidor | `value="bogota"` |
| `<option>` | `selected` | Opción preseleccionada | `selected` |

### Atributos de `<textarea>`

| Atributo | Descripción | Ejemplo |
|---|---|---|
| `rows` | Número de filas visibles | `rows="4"` |
| `cols` | Número de columnas visibles | `cols="40"` |
| `placeholder` | Texto de ayuda | `placeholder="Escribe aquí..."` |
| `maxlength` | Límite de caracteres | `maxlength="500"` |

### Ejemplo: campo de texto con label

```html
<label for="nombre">Nombre:</label>
<input type="text" id="nombre" name="nombre" placeholder="Ej: María López" required>
```

> **Importante:** El `for` del `<label>` debe coincidir con el `id` del `<input>`. Esto hace que al hacer clic en el texto, el cursor salte al campo.

### Ejemplo: radio buttons (selección única)

```html
<label>Jornada:</label><br>

<input type="radio" id="manana" name="jornada" value="manana">
<label for="manana">Mañana</label><br>

<input type="radio" id="tarde" name="jornada" value="tarde">
<label for="tarde">Tarde</label>
```

> **Clave:** Todos los radio buttons del mismo grupo deben tener el **mismo `name`**. Así el navegador sabe que solo uno puede estar seleccionado.

### Ejemplo: checkboxes (selección múltiple)

```html
<label>Intereses:</label><br>

<input type="checkbox" id="musica" name="intereses" value="musica">
<label for="musica">Música</label><br>

<input type="checkbox" id="deporte" name="intereses" value="deporte">
<label for="deporte">Deporte</label><br>

<input type="checkbox" id="tecnologia" name="intereses" value="tecnologia">
<label for="tecnologia">Tecnología</label>
```

### Ejemplo: select (menú desplegable)

```html
<label for="ciudad">Ciudad:</label>
<select id="ciudad" name="ciudad" required>
    <option value="">— Seleccione —</option>
    <option value="bogota">Bogotá</option>
    <option value="medellin">Medellín</option>
    <option value="cali">Cali</option>
</select>
```

### Ejemplo: textarea

```html
<label for="mensaje">Mensaje:</label><br>
<textarea id="mensaje" name="mensaje" rows="5" cols="40"
    placeholder="Escribe tu mensaje aquí..." maxlength="500"></textarea>
```

### Ejemplo: fieldset y legend (agrupar campos)

```html
<fieldset>
    <legend>Datos personales</legend>

    <label for="nombre">Nombre:</label><br>
    <input type="text" id="nombre" name="nombre" required><br><br>

    <label for="edad">Edad:</label><br>
    <input type="number" id="edad" name="edad" min="15" max="99">
</fieldset>
```

### Ejemplo: formulario completo

```html
<form action="/enviar" method="POST">
    <fieldset>
        <legend>Registro</legend>

        <label for="nombre">Nombre:</label><br>
        <input type="text" id="nombre" name="nombre" required><br><br>

        <label for="correo">Correo:</label><br>
        <input type="email" id="correo" name="correo" required><br><br>

        <label for="password">Contraseña:</label><br>
        <input type="password" id="password" name="password" minlength="8" required><br><br>

        <label for="nacimiento">Fecha de nacimiento:</label><br>
        <input type="date" id="nacimiento" name="nacimiento"><br><br>

        <button type="submit">Registrarse</button>
        <button type="reset">Limpiar formulario</button>
    </fieldset>
</form>
```

---

## 10. Contenedores genéricos

No tienen significado visual ni semántico por sí solos, pero son muy útiles para agrupar elementos.

| Etiqueta | ¿Qué hace? | Tipo | ¿Se cierra? |
|---|---|---|---|
| `<div>` | Contenedor de **bloque** (ocupa todo el ancho) | Bloque | Sí |
| `<span>` | Contenedor **en línea** (no rompe el flujo) | En línea | Sí |

### Ejemplo

```html
<!-- div: agrupa una sección entera -->
<div>
    <h2>Noticias</h2>
    <p>Hoy aprendimos HTML.</p>
</div>

<!-- span: resalta algo dentro de un texto -->
<p>El total es <span>$120.000</span> pesos.</p>
```

> **¿Cuándo usar `<div>` vs etiquetas semánticas?** Si existe una etiqueta semántica que describe el contenido (`<header>`, `<section>`, `<article>`, etc.), úsenla. `<div>` es el último recurso cuando ninguna semántica aplica.

---

## 11. Etiquetas semánticas

Le dan **significado** a la estructura de la página. Ayudan a los navegadores, lectores de pantalla y motores de búsqueda a entender qué es cada parte.

| Etiqueta | ¿Qué representa? | ¿Se cierra? |
|---|---|---|
| `<header>` | Encabezado de la página o de una sección | Sí |
| `<nav>` | Bloque de navegación (menú) | Sí |
| `<main>` | Contenido principal de la página (**solo uno** por página) | Sí |
| `<section>` | Sección temática del contenido | Sí |
| `<article>` | Contenido independiente (noticia, post, tarjeta) | Sí |
| `<aside>` | Contenido complementario o lateral | Sí |
| `<footer>` | Pie de página o de sección | Sí |

### Estructura típica de una página

```html
<body>
    <header>
        <h1>Mi Sitio Web</h1>
        <nav>
            <a href="#inicio">Inicio</a>
            <a href="#acerca">Acerca de</a>
            <a href="#contacto">Contacto</a>
        </nav>
    </header>

    <main>
        <section id="inicio">
            <h2>Bienvenidos</h2>
            <p>Contenido principal.</p>
        </section>

        <article>
            <h2>Noticia del día</h2>
            <p>Contenido de la noticia.</p>
        </article>

        <aside>
            <h3>Dato curioso</h3>
            <p>HTML se creó en 1991.</p>
        </aside>
    </main>

    <footer>
        <p>&copy; 2026 — Todos los derechos reservados.</p>
    </footer>
</body>
```

> **Regla simple:** Si pueden reemplazar un `<div>` por una etiqueta semántica, háganlo. El código queda más legible y mejora la accesibilidad.

---

## 12. Atributos globales

Estos atributos se pueden usar en **cualquier** etiqueta HTML.

| Atributo | Descripción | Ejemplo |
|---|---|---|
| `id` | Identificador **único** del elemento (no repetir) | `<div id="menu">` |
| `class` | Clase para agrupar elementos similares (puede repetirse) | `<p class="destacado">` |
| `title` | Tooltip que aparece al pasar el mouse | `<abbr title="HyperText Markup Language">HTML</abbr>` |
| `hidden` | Oculta el elemento de la página | `<p hidden>Texto oculto</p>` |
| `style` | Estilos CSS directos (no recomendado para proyectos grandes) | `<p style="color: red;">` |
| `tabindex` | Orden de tabulación con el teclado | `<button tabindex="1">` |
| `lang` | Idioma del contenido del elemento | `<p lang="en">Hello</p>` |
| `data-*` | Atributos personalizados para guardar datos | `<div data-precio="15000">` |

### Diferencia entre `id` y `class`

```html
<!-- id: ÚNICO en toda la página. Para identificar UN elemento específico -->
<section id="contacto">...</section>

<!-- class: puede repetirse. Para aplicar estilos o comportamientos a VARIOS elementos -->
<p class="resaltado">Primer párrafo resaltado</p>
<p class="resaltado">Segundo párrafo resaltado</p>
```

---

## 13. Entidades HTML especiales

Cuando necesitan mostrar caracteres que HTML usa como parte de su sintaxis, deben usar entidades.

| Entidad | Carácter | Descripción |
|---|---|---|
| `&lt;` | < | Menor que |
| `&gt;` | > | Mayor que |
| `&amp;` | & | Ampersand |
| `&quot;` | " | Comillas dobles |
| `&apos;` | ' | Comilla simple |
| `&copy;` | © | Símbolo de copyright |
| `&reg;` | ® | Marca registrada |
| `&nbsp;` | (espacio) | Espacio que no se rompe |
| `&ndash;` | – | Guión medio |
| `&mdash;` | — | Guión largo |

### Ejemplo

```html
<p>&copy; 2026 — Festival de Comida &amp; Cultura</p>
<p>Para escribir una etiqueta en texto: &lt;p&gt; es un párrafo.</p>
```

---

## Resumen visual: ¿Qué etiqueta necesito?

| Quiero... | Uso... |
|---|---|
| Estructurar el documento | `<html>`, `<head>`, `<body>` |
| Poner un título en la pestaña | `<title>` |
| Conectar un archivo CSS | `<link rel="stylesheet" href="...">` |
| Un título grande | `<h1>` a `<h6>` |
| Un párrafo de texto | `<p>` |
| Texto en negrita con importancia | `<strong>` |
| Texto en cursiva con énfasis | `<em>` |
| Un salto de línea | `<br>` |
| Una línea separadora | `<hr>` |
| Una lista con viñetas | `<ul>` + `<li>` |
| Una lista con números | `<ol>` + `<li>` |
| Un enlace/link | `<a href="...">` |
| Una imagen | `<img src="..." alt="...">` |
| Una tabla de datos | `<table>` + `<thead>` + `<tbody>` + `<tr>` + `<th>` + `<td>` |
| Un formulario | `<form>` + `<input>` + `<label>` + `<button>` |
| Un menú desplegable | `<select>` + `<option>` |
| Un campo de texto grande | `<textarea>` |
| Agrupar campos de formulario | `<fieldset>` + `<legend>` |
| El encabezado de la página | `<header>` |
| Un menú de navegación | `<nav>` |
| El contenido principal | `<main>` |
| Una sección temática | `<section>` |
| Contenido independiente | `<article>` |
| Contenido complementario | `<aside>` |
| El pie de página | `<footer>` |
| Agrupar elementos (bloque) | `<div>` |
| Resaltar texto dentro de una línea | `<span>` |
