App Inventor (Condicionales simples)

## Objetivo
Practicar **condicionales simples** usando `if / else` (y un ejercicio con `else if`) para tomar decisiones en una app.

## Reglas
- Usar App Inventor con bloques.
- En los ejercicios 1 y 2: solo `if / else`.
- En el ejercicio 3: se permite `else if`.
- Mantener nombres claros:
  - TextBox: `txt...`
  - Button: `btn...`
  - Label: `lbl...`

## Entregables
- Archivo(s) `.aia` (puede ser 1 proyecto con 3 pantallas o 3 proyectos).
- 1 captura por ejercicio con entradas y resultado visible.

Estructura sugerida:
- `/aia/`
- `/screenshots/`

---

## Ejercicio 1 — Acceso permitido / denegado (Edad mínima)

### Enunciado
Crea una app que reciba la **edad** de una persona y determine si puede acceder.

### Entrada
- Edad (número entero)

### Salida
- Un mensaje en pantalla indicando:
  - **"Acceso permitido"** si la edad es **mayor o igual a 18**
  - **"Acceso denegado"** si la edad es **menor a 18**

### UI mínima (Designer)
- `txtEdad` (Hint: "Edad")
- `btnVerificar` (Text: "Verificar")
- `lblResultado`

### Criterios de aceptación
- Al presionar **Verificar**, se muestra el mensaje correcto según la edad.
- El mensaje debe ser claro y visible (Label).

### Extra (opcional)
Cambiar el fondo de la pantalla:
- Permitido → color “positivo”
- Denegado → color “de alerta”

---

## Ejercicio 2 — Par o impar

### Enunciado
Crea una app que reciba un **número entero** y muestre si es **PAR** o **IMPAR**.

### Entrada
- Número entero

### Salida
- **"Es PAR"** si el número tiene residuo 0 al dividirse por 2
- **"Es IMPAR"** en caso contrario

### Pista (bloques)
- Usa el bloque matemático **`mod`** (residuo).
- Si `n mod 2 = 0`, entonces es par.

### UI mínima (Designer)
- `txtNumero` (Hint: "Número entero")
- `btnEvaluar` (Text: "Evaluar")
- `lblResultado`

### Criterios de aceptación
- Al presionar **Evaluar**, se muestra PAR o IMPAR correctamente.

### Extra (opcional)
Mostrar también el residuo, por ejemplo:
- "Residuo: 1"

---

## Ejercicio 3 — Tarifa de envío por peso (con else-if)

### Enunciado
Crea una app que calcule la **tarifa de envío** según el **peso del paquete (kg)**.

### Entrada
- Peso en kg (número)

### Salida
Mostrar la tarifa correspondiente:
- Si el peso es **menor o igual a 1 kg** → Tarifa: **8000**
- Si el peso es **menor o igual a 5 kg** → Tarifa: **12000**
- Si el peso es **mayor a 5 kg** → Tarifa: **20000**

### UI mínima (Designer)
- `txtPeso` (Hint: "Peso en kg")
- `btnCalcular` (Text: "Calcular")
- `lblTarifa`

### Criterios de aceptación
- Al presionar **Calcular**, se muestra la tarifa correcta.
- La tarifa debe mostrarse con texto descriptivo, por ejemplo: "Tarifa: 12000".

### Extra (opcional)
Agregar una validación simple:
- Si `peso <= 0` mostrar: **"Peso inválido"**
