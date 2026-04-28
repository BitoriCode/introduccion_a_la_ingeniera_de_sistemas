# Módulo 3: HTML + JavaScript — La combinación completa

## Integrando estructura y lógica

Ya conocemos HTML (la estructura) y JavaScript (la lógica). Ahora vamos a juntarlos para crear páginas web que **realmente hagan cosas**. Esta es la parte donde todo cobra sentido y donde van a ver cómo su código interactúa con el usuario.

> **Concepto clave:** Cuando JavaScript interactúa con el HTML, lo hace a través del **DOM** (Document Object Model). El DOM es la representación en memoria de todo el HTML de la página, organizado como un árbol de nodos que JavaScript puede leer y modificar.

---

## 1. ¿Qué es el DOM(Document Object Model)?

Cuando el navegador carga un archivo HTML, crea una estructura en memoria llamada **DOM**. Pueden visualizarlo como un árbol jerárquico:

```
document
└── html
    ├── head
    │   ├── meta
    │   └── title
    └── body
        ├── h1
        ├── p
        └── div
            ├── p
            └── button
```

JavaScript puede acceder a **cualquier nodo** de ese árbol, leer su contenido, modificarlo, eliminarlo o agregar nuevos nodos. Ahí es donde está el poder de esta combinación.

---

## 2. Seleccionar elementos del HTML

Lo primero que necesitamos hacer desde JavaScript es **encontrar** los elementos HTML que queremos manipular.

### Ejemplo HTML base

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>DOM en acción</title>
</head>
<body>
    <h1 id="titulo">¡Bienvenidos!</h1>
    <p class="info">Este es un párrafo con clase.</p>
    <p class="info">Este es otro párrafo con la misma clase.</p>
    <button id="btn-saludar">Saludar</button>
    <ul id="lista-frutas">
        <li>Mango</li>
        <li>Lulo</li>
        <li>Guanábana</li>
    </ul>

    <script src="app.js"></script>
</body>
</html>
```

### Métodos de selección

```javascript
// Por ID — retorna UN solo elemento
const titulo = document.getElementById("titulo");
console.log(titulo.textContent);  // "¡Bienvenidos!"

// Por selector CSS — retorna el PRIMER elemento que coincida
const primerParrafo = document.querySelector(".info");
console.log(primerParrafo.textContent);

// Por selector CSS — retorna TODOS los elementos que coincidan
const todosLosParrafos = document.querySelectorAll(".info");
console.log(todosLosParrafos.length);  // 2

// Recorrer todos los elementos seleccionados
todosLosParrafos.forEach(parrafo => {
    console.log(parrafo.textContent);
});
```

### Tabla resumen de selectores

| Método | Retorna | Ejemplo |
|---|---|---|
| `getElementById("id")` | Un elemento | `document.getElementById("titulo")` |
| `querySelector(".clase")` | Primer coincidencia | `document.querySelector(".info")` |
| `querySelector("#id")` | Primer coincidencia | `document.querySelector("#titulo")` |
| `querySelectorAll("selector")` | Todos los que coincidan | `document.querySelectorAll("li")` |

> **Consejo:** `querySelector` y `querySelectorAll` son los más versátiles porque aceptan **cualquier selector CSS**. Son los que más van a usar.

---

## 3. Modificar contenido y atributos

Una vez seleccionado un elemento, podemos cambiarle prácticamente todo:

### Cambiar texto

```javascript
const titulo = document.getElementById("titulo");

// textContent — solo texto plano
titulo.textContent = "¡Hola a todos!";

// innerHTML — puede incluir HTML (úsenlo con cuidado)
titulo.innerHTML = "¡Hola, <em>estudiantes</em>!";
```

> **Precaución con `innerHTML`:** Si insertan contenido que viene del usuario directamente en `innerHTML`, pueden abrir la puerta a ataques de tipo XSS (Cross-Site Scripting). Si el contenido viene del usuario, usen `textContent` para que sea texto plano y seguro.

### Cambiar atributos

```javascript
const enlace = document.querySelector("a");

// Obtener un atributo
console.log(enlace.getAttribute("href"));

// Cambiar un atributo
enlace.setAttribute("href", "https://nueva-url.com");
enlace.setAttribute("target", "_blank");

// Quitar un atributo
enlace.removeAttribute("target");
```

---

## 4. Eventos: haciendo que las cosas pasen

Los **eventos** son acciones que ocurren en la página (un clic, una tecla, el mouse moviéndose, etc.). Con JavaScript podemos **escuchar** esos eventos y reaccionar a ellos.

### addEventListener — La forma correcta

```javascript
const boton = document.getElementById("btn-saludar");

boton.addEventListener("click", function() {
    alert("¡Hola! Bienvenidos.");
});

// O con función flecha (más moderno):
boton.addEventListener("click", () => {
    alert("¡Hola! Bienvenidos.");
});
```

### Eventos más comunes

| Evento | ¿Cuándo se dispara? |
|---|---|
| `click` | Al hacer clic en el elemento |
| `dblclick` | Al hacer doble clic |
| `mouseover` | Cuando el mouse pasa por encima |
| `mouseout` | Cuando el mouse sale del elemento |
| `keydown` | Al presionar una tecla |
| `keyup` | Al soltar una tecla |
| `input` | Cuando cambia el valor de un campo de formulario |
| `change` | Cuando un campo pierde el foco después de cambiar |
| `submit` | Al enviar un formulario |
| `load` | Cuando la página termina de cargar |

### El objeto `event`

Cuando ocurre un evento, JavaScript nos da un objeto con información detallada:

```javascript
document.addEventListener("keydown", (event) => {
    console.log(`Tecla presionada: ${event.key}`);
    console.log(`Código de tecla: ${event.code}`);
});

const boton = document.getElementById("btn-saludar");
boton.addEventListener("click", (event) => {
    console.log(`Clic en posición X: ${event.clientX}, Y: ${event.clientY}`);
    console.log(`Elemento clickeado:`, event.target);
});
```

---

## 5. Crear y eliminar elementos dinámicamente

Podemos crear elementos HTML desde JavaScript y agregarlos a la página:

### Crear un nuevo elemento

```javascript
// 1. Crear el elemento
const nuevoParrafo = document.createElement("p");

// 2. Darle contenido
nuevoParrafo.textContent = "Este párrafo fue creado con JavaScript";

// 3. (Opcional) Agregarle clases o atributos
nuevoParrafo.classList.add("dinamico");

// 4. Agregarlo al DOM
document.body.appendChild(nuevoParrafo);
```

### Agregar elementos a una lista

```javascript
const lista = document.getElementById("lista-frutas");

const nuevaFruta = document.createElement("li");
nuevaFruta.textContent = "Maracuyá";
lista.appendChild(nuevaFruta);
```

### Eliminar un elemento

```javascript
const lista = document.getElementById("lista-frutas");
const primerElemento = lista.querySelector("li");

// Método moderno
primerElemento.remove();

// Método clásico (desde el padre)
// lista.removeChild(primerElemento);
```

### Ejemplo completo: Lista dinámica

```html
<!-- HTML -->
<input type="text" id="input-fruta" placeholder="Escriba una fruta">
<button id="btn-agregar">Agregar fruta</button>
<ul id="lista-frutas"></ul>
```

```javascript
// JavaScript
const inputFruta = document.getElementById("input-fruta");
const btnAgregar = document.getElementById("btn-agregar");
const listaFrutas = document.getElementById("lista-frutas");

btnAgregar.addEventListener("click", () => {
    const texto = inputFruta.value.trim();

    if (texto === "") {
        alert("Por favor, escriba algo primero");
        return;
    }

    const nuevaFruta = document.createElement("li");
    nuevaFruta.textContent = texto;
    listaFrutas.appendChild(nuevaFruta);

    inputFruta.value = "";  // Limpiar el campo
    inputFruta.focus();     // Volver a enfocar el campo
});
```

---

## 6. Formularios con JavaScript

Acá es donde se pone interesante. Podemos validar y manejar formularios completamente con JavaScript:

### Ejemplo: Formulario de registro

```html
<!-- HTML -->
<form id="formulario-registro">
    <div>
        <label for="nombre">Nombre completo:</label>
        <input type="text" id="nombre" name="nombre" required>
    </div>

    <div>
        <label for="correo">Correo electrónico:</label>
        <input type="email" id="correo" name="correo" required>
    </div>

    <div>
        <label for="edad">Edad:</label>
        <input type="number" id="edad" name="edad" min="15" max="99" required>
    </div>

    <div>
        <label for="carrera">Carrera:</label>
        <select id="carrera" name="carrera" required>
            <option value="">Seleccione...</option>
            <option value="sistemas">Ingeniería de Sistemas</option>
            <option value="industrial">Ingeniería Industrial</option>
            <option value="civil">Ingeniería Civil</option>
            <option value="electronica">Ingeniería Electrónica</option>
        </select>
    </div>

    <button type="submit">Registrarse</button>
</form>

<div id="resultado"></div>
```

```javascript
// JavaScript
const formulario = document.getElementById("formulario-registro");
const resultado = document.getElementById("resultado");

formulario.addEventListener("submit", (event) => {
    // Prevenir que el formulario se envíe y recargue la página
    event.preventDefault();

    // Obtener los valores
    const nombre = document.getElementById("nombre").value.trim();
    const correo = document.getElementById("correo").value.trim();
    const edad = parseInt(document.getElementById("edad").value);
    const carrera = document.getElementById("carrera").value;

    // Validaciones personalizadas
    if (nombre.length < 3) {
        alert("El nombre debe tener al menos 3 caracteres");
        return;
    }

    if (edad < 15 || edad > 99) {
        alert("La edad debe estar entre 15 y 99 años");
        return;
    }

    // Mostrar los datos en la página
    resultado.innerHTML = `
        <h3>Registro exitoso</h3>
        <p><strong>Nombre:</strong> ${escapeHTML(nombre)}</p>
        <p><strong>Correo:</strong> ${escapeHTML(correo)}</p>
        <p><strong>Edad:</strong> ${edad}</p>
        <p><strong>Carrera:</strong> ${escapeHTML(carrera)}</p>
    `;

    // Limpiar el formulario
    formulario.reset();
});

// Función auxiliar para prevenir inyección de HTML
function escapeHTML(texto) {
    const div = document.createElement("div");
    div.textContent = texto;
    return div.innerHTML;
}
```

> **Nota de seguridad:** Fíjense que usamos la función `escapeHTML()` para limpiar el texto antes de insertarlo en `innerHTML`. Esto previene ataques XSS (cuando alguien introduce código malicioso en los campos del formulario).

---

## 7. Ejemplo práctico: Calculadora interactiva

Vamos a armar un proyecto completo juntando todo lo que hemos aprendido:

### HTML (calculadora.html)

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora</title>
</head>
<body>
    <h1>Calculadora</h1>

    <div class="calculadora">
        <label for="numero1">Primer número:</label>
        <input type="number" id="numero1" placeholder="Ejemplo: 10" step="any">

        <label for="numero2">Segundo número:</label>
        <input type="number" id="numero2" placeholder="Ejemplo: 5" step="any">

        <label for="operacion">Operación:</label>
        <select id="operacion">
            <option value="suma">Suma (+)</option>
            <option value="resta">Resta (-)</option>
            <option value="multiplicacion">Multiplicación (x)</option>
            <option value="division">División (/)</option>
        </select>

        <button id="btn-calcular">Calcular</button>

        <div id="resultado"></div>
    </div>

    <div id="historial">
        <h3>Historial de operaciones</h3>
        <ul id="lista-historial"></ul>
        <button id="btn-limpiar">
            Limpiar historial
        </button>
    </div>

    <script src="calculadora.js"></script>
</body>
</html>
```

### JavaScript (calculadora.js)

```javascript
// Seleccionar elementos del DOM
const inputNum1 = document.getElementById("numero1");
const inputNum2 = document.getElementById("numero2");
const selectOperacion = document.getElementById("operacion");
const btnCalcular = document.getElementById("btn-calcular");
const divResultado = document.getElementById("resultado");
const listaHistorial = document.getElementById("lista-historial");
const btnLimpiar = document.getElementById("btn-limpiar");

// Arreglo para guardar el historial
const historial = [];

// Función principal de cálculo
function calcular(a, b, operacion) {
    switch (operacion) {
        case "suma":
            return { resultado: a + b, simbolo: "+" };
        case "resta":
            return { resultado: a - b, simbolo: "-" };
        case "multiplicacion":
            return { resultado: a * b, simbolo: "x" };
        case "division":
            if (b === 0) {
                return { error: "No se puede dividir entre cero" };
            }
            return { resultado: a / b, simbolo: "/" };
        default:
            return { error: "Operación no válida" };
    }
}

// Función para mostrar el resultado
function mostrarResultado(mensaje, esError) {
    divResultado.textContent = mensaje;
}

// Función para agregar al historial
function agregarAlHistorial(texto) {
    historial.push(texto);

    const li = document.createElement("li");
    li.textContent = texto;
    listaHistorial.appendChild(li);
}

// Evento del botón calcular
btnCalcular.addEventListener("click", () => {
    const num1 = parseFloat(inputNum1.value);
    const num2 = parseFloat(inputNum2.value);
    const operacion = selectOperacion.value;

    // Validar que sean números
    if (isNaN(num1) || isNaN(num2)) {
        mostrarResultado("Ingrese números válidos en ambos campos", true);
        return;
    }

    // Calcular
    const resultado = calcular(num1, num2, operacion);

    if (resultado.error) {
        mostrarResultado(resultado.error, true);
        return;
    }

    // Redondear a máximo 4 decimales para mayor claridad
    const valorFinal = parseFloat(resultado.resultado.toFixed(4));
    const textoOperacion = `${num1} ${resultado.simbolo} ${num2} = ${valorFinal}`;

    mostrarResultado(`Resultado: ${valorFinal}`, false);
    agregarAlHistorial(textoOperacion);
});

// Evento para limpiar el historial
btnLimpiar.addEventListener("click", () => {
    historial.length = 0;
    listaHistorial.innerHTML = "";
    divResultado.textContent = "";
    inputNum1.value = "";
    inputNum2.value = "";
    inputNum1.focus();
});

// Permitir calcular con la tecla Enter
document.addEventListener("keydown", (event) => {
    if (event.key === "Enter") {
        btnCalcular.click();
    }
});
```

---

## 8. Ejemplo práctico: Lista de tareas (To-Do List)

Este es un clásico del desarrollo web. Vamos a hacer una lista de tareas completa:

### HTML (tareas.html)

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mis Tareas</title>
</head>
<body>
    <div class="contenedor">
        <h1>Mis Tareas</h1>

        <div class="input-grupo">
            <input type="text" id="input-tarea" placeholder="¿Qué hay que hacer?">
            <button id="btn-agregar">Agregar</button>
        </div>

        <div class="filtros">
            <button class="activo" data-filtro="todas">Todas</button>
            <button data-filtro="pendientes">Pendientes</button>
            <button data-filtro="completadas">Completadas</button>
        </div>

        <ul id="lista-tareas"></ul>

        <p class="contador" id="contador"></p>
    </div>

    <script src="tareas.js"></script>
</body>
</html>
```

### JavaScript (tareas.js)

```javascript
// === ELEMENTOS DEL DOM ===
const inputTarea = document.getElementById("input-tarea");
const btnAgregar = document.getElementById("btn-agregar");
const listaTareas = document.getElementById("lista-tareas");
const contador = document.getElementById("contador");
const filtros = document.querySelectorAll(".filtros button");

// === ESTADO DE LA APLICACIÓN ===
let tareas = [];
let filtroActual = "todas";

// === FUNCIONES ===

// Generar un ID único simple
function generarId() {
    return Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
}

// Agregar una tarea nueva
function agregarTarea() {
    const texto = inputTarea.value.trim();

    if (texto === "") {
        alert("Por favor, escriba una tarea primero");
        return;
    }

    const nuevaTarea = {
        id: generarId(),
        texto: texto,
        completada: false
    };

    tareas.push(nuevaTarea);
    inputTarea.value = "";
    inputTarea.focus();

    renderizarTareas();
}

// Alternar el estado de completada
function toggleTarea(id) {
    const tarea = tareas.find(t => t.id === id);
    if (tarea) {
        tarea.completada = !tarea.completada;
        renderizarTareas();
    }
}

// Eliminar una tarea
function eliminarTarea(id) {
    tareas = tareas.filter(t => t.id !== id);
    renderizarTareas();
}

// Filtrar tareas según el filtro activo
function obtenerTareasFiltradas() {
    switch (filtroActual) {
        case "pendientes":
            return tareas.filter(t => !t.completada);
        case "completadas":
            return tareas.filter(t => t.completada);
        default:
            return tareas;
    }
}

// Renderizar (dibujar) las tareas en el DOM
function renderizarTareas() {
    // Limpiar la lista actual
    listaTareas.innerHTML = "";

    const tareasFiltradas = obtenerTareasFiltradas();

    tareasFiltradas.forEach(tarea => {
        const li = document.createElement("li");
        if (tarea.completada) {
            li.classList.add("completada");
        }

        // Texto de la tarea (clic para completar/descompletar)
        const spanTexto = document.createElement("span");
        spanTexto.classList.add("tarea-texto");
        spanTexto.textContent = tarea.texto;
        spanTexto.addEventListener("click", () => toggleTarea(tarea.id));

        // Botón de eliminar
        const btnEliminar = document.createElement("button");
        btnEliminar.classList.add("btn-eliminar");
        btnEliminar.textContent = "X";
        btnEliminar.addEventListener("click", () => eliminarTarea(tarea.id));

        li.appendChild(spanTexto);
        li.appendChild(btnEliminar);
        listaTareas.appendChild(li);
    });

    // Actualizar el contador
    const pendientes = tareas.filter(t => !t.completada).length;
    const total = tareas.length;
    contador.textContent = `${pendientes} pendiente(s) de ${total} tarea(s)`;
}

// === EVENTOS ===

// Botón agregar
btnAgregar.addEventListener("click", agregarTarea);

// Tecla Enter para agregar
inputTarea.addEventListener("keydown", (event) => {
    if (event.key === "Enter") {
        agregarTarea();
    }
});

// Filtros
filtros.forEach(boton => {
    boton.addEventListener("click", () => {
        // Quitar clase activo de todos
        filtros.forEach(b => b.classList.remove("activo"));
        // Agregar clase activo al botón clickeado
        boton.classList.add("activo");
        // Cambiar el filtro actual
        filtroActual = boton.getAttribute("data-filtro");
        // Renderizar con el nuevo filtro
        renderizarTareas();
    });
});

// Renderizar inicial
renderizarTareas();
```

---

## 9. Almacenamiento local (localStorage)

¿No sería bueno que las tareas no se perdieran al recargar la página? Para eso existe `localStorage`:

```javascript
// Guardar datos
localStorage.setItem("nombre", "Camila");
localStorage.setItem("edad", "22");

// Recuperar datos
const nombre = localStorage.getItem("nombre");
console.log(nombre);  // "Camila"

// Guardar un arreglo u objeto (hay que convertirlo a texto JSON)
const tareas = [
    { texto: "Estudiar", completada: false },
    { texto: "Hacer ejercicio", completada: true }
];
localStorage.setItem("tareas", JSON.stringify(tareas));

// Recuperar un arreglo u objeto
const tareasRecuperadas = JSON.parse(localStorage.getItem("tareas"));
console.log(tareasRecuperadas);

// Eliminar un dato
localStorage.removeItem("nombre");

// Limpiar todo el localStorage
localStorage.clear();
```

### Bonus: Agregar persistencia a la lista de tareas

Si quieren que la lista de tareas del ejemplo anterior se guarde entre recargas, agreguen estas funciones al archivo `tareas.js`:

```javascript
// Guardar tareas en localStorage
function guardarTareas() {
    localStorage.setItem("misTareas", JSON.stringify(tareas));
}

// Cargar tareas desde localStorage
function cargarTareas() {
    const tareasGuardadas = localStorage.getItem("misTareas");
    if (tareasGuardadas) {
        tareas = JSON.parse(tareasGuardadas);
    }
}

// Modifiquen renderizarTareas para que también guarde:
// Al final de la función renderizarTareas(), agreguen:
// guardarTareas();

// Y al inicio del archivo, carguen las tareas guardadas:
// cargarTareas();
// renderizarTareas();
```

---

## 10. Buenas prácticas y consejos finales

### Organización del código

```
mi-proyecto/
├── index.html          <- Estructura
├── js/
│   └── app.js          <- Lógica
└── img/
    └── logo.png        <- Imágenes
```

### Consejos que les van a servir a lo largo de su formación

1. **Separen las responsabilidades:** HTML para estructura, JS para lógica. Eviten mezclarlos.

2. **Usen nombres descriptivos:** `btnEnviar` es mejor que `b1`. `listaEstudiantes` es mejor que `arr`.

3. **Comenten su código:** Especialmente cuando están aprendiendo. Un comentario de una línea puede ahorrar horas de confusión.

4. **Prueben en la consola:** Antes de escribir código complejo, prueben las ideas en la consola del navegador.

5. **No le tengan miedo a los errores:** Los errores son normales y son sus mejores maestros. Lean el mensaje de error con calma.

6. **Usen `textContent` en vez de `innerHTML`** cuando solo necesiten insertar texto plano. Es más seguro.

7. **Siempre validen los datos del usuario:** Nunca confíen en que el usuario va a escribir lo correcto.

---

## Proyecto final sugerido

### "Directorio de Estudiantes"

Creen una página web que permita:

1. **Registrar estudiantes** con un formulario (nombre, correo, carrera, semestre).
2. **Mostrar** los estudiantes en una tabla dinámica.
3. **Buscar** estudiantes por nombre o carrera.
4. **Eliminar** estudiantes de la lista.
5. **Guardar** los datos en `localStorage` para que no se pierdan.

Esto combina todo lo que aprendimos: formularios HTML, manipulación del DOM, eventos, arreglos, objetos y almacenamiento local.

> **Reto extra:** Agreguen la opción de editar un estudiante existente.

---

## Recursos recomendados

- [MDN Web Docs - DOM](https://developer.mozilla.org/es/docs/Web/API/Document_Object_Model) — Documentación del DOM en español.
- [MDN Web Docs - Eventos](https://developer.mozilla.org/es/docs/Web/Events) — Lista completa de eventos del navegador.
- [JavaScript30](https://javascript30.com/) — 30 proyectos prácticos en 30 días (en inglés, pero muy buenos).

---

## Resumen general del módulo

| Módulo | Qué aprendimos |
|---|---|
| **HTML** | Estructura de documentos, etiquetas de texto, listas, tablas, formularios, HTML semántico |
| **JavaScript** | Variables, tipos de datos, operadores, condicionales, ciclos, funciones, arrays, objetos |
| **HTML + JS** | DOM, selección de elementos, eventos, manipulación dinámica, formularios interactivos, localStorage |

---

## Cierre del módulo

Llegaron hasta el final del módulo de desarrollo web. Ya tienen las herramientas fundamentales para crear páginas web interactivas. Esto es apenas el comienzo — si les gustó, exploren más sobre APIs, frameworks, y sigan construyendo proyectos propios. La práctica constante es lo que hace la diferencia.
