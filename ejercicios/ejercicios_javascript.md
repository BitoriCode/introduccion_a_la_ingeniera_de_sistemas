# Ejercicios de JavaScript — Fundamentos básicos

## Indicaciones generales

Estos ejercicios están pensados para practicar los fundamentos de JavaScript: **variables, tipos de datos, operadores, condicionales, ciclos, funciones y arreglos básicos**. No se requiere HTML ni manipulación del DOM, solo JavaScript puro.

Para cada ejercicio, creen un archivo `.js` y ejecútenlo de una de estas dos formas:
- Abriendo la consola del navegador (`F12` → pestaña **Console**) y pegando el código.
- Creando un archivo `.html` con un `<script>` que enlace al `.js` y revisando la consola.

> **Recuerden:** Usen `console.log()` para ver los resultados de cada ejercicio.

---

## Bloque 1: Variables, tipos de datos y operadores

---

### Ejercicio 1 — Presentación personal

**Dificultad:** Baja

**Enunciado:** Declaren tres variables: `nombre`, `edad` y `ciudad`. Asígnenles sus propios datos. Luego usen un **template literal** para imprimir en consola una frase como:

```
Hola, me llamo Camila, tengo 21 años y soy de Bogotá.
```

**Pistas:**
- Para los datos que no van a cambiar, usen `const`. Para los que podrían cambiar, `let`.
- Recuerden que los template literals usan backticks (`` ` ``) y `${}` para incrustar variables.

---

### Ejercicio 2 — La caja registradora

**Dificultad:** Baja

**Enunciado:** Un estudiante fue a la tienda y compró lo siguiente:
- Cuaderno: $4.500
- Lapicero: $1.200
- Borrador: $800
- Resaltador: $2.300

Declaren una variable para cada producto con su precio. Luego calculen e impriman en consola:
1. El total de la compra.
2. El total si le aplican un descuento del 10%.
3. El vuelto si pagó con un billete de $20.000.

**Pistas:**
- El descuento se calcula así: `total * 0.10` o `total * (10 / 100)`.
- El vuelto es `pago - totalConDescuento`.

---

### Ejercicio 3 — Verificador de tipos

**Dificultad:** Baja

**Enunciado:** Declaren las siguientes variables con estos valores exactos:
- `a = 42`
- `b = "42"`
- `c = true`
- `d = null`
- `e = undefined`
- `f = 3.14`

Luego, para cada una, impriman en consola el **valor** y su **tipo** (usando `typeof`), con un formato así:

```
a → valor: 42, tipo: number
b → valor: 42, tipo: string
...
```

Finalmente, impriman el resultado de `a == b` y `a === b` y expliquen (en un comentario en el código) por qué son diferentes.

---

## Bloque 2: Condicionales

---

### Ejercicio 4 — Clasificador de notas

**Dificultad:** Baja

**Enunciado:** Declaren una variable `nota` con un número entre 0 y 5. Usando `if / else if / else`, impriman en consola el concepto correspondiente según esta escala:

| Rango | Concepto |
|---|---|
| 4.6 – 5.0 | Excelente |
| 4.0 – 4.5 | Sobresaliente |
| 3.5 – 3.9 | Aceptable |
| 3.0 – 3.4 | Aprobó |
| 0 – 2.9 | Reprobó |

Prueben el código cambiando el valor de `nota` al menos 3 veces para verificar que funciona correctamente.

---

### Ejercicio 5 — ¿Qué día es hoy?

**Dificultad:** Baja

**Enunciado:** Declaren una variable `dia` con el nombre de un día de la semana (en minúsculas). Usando `switch`, impriman en consola un mensaje diferente para cada día. Por ejemplo:
- `"lunes"` → `"Inicio de semana, ánimo."`
- `"miercoles"` → `"Ya vamos por la mitad."`
- `"viernes"` → `"¡Por fin viernes!"`
- Para sábado y domingo, usen el mismo mensaje: `"Fin de semana, a descansar."`
- Para cualquier otro valor: `"Eso no es un día válido."`

**Pistas:**
- Recuerden el `break` después de cada `case`.
- Para que sábado y domingo compartan mensaje, pueden escribir dos `case` seguidos sin `break` entre ellos.

---

### Ejercicio 6 — Calculadora con validación

**Dificultad:** Media

**Enunciado:** Declaren tres variables: `num1`, `num2` y `operacion`. La operación puede ser `"suma"`, `"resta"`, `"multiplicacion"` o `"division"`. Usando `if / else if`, calculen el resultado e impriman:

```
10 + 5 = 15
```

Además, agreguen una validación: si la operación es `"division"` y `num2` es `0`, impriman un mensaje de error en lugar de hacer la división.

**Pistas:**
- Recuerden que dividir por cero en matemáticas no está definido.
- Pueden construir el mensaje con template literals: `` `${num1} + ${num2} = ${resultado}` ``

---

## Bloque 3: Ciclos

---

### Ejercicio 7 — Tabla de multiplicar

**Dificultad:** Baja

**Enunciado:** Declaren una variable `numero` con cualquier valor entre 1 y 12. Usando un ciclo `for`, impriman en consola la tabla de multiplicar completa de ese número, en este formato:

```
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
...
3 x 10 = 30
```

**Reto extra:** Modifiquen el código para que imprima las tablas del 1 al 10 usando un ciclo `for` dentro de otro (ciclos anidados).

---

### Ejercicio 8 — Números especiales

**Dificultad:** Media

**Enunciado:** Usando un ciclo `for` del 1 al 50, impriman en consola:
- Los **números pares**.
- Los **múltiplos de 3**.
- Los **números que son pares Y múltiplos de 3 al mismo tiempo**.

Cada grupo debe estar claramente separado con un título. Por ejemplo:

```
--- Números pares ---
2, 4, 6, 8...

--- Múltiplos de 3 ---
3, 6, 9, 12...

--- Pares y múltiplos de 3 ---
6, 12, 18...
```

**Pistas:**
- Un número es par si `numero % 2 === 0`.
- Un número es múltiplo de 3 si `numero % 3 === 0`.
- Para los dos al mismo tiempo, usen el operador `&&`.

---

### Ejercicio 9 — Cuenta regresiva

**Dificultad:** Baja

**Enunciado:** Usando un ciclo `while`, impriman una cuenta regresiva desde 10 hasta 0. El último mensaje debe ser `"¡Despegue!"`.

El resultado esperado en consola:
```
10
9
8
...
1
0
¡Despegue!
```

**Reto extra:** Modifiquen el ciclo para que también muestre si cada número es par o impar. Por ejemplo: `"10 - par"`, `"9 - impar"`, etc.

---

### Ejercicio 10 — Adivina el número

**Dificultad:** Media

**Enunciado:** Sin funciones ni interactividad por ahora, simulen el juego "adivina el número" de la siguiente forma:
- Definan un `numeroSecreto` con valor fijo (por ejemplo, `7`).
- Creen un arreglo de intentos: `[3, 8, 1, 7, 5]`.
- Usando un ciclo `for`, revisen cada intento. Para cada uno impriman:
  - Si es muy bajo: `"Intento X: demasiado bajo"`
  - Si es muy alto: `"Intento X: demasiado alto"`
  - Si es correcto: `"Intento X: ¡correcto! Encontrado en el intento N"`
- Cuando se encuentre el número correcto, el ciclo debe detenerse (usen `break`).

---

## Bloque 4: Funciones

---

### Ejercicio 11 — Conversor de temperaturas

**Dificultad:** Baja

**Enunciado:** Creen las siguientes tres funciones:

1. `celsiusAFahrenheit(celsius)` — Fórmula: `(celsius * 9/5) + 32`
2. `fahrenheitACelsius(fahrenheit)` — Fórmula: `(fahrenheit - 32) * 5/9`
3. `celsiusAKelvin(celsius)` — Fórmula: `celsius + 273.15`

Cada función debe retornar el resultado **redondeado a 2 decimales** (usen `Math.round(resultado * 100) / 100` o `resultado.toFixed(2)`).

Prueben cada función con al menos 3 valores distintos e impriman los resultados en consola con un mensaje claro.

---

### Ejercicio 12 — Validador de contraseña

**Dificultad:** Media

**Enunciado:** Creen una función `validarPassword(password)` que reciba un string y retorne un mensaje indicando si la contraseña es válida o no, según estas reglas:

1. Debe tener al menos **8 caracteres**.
2. No puede ser solo números (tiene que tener al menos una letra).

Para verificar si contiene letras, pueden comparar la longitud del string original con la longitud al eliminar los dígitos. No es necesario usar expresiones regulares.

**Ejemplos esperados:**
```
validarPassword("abc")         → "Inválida: muy corta (mínimo 8 caracteres)"
validarPassword("12345678")    → "Inválida: debe contener al menos una letra"
validarPassword("pass1234")    → "Válida"
validarPassword("MiClave99")   → "Válida"
```

**Pistas:**
- La longitud se obtiene con `.length`.
- Para verificar si tiene solo números: `Number(password)` retorna `NaN` si tiene letras. Pueden usar `isNaN(Number(password))`.

---

### Ejercicio 13 — Calculadora de propinas

**Dificultad:** Media

**Enunciado:** Creen una función `calcularCuenta(valorTotal, numeroDePersonas, porcentajePropina)` que reciba:
- El valor total de la cuenta de un restaurante.
- El número de personas que van a dividir la cuenta.
- El porcentaje de propina (como número, por ejemplo `10` para el 10%).

La función debe retornar un **objeto** con:
- `subtotal`: El valor original.
- `propina`: El valor de la propina.
- `total`: El subtotal más la propina.
- `porPersona`: El total dividido entre las personas.

Impriman el resultado completo. Por ejemplo, para una cuenta de $80.000 entre 4 personas con 10% de propina:

```
Subtotal:   $80.000
Propina:    $8.000
Total:      $88.000
Por persona: $22.000
```

**Pistas:**
- La propina se calcula así: `valorTotal * (porcentajePropina / 100)`.
- Pueden usar `Math.round()` para evitar decimales extraños.

---

### Ejercicio 14 — FizzBuzz con función

**Dificultad:** Media

**Enunciado:** Creen una función `fizzBuzz(n)` que reciba un número `n` y retorne:
- `"Fizz"` si el número es múltiplo de 3.
- `"Buzz"` si es múltiplo de 5.
- `"FizzBuzz"` si es múltiplo de 3 **y** de 5 al mismo tiempo.
- El número mismo (como string) si no cumple ninguna condición.

Luego, usando un ciclo `for` del 1 al 30, llamen a la función con cada número e impriman el resultado.

El comienzo del resultado esperado:
```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
...
```

---

## Bloque 5: Arreglos (básico)

---

### Ejercicio 15 — Mi lista de reproducción

**Dificultad:** Baja

**Enunciado:** Creen un arreglo llamado `playlist` con 5 canciones de su gusto (solo el nombre como string). Luego:

1. Impriman toda la lista usando un ciclo `for`.
2. Impriman cuántas canciones tiene la lista.
3. Agreguen una nueva canción **al final** con `push`.
4. Agreguen una canción **al inicio** con `unshift`.
5. Eliminen la **última** canción con `pop`.
6. Impriman la lista actualizada.

Para cada paso impriman un título descriptivo en consola. Por ejemplo:
```
--- Lista original ---
1. Canción 1
2. Canción 2
...
```

---

### Ejercicio 16 — Buscador en la lista

**Dificultad:** Baja

**Enunciado:** Dado el siguiente arreglo de países:

```javascript
const paises = ["Colombia", "México", "Argentina", "Chile", "Perú", "Brasil", "Ecuador", "Venezuela"];
```

Sin usar métodos como `includes()` ni `indexOf()`, creen una función `buscarPais(lista, pais)` que recorra el arreglo **manualmente** con un ciclo `for` y:
- Retorne `true` y la posición si el país existe.
- Retorne `false` si no existe.

Prueben la función con al menos 3 búsquedas (una que exista, otra que no, y una con mayúsculas/minúsculas incorrectas).

**Reto extra:** Modifiquen la función para que la búsqueda no sea sensible a mayúsculas. (Pista: `"Colombia".toLowerCase() === "colombia"`)

---

### Ejercicio 17 — Análisis de notas

**Dificultad:** Media

**Enunciado:** Dado un arreglo de notas:

```javascript
const notas = [3.5, 4.2, 2.8, 4.9, 3.1, 4.5, 2.5, 3.8, 4.1, 3.3];
```

Sin usar métodos avanzados (`map`, `filter`, `reduce`), recorran el arreglo con un ciclo `for` y calculen:

1. **El promedio** del grupo.
2. **La nota más alta**.
3. **La nota más baja**.
4. **Cuántos estudiantes aprobaron** (nota >= 3.0).
5. **Cuántos reprobaron**.

Impriman los resultados de forma clara.

**Pistas:**
- Para el promedio: sumen todos los valores y dividan entre `notas.length`.
- Para la más alta/baja: empiecen asumiendo que la primera nota es la más alta/baja, y vayan comparando.

---

### Ejercicio 18 — Inventario de la tienda

**Dificultad:** Media

**Enunciado:** Creen un arreglo de objetos llamado `inventario`, donde cada objeto tenga:
- `producto`: nombre del producto (string)
- `precio`: precio unitario (number)
- `cantidad`: unidades disponibles (number)

Agréguenle al menos 5 productos de su elección. Luego, usando ciclos `for` (sin métodos avanzados), calculen e impriman:

1. El **valor total del inventario** (suma de `precio * cantidad` de cada producto).
2. El **producto más caro**.
3. El **producto con más unidades**.
4. Una lista de todos los productos que tengan menos de **3 unidades** disponibles (stock bajo).

---

### Ejercicio 19 — Ordenamiento de burbuja

**Dificultad:** Alta

**Enunciado:** Implementen el **algoritmo de burbuja** para ordenar un arreglo de números de menor a mayor, **sin usar** el método `.sort()`.

El algoritmo de burbuja funciona así:
1. Recorren el arreglo comparando cada elemento con el siguiente.
2. Si el elemento actual es mayor que el siguiente, los intercambian.
3. Repiten el proceso hasta que el arreglo esté ordenado.

```javascript
const numeros = [64, 34, 25, 12, 22, 11, 90];
// Resultado esperado: [11, 12, 22, 25, 34, 64, 90]
```

**Pistas:**
- Necesitarán dos ciclos `for` anidados.
- Para intercambiar dos valores usen una variable temporal:
  ```javascript
  let temp = arreglo[i];
  arreglo[i] = arreglo[j];
  arreglo[j] = temp;
  ```

---

### Ejercicio 20 — Reto final: Gestión de lista de tareas

**Dificultad:** Alta

**Enunciado:** Construyan un sistema básico de gestión de tareas usando **solo arreglos y funciones** (sin HTML, todo en consola). El sistema debe tener las siguientes funciones:

```javascript
agregarTarea(lista, descripcion)    // Agrega una tarea nueva (pendiente)
completarTarea(lista, indice)       // Marca una tarea como completada
eliminarTarea(lista, indice)        // Elimina una tarea por su posición
mostrarTareas(lista)                // Imprime todas las tareas con su estado
contarPendientes(lista)             // Retorna cuántas tareas están pendientes
```

Cada tarea debe ser un objeto con:
- `descripcion`: texto de la tarea.
- `completada`: `false` por defecto, `true` cuando se completa.

Al final, demuestren el sistema ejecutando una secuencia de operaciones: agregar 4 tareas, completar 2, eliminar 1 y mostrar el estado final.

**Ejemplo de salida esperada:**
```
--- Lista de tareas ---
[1] ✅ Estudiar HTML
[2] ✅ Practicar JavaScript
[3] ⏳ Hacer el ejercicio 18
Pendientes: 1
```

---

## Resumen de conceptos por ejercicio

| Ejercicio | Concepto principal |
|---|---|
| 1 | Variables, template literals |
| 2 | Operadores aritméticos, variables |
| 3 | Tipos de datos, `typeof`, `==` vs `===` |
| 4 | `if / else if / else`, rangos numéricos |
| 5 | `switch`, `case`, `break` |
| 6 | Condicionales + validación lógica |
| 7 | Ciclo `for`, operaciones dentro del ciclo |
| 8 | `for`, operador módulo `%`, `&&` |
| 9 | Ciclo `while`, `break` |
| 10 | `for`, `break`, condicionales combinadas |
| 11 | Funciones con retorno, `Math.round()` |
| 12 | Funciones con validación, `.length` |
| 13 | Funciones que retornan objetos |
| 14 | Funciones + ciclos combinados |
| 15 | Arreglos: `push`, `pop`, `unshift`, `length` |
| 16 | Arreglos + ciclos + búsqueda manual |
| 17 | Arreglos + ciclos + acumuladores |
| 18 | Arreglos de objetos + análisis con ciclos |
| 19 | Ciclos anidados, algoritmo de ordenamiento |
| 20 | Integración: funciones + arreglos de objetos |
