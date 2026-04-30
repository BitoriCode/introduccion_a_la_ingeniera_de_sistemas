# Ejercicios — HTML y JavaScript juntos

## Indicaciones generales

Este archivo contiene **5 ejercicios** progresivos que combinan HTML y JavaScript. Cada ejercicio es un poco más desafiante que el anterior.

- Cada ejercicio trae el **HTML completo** y un **JS con código parcial**. Su trabajo es completar los `TODO`.
- No borren ni muevan el código que ya está escrito, solo llenen los espacios que faltan.
- Para cada ejercicio creen una carpeta independiente. Ejemplo: `ejercicio-01/index.html` y `ejercicio-01/script.js`.

> **Consejo:** lean todo el código dado antes de escribir algo. Entender lo que ya existe es la mitad del trabajo.

---

## Ejercicio 1 — Mi primer evento *(el más guiado)*

**Objetivo:** Seleccionar un elemento del DOM y cambiar su texto al hacer clic en un botón.

**Enunciado:** La página tiene un párrafo que dice "Esperando..." y un botón. Al hacer clic, el párrafo debe cambiar a "¡Hola desde JavaScript!".

**Pasos:**
1. Selecciona el párrafo con `getElementById`.
2. Selecciona el botón con `getElementById`.
3. Agrega un `addEventListener("click", ...)` al botón.
4. Dentro del listener, cambia el `textContent` del párrafo.

**index.html** *(ya está completo, no lo modifiquen)*

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi primer evento</title>
</head>
<body>
  <h2>Mi primer evento</h2>
  <p id="mensaje">Esperando...</p>
  <button id="btn-saludar">Saludar</button>

  <script src="script.js"></script>
</body>
</html>
```

**script.js** *(completen los TODO)*

```js
// Paso 1: seleccionar el párrafo por su id "mensaje"
const parrafo = document.getElementById("mensaje");

// Paso 2: seleccionar el botón por su id "btn-saludar"
// TODO: const boton = ...

// Paso 3: agregar el evento click al botón
// TODO: boton.addEventListener("click", function() {
//         // Paso 4: cambiar el textContent del párrafo
//       });
```

**Qué practicamos:** `getElementById`, `addEventListener("click")`, `textContent`.

---

## Ejercicio 2 — Saludo personalizado

**Objetivo:** Leer el valor de un campo de texto y mostrarlo en la página usando template literals.

**Enunciado:** La página tiene un campo de texto donde el usuario escribe su nombre, y un botón "Saludar". Al hacer clic, debe aparecer el mensaje "¡Hola, [nombre]! Bienvenido." Si el campo está vacío, mostrar "Por favor escribe tu nombre."

**Pasos:**
1. Selecciona el input, el botón y el párrafo de resultado.
2. En el listener del botón, lee el valor del input con `.value`.
3. Usa un `if` para revisar si el valor está vacío.
4. Muestra el mensaje con un template literal.

**index.html** *(ya está completo)*

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Saludo personalizado</title>
</head>
<body>
  <h2>Saludo personalizado</h2>
  <label for="nombre">Tu nombre:</label>
  <input type="text" id="nombre" placeholder="Escribe tu nombre">
  <button id="btn-saludar">Saludar</button>
  <p id="resultado"></p>

  <script src="script.js"></script>
</body>
</html>
```

**script.js** *(completen los TODO)*

```js
// Seleccionamos los tres elementos que necesitamos
const inputNombre = document.getElementById("nombre");
const btnSaludar  = document.getElementById("btn-saludar");
const resultado   = document.getElementById("resultado");

btnSaludar.addEventListener("click", function() {
  // TODO: leer el valor del input y guardarlo en una variable
  // Pista: const nombre = inputNombre.value;

  // TODO: si el nombre está vacío, mostrar "Por favor escribe tu nombre."
  //       de lo contrario, mostrar "¡Hola, [nombre]! Bienvenido."
  // Pista: usa un if/else y template literals (`¡Hola, ${nombre}!...`)
});
```

**Qué practicamos:** `.value`, template literals, `if/else`, `textContent`.

---

## Ejercicio 3 — Calculadora de propina

**Objetivo:** Leer dos campos numéricos, usar una función con parámetros y `return`, y mostrar el resultado.

**Enunciado:** La página tiene un campo para el valor de la cuenta y un campo para el porcentaje de propina. Al hacer clic en "Calcular", debe mostrarse cuánto es la propina y cuánto es el total. Si alguno de los campos no tiene un número válido, mostrar un mensaje de error.

- Propina = cuenta × (porcentaje / 100)
- Total = cuenta + propina

**Pasos:**
1. Lee los dos valores con `parseFloat`.
2. Valida con `isNaN` que ambos sean números.
3. Crea una función `calcularPropina(cuenta, porcentaje)` que retorne el valor de la propina.
4. Muestra la propina y el total en los párrafos de resultado.

**index.html** *(ya está completo)*

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Calculadora de propina</title>
</head>
<body>
  <h2>Calculadora de propina</h2>

  <label for="cuenta">Valor de la cuenta ($):</label>
  <input type="number" id="cuenta" placeholder="Ej: 50000">

  <label for="porcentaje">Propina (%):</label>
  <input type="number" id="porcentaje" placeholder="Ej: 10">

  <button id="btn-calcular">Calcular</button>

  <p id="resultado-propina"></p>
  <p id="resultado-total"></p>

  <script src="script.js"></script>
</body>
</html>
```

**script.js** *(completen los TODO)*

```js
// TODO: crea la función calcularPropina que reciba cuenta y porcentaje
//       y retorne el valor de la propina
// Pista: function calcularPropina(cuenta, porcentaje) {
//          return cuenta * (porcentaje / 100);
//        }

const btnCalcular       = document.getElementById("btn-calcular");
const resultadoPropina  = document.getElementById("resultado-propina");
const resultadoTotal    = document.getElementById("resultado-total");

btnCalcular.addEventListener("click", function() {
  // TODO: leer los valores de los dos inputs con parseFloat
  // Pista: const cuenta     = parseFloat(document.getElementById("cuenta").value);
  //        const porcentaje = parseFloat(document.getElementById("porcentaje").value);

  // TODO: validar que ambos sean números con isNaN
  // Pista: if (isNaN(cuenta) || isNaN(porcentaje)) { ... }

  // TODO: llamar a calcularPropina y calcular el total
  // Pista: const propina = calcularPropina(cuenta, porcentaje);
  //        const total   = cuenta + propina;

  // TODO: mostrar los resultados en los párrafos
  // Pista: resultadoPropina.textContent = `Propina: $${propina.toFixed(0)}`;
  //        resultadoTotal.textContent   = `Total:   $${total.toFixed(0)}`;
});
```

**Qué practicamos:** funciones con `return`, `parseFloat`, `isNaN`, `.toFixed`.

---

## Ejercicio 4 — Mostrar y ocultar información

**Objetivo:** Alternar la visibilidad de un elemento usando una variable booleana y `style.display`.

**Enunciado:** La página muestra una tarjeta con información de contacto que inicialmente está oculta. Hay un botón que dice "Mostrar datos". Al hacer clic, la tarjeta se muestra y el botón cambia a "Ocultar datos". Al volver a hacer clic, se oculta de nuevo y el texto del botón regresa a "Mostrar datos".

**Pasos:**
1. Crea una variable `let visible = false` para recordar el estado.
2. En el listener, usa un `if/else` según el valor de `visible`.
3. Si `visible` es `false`: cambia `style.display` de la tarjeta a `"block"` y actualiza el texto del botón.
4. Si `visible` es `true`: cambia `style.display` a `"none"` y regresa el texto del botón.
5. Al final de cada caso, invierte el valor de `visible`.

**index.html** *(ya está completo)*

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mostrar y ocultar</title>
</head>
<body>
  <h2>Contacto</h2>
  <button id="btn-toggle">Mostrar datos</button>

  <div id="tarjeta" style="display: none; border: 1px solid #ccc; padding: 1em; margin-top: 1em;">
    <p><strong>Nombre:</strong> Soporte técnico</p>
    <p><strong>Correo:</strong> soporte@universidad.edu.co</p>
    <p><strong>Teléfono:</strong> 601 234 5678</p>
  </div>

  <script src="script.js"></script>
</body>
</html>
```

**script.js** *(completen los TODO)*

```js
const btnToggle = document.getElementById("btn-toggle");
const tarjeta   = document.getElementById("tarjeta");

// Esta variable recuerda si la tarjeta está visible o no
let visible = false;

btnToggle.addEventListener("click", function() {
  if (visible === false) {
    // TODO: mostrar la tarjeta cambiando su style.display a "block"
    // TODO: cambiar el texto del botón a "Ocultar datos"
    visible = true;
  } else {
    // TODO: ocultar la tarjeta cambiando su style.display a "none"
    // TODO: cambiar el texto del botón a "Mostrar datos"
    visible = false;
  }
});
```

**Qué practicamos:** variable booleana de estado, `style.display`, `if/else`, `textContent` en un botón.

---

## Ejercicio 5 — Lista de favoritos

**Objetivo:** Agregar elementos a un array y mostrar la lista actualizada en la página.

**Enunciado:** La página tiene un campo de texto y un botón "Agregar". El usuario escribe una película (o canción, o lo que quiera) y al hacer clic aparece en una lista. Si el campo está vacío, mostrar el mensaje "Escribe algo antes de agregar." El campo se limpia automáticamente después de agregar.

**Pasos:**
1. Crea un array `let favoritos = []`.
2. En el listener, lee el valor del input y valida que no esté vacío.
3. Si hay valor, agrégalo al array con `.push()` y limpia el input (`input.value = ""`).
4. Llama a una función `mostrarLista()` que actualice el contenido del `<ul>`.
5. En `mostrarLista()`, recorre el array con `forEach` y construye el HTML de la lista.

**index.html** *(ya está completo)*

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Lista de favoritos</title>
</head>
<body>
  <h2>Mi lista de favoritos</h2>

  <label for="item">Agregar:</label>
  <input type="text" id="item" placeholder="Ej: Inception">
  <button id="btn-agregar">Agregar</button>
  <p id="aviso"></p>

  <ul id="lista"></ul>

  <script src="script.js"></script>
</body>
</html>
```

**script.js** *(completen los TODO)*

```js
let favoritos = [];

const inputItem  = document.getElementById("item");
const btnAgregar = document.getElementById("btn-agregar");
const aviso      = document.getElementById("aviso");
const lista      = document.getElementById("lista");

// Esta función recorre el array y actualiza el <ul> en la página
function mostrarLista() {
  // Limpiar lo que había antes
  lista.innerHTML = "";

  // TODO: recorrer el array favoritos con forEach y por cada elemento
  //       crear un <li> con su nombre y agregarlo al <ul>
  // Pista: favoritos.forEach(function(item) {
  //          const li = document.createElement("li");
  //          li.textContent = item;
  //          lista.appendChild(li);
  //        });
}

btnAgregar.addEventListener("click", function() {
  const texto = inputItem.value.trim();

  // TODO: si texto está vacío, mostrar "Escribe algo antes de agregar." en el párrafo aviso y salir con return

  // Si hay texto, limpia el aviso
  aviso.textContent = "";

  // TODO: agregar texto al array favoritos con .push()

  // TODO: limpiar el input (inputItem.value = "")

  // TODO: llamar a mostrarLista() para actualizar la página
});
```

**Qué practicamos:** arrays, `.push()`, `forEach`, `createElement`, `appendChild`, limpiar y redibujar una lista.

**Enunciado:** Crear una página con un número visible en pantalla y tres botones: uno para sumar 1, uno para restar 1 y uno para reiniciar el contador a 0.

### Solución

**index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contador</title>
</head>
<body>

  <h2>Contador interactivo</h2>
  <p id="display">0</p>
  <button id="btn-sumar">+ Sumar</button>
  <button id="btn-restar">− Restar</button>
  <button id="btn-reiniciar">Reiniciar</button>

  <script src="script.js"></script>
</body>
</html>
```

**script.js**

```js
// Variable que guarda el valor actual del contador
let cuenta = 0;

// Seleccionamos el elemento donde se muestra el número
const display = document.getElementById("display");
const btnSumar = document.getElementById("btn-sumar")
const btnRestar = document.getElementById("btn-restar")
const btnReiniciar = document.getElementById("btn-reiniciar")

// Función que actualiza el texto en pantalla
function actualizar() {
  display.textContent = cuenta;
}

// Cada botón tiene su propio listener
btnSumar.addEventListener("click", function () {
  cuenta++;
  actualizar();
});

btnRestar.addEventListener("click", function () {
  cuenta--;
  actualizar();
});

btnReiniciar.addEventListener("click", function () {
  cuenta = 0;
  actualizar();
});
```

**Qué practicamos:** variable de estado (`let cuenta`), `getElementById`, `addEventListener`, `textContent`.

---

## Ejercicio 2 — Conversor de temperatura *(resuelto)*

**Objetivo:** Practicar funciones con parámetros y `return`, lectura de valores desde el DOM y manejo de `<select>`.

**Enunciado:** Crear una página con un campo numérico, un menú desplegable para elegir el tipo de conversión y un botón. Al hacer clic, mostrar el resultado en la página. Si el campo está vacío o no es un número, mostrar un mensaje de error.

Conversiones disponibles:
- Celsius → Fahrenheit: `(c × 9/5) + 32`
- Fahrenheit → Celsius: `(f − 32) × 5/9`
- Celsius → Kelvin: `c + 273.15`

### Solución

**index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Conversor de temperatura</title>
</head>
<body>

  <h2>Conversor de temperatura</h2>

  <label for="valor">Temperatura:</label>
  <input type="number" id="valor" placeholder="Ej: 100">

  <label for="tipo">Convertir de:</label>
  <select id="tipo">
    <option value="c-f">Celsius → Fahrenheit</option>
    <option value="f-c">Fahrenheit → Celsius</option>
    <option value="c-k">Celsius → Kelvin</option>
  </select>

  <button id="btn-convertir">Convertir</button>
  <p id="resultado"></p>

  <script src="script.js"></script>
</body>
</html>
```

**script.js**

```js
// Cada fórmula está en su propia función con parámetro y return
function celsiusAFahrenheit(c) {
  return (c * 9 / 5) + 32;
}

function fahrenheitACelsius(f) {
  return (f - 32) * 5 / 9;
}

function celsiusAKelvin(c) {
  return c + 273.15;
}

// Esta función decide cuál fórmula usar según el tipo elegido
function convertir(valor, tipo) {
  if (tipo === "c-f") return celsiusAFahrenheit(valor);
  if (tipo === "f-c") return fahrenheitACelsius(valor);
  if (tipo === "c-k") return celsiusAKelvin(valor);
}

document.getElementById("btn-convertir").addEventListener("click", function () {
  const valor = parseFloat(document.getElementById("valor").value);
  const tipo = document.getElementById("tipo").value;
  const resultado = document.getElementById("resultado");

  // Validación: el campo debe tener un número real
  if (isNaN(valor)) {
    resultado.textContent = "Por favor ingresa un número válido.";
    return;
  }

  const convertido = convertir(valor, tipo);
  resultado.textContent = `Resultado: ${convertido.toFixed(2)}`;
});
```

**Qué practicamos:** funciones con `return`, `parseFloat`, `isNaN`, `<select>` + `.value`, `toFixed`.

---

## Ejercicio 3 — Lista de tareas

**Objetivo:** Practicar manipulación dinámica del DOM, arrays y renderizado con `createElement`.

**Enunciado:** Crear una página con un campo de texto y un botón "Agregar". Cada tarea que el usuario escriba debe aparecer en una lista debajo. Cada elemento de la lista debe tener un botón "Eliminar" que lo borre.

**Requisitos:**
- Si el campo está vacío al hacer clic, mostrar el mensaje: *"Escribe una tarea antes de agregar."*
- También debe ser posible agregar presionando la tecla `Enter`.
- Las tareas se guardan en un array y la lista se redibuja completa cada vez que cambia el array.

**Pistas:**
- Usa un array `let tareas = []` para guardar las tareas.
- Crea una función `renderizar()` que borre el contenido del `<ul>` y lo vuelva a dibujar desde el array.
- Dentro de `renderizar()`, usa `createElement("li")` y `createElement("button")` para construir cada fila.
- Para el botón Eliminar, usa `tareas.splice(indice, 1)` y llama a `renderizar()` de nuevo.
- Para detectar `Enter`, agrega un `addEventListener("keydown", ...)` al input y revisa `event.key === "Enter"`.

---

## Ejercicio 4 — Formulario con validación

**Objetivo:** Practicar `event.preventDefault()`, validación de múltiples campos y feedback visible por campo.

**Enunciado:** Crear un formulario de registro con los siguientes campos:

| Campo | Tipo | Regla de validación |
|---|---|---|
| Nombre | texto | Mínimo 3 caracteres |
| Correo | email | Debe contener `@` y `.` |
| Edad | número | Entre 16 y 99 |
| Acepto los términos | checkbox | Debe estar marcado |

Al hacer clic en Enviar:
- Usar `event.preventDefault()` para que la página no se recargue.
- Revisar cada campo con JavaScript (no solo con `required`).
- Mostrar un mensaje de error en rojo **debajo de cada campo** que falle.
- Si todo es válido, mostrar un mensaje de éxito en verde y limpiar el formulario con `form.reset()`.

**Pistas:**
- Coloca un `<span id="error-nombre"></span>` debajo de cada campo para mostrar los errores.
- Antes de validar, limpia todos los mensajes de error (`span.textContent = ""`).
- Para el correo puedes usar: `correo.includes("@") && correo.includes(".")`.
- Para el checkbox: `document.getElementById("terminos").checked`.

### Código parcial

Este ejercicio usa dos patrones que no aparecen en los ejemplos anteriores: mostrar errores **por campo** en lugar de con `alert`, y usar `form.reset()`. El HTML y el esqueleto del JS ya están listos; completen los `TODO`.

**index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Formulario con validación</title>
  <style>
    .error { color: red; font-size: 0.85em; }
    .exito { color: green; }
  </style>
</head>
<body>

  <h2>Registro de usuario</h2>

  <form id="formulario">
    <div>
      <label for="nombre">Nombre:</label>
      <input type="text" id="nombre">
      <span class="error" id="error-nombre"></span>
    </div>
    <div>
      <label for="correo">Correo:</label>
      <input type="text" id="correo">
      <span class="error" id="error-correo"></span>
    </div>
    <div>
      <label for="edad">Edad:</label>
      <input type="number" id="edad">
      <span class="error" id="error-edad"></span>
    </div>
    <div>
      <input type="checkbox" id="terminos">
      <label for="terminos">Acepto los términos</label>
      <span class="error" id="error-terminos"></span>
    </div>
    <button type="submit">Enviar</button>
  </form>

  <p class="exito" id="mensaje-exito"></p>

  <script src="script.js"></script>
</body>
</html>
```

**script.js**

```js
// Seleccionar el formulario y todos los campos
const form          = document.getElementById("formulario");
const inputNombre   = document.getElementById("nombre");
const inputCorreo   = document.getElementById("correo");
const inputEdad     = document.getElementById("edad");
const chkTerminos   = document.getElementById("terminos");

// Seleccionar los spans donde van a aparecer los errores
const errorNombre   = document.getElementById("error-nombre");
const errorCorreo   = document.getElementById("error-correo");
const errorEdad     = document.getElementById("error-edad");
const errorTerminos = document.getElementById("error-terminos");
const msgExito      = document.getElementById("mensaje-exito");

form.addEventListener("submit", function(event) {
  // Evitar que la página se recargue
  event.preventDefault();

  // Limpiar todos los mensajes antes de validar de nuevo
  errorNombre.textContent   = "";
  errorCorreo.textContent   = "";
  errorEdad.textContent     = "";
  errorTerminos.textContent = "";
  msgExito.textContent      = "";

  let hayErrores = false;

  // TODO: Validar nombre — mínimo 3 caracteres
  // Pista: const nombre = inputNombre.value.trim();
  //        if (nombre.length < 3) { ... }

  // TODO: Validar correo — debe contener "@" y "."
  // Pista: const correo = inputCorreo.value.trim();
  //        if (!correo.includes("@") || !correo.includes(".")) { ... }

  // TODO: Validar edad — entre 16 y 99
  // Pista: const edad = parseInt(inputEdad.value);
  //        if (isNaN(edad) || edad < 16 || edad > 99) { ... }

  // TODO: Validar checkbox
  // Pista: if (!chkTerminos.checked) { ... }

  // Si todo está bien, mostrar éxito y limpiar el formulario
  if (!hayErrores) {
    msgExito.textContent = "¡Registro exitoso!";
    // TODO: llama form.reset() para limpiar todos los campos
  }
});
```

---

## Ejercicio 5 — Buscador en vivo

**Objetivo:** Practicar el evento `input`, el método `filter`, `toLowerCase` y renderizado dinámico de una tabla.

**Enunciado:** Tienes la siguiente lista de productos definida en el código. Crear una página que muestre todos los productos en una tabla y que filtre los resultados en tiempo real mientras el usuario escribe en un campo de búsqueda.

```js
const productos = [
  { nombre: "Manzana",    categoria: "Frutas" },
  { nombre: "Banano",     categoria: "Frutas" },
  { nombre: "Zanahoria",  categoria: "Verduras" },
  { nombre: "Espinaca",   categoria: "Verduras" },
  { nombre: "Leche",      categoria: "Lácteos" },
  { nombre: "Queso",      categoria: "Lácteos" },
  { nombre: "Arroz",      categoria: "Granos" },
  { nombre: "Lentejas",   categoria: "Granos" },
  { nombre: "Pollo",      categoria: "Carnes" },
  { nombre: "Atún",       categoria: "Carnes" }
];
```

**Requisitos:**
- Al cargar la página se muestran todos los productos en una tabla con columnas: **Nombre** y **Categoría**.
- Mientras el usuario escribe en el campo de búsqueda, la tabla se actualiza sin hacer clic en ningún botón.
- La búsqueda no distingue mayúsculas de minúsculas.
- Si no hay resultados, mostrar una fila con el texto *"No se encontraron productos."*

**Pistas:**
- Usa el evento `"input"` sobre el campo de búsqueda (no `"click"`).
- Filtra el array con `productos.filter(p => p.nombre.toLowerCase().includes(texto))`.
- Crea una función `renderizarTabla(lista)` que reciba el array filtrado y redibuje el `<tbody>`.
- Para limpiar el tbody antes de redibujar: `tbody.innerHTML = ""`.

### Código parcial

Este ejercicio usa dos cosas nuevas: el método `.filter()` sobre arrays y el patrón de **limpiar y redibujar** una tabla. El HTML está completo; en el JS completen los `TODO`.

**index.html**

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Buscador de productos</title>
</head>
<body>

  <h2>Buscador de productos</h2>
  <label for="busqueda">Buscar:</label>
  <input type="text" id="busqueda" placeholder="Escribe para filtrar...">

  <table id="tabla-productos">
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Categoría</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>

  <script src="script.js"></script>
</body>
</html>
```

**script.js**

```js
const productos = [
  { nombre: "Manzana",   categoria: "Frutas" },
  { nombre: "Banano",    categoria: "Frutas" },
  { nombre: "Zanahoria", categoria: "Verduras" },
  { nombre: "Espinaca",  categoria: "Verduras" },
  { nombre: "Leche",     categoria: "Lácteos" },
  { nombre: "Queso",     categoria: "Lácteos" },
  { nombre: "Arroz",     categoria: "Granos" },
  { nombre: "Lentejas",  categoria: "Granos" },
  { nombre: "Pollo",     categoria: "Carnes" },
  { nombre: "Atún",      categoria: "Carnes" }
];

const tbody        = document.querySelector("#tabla-productos tbody");
const campoBusqueda = document.getElementById("busqueda");

// Esta función recibe un array y dibuja las filas en el tbody
function renderizarTabla(lista) {
  // Limpiar las filas anteriores antes de redibujar
  tbody.innerHTML = "";

  if (lista.length === 0) {
    // TODO: Crear una fila que muestre "No se encontraron productos."
    // Pista: const fila = document.createElement("tr");
    //        fila.innerHTML = `<td colspan="2">No se encontraron productos.</td>`;
    //        tbody.appendChild(fila);
    return;
  }

  // Recorrer la lista y crear una fila <tr> por cada producto
  lista.forEach(function(producto) {
    const fila = document.createElement("tr");

    // TODO: Crear dos celdas <td>: una con producto.nombre y otra con producto.categoria
    // Pista: const celda = document.createElement("td");
    //        celda.textContent = producto.nombre;
    //        fila.appendChild(celda);

    tbody.appendChild(fila);
  });
}

// Mostrar todos los productos al cargar la página
renderizarTabla(productos);

// Filtrar en tiempo real mientras el usuario escribe
campoBusqueda.addEventListener("input", function() {
  const texto = campoBusqueda.value.toLowerCase();

  // TODO: Usar .filter() para quedarse solo con los productos que coincidan
  // Pista: const filtrados = productos.filter(function(p) {
  //          return p.nombre.toLowerCase().includes(texto);
  //        });
  //        renderizarTabla(filtrados);
});
```
