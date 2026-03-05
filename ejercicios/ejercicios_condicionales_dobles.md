# Condicionales dobles (condiciones compuestas con AND / OR)

## Objetivo
Practicar **condicionales dobles** usando condiciones compuestas:
- `AND` (se deben cumplir **dos** cosas)
- `OR` (se debe cumplir **al menos una**)

## Reglas
- Se permite `if / else` y usar `and / or` (bloques de **Logic**).
- NO usar ciclos ni temporizadores.
- Mantener nombres claros (`txt...`, `btn...`, `lbl...`).

## Entregables
- `.aia` (1 proyecto con 4 pantallas o 4 proyectos).
- 1 captura por ejercicio con entradas diligenciadas y resultado visible.

---

## Ejercicio 1 — Aprobación con nota Y asistencia (AND)

### Enunciado
Crea una app que determine si un estudiante **aprueba** una materia usando **dos condiciones**:
- Nota final (0 a 5)
- Asistencia (0 a 100)

### Reglas
- Aprueba si: `nota >= 3` **Y** `asistencia >= 80`
- Si no cumple ambas, reprueba.

### UI mínima (Designer)
- `txtNota` (Hint: "Nota (0 a 5)")
- `txtAsistencia` (Hint: "Asistencia (0 a 100)")
- `btnEvaluar`
- `lblResultado`

### Criterios de aceptación
- Al presionar **Evaluar**, muestra:
  - "APRUEBA" si cumple las dos condiciones
  - "REPRUEBA" si no
- El resultado debe verse claramente en pantalla.

### Extra (opcional)
Mostrar también un resumen: `"Nota: X | Asistencia: Y"`

---

## Ejercicio 2 — Descuento por compra O cliente VIP (OR)

### Enunciado
Crea una app que calcule el total a pagar aplicando descuento si se cumple **una** de estas condiciones:
- Subtotal mayor o igual a 100000
- El cliente es VIP

### Entradas
- Subtotal (número)
- VIP (Switch o CheckBox)

### Reglas
- Si `subtotal >= 100000` **O** `VIP = true` → descuento del **10%**
- Si no → descuento del **0%**
- Total = subtotal - descuento

### UI mínima
- `txtSubtotal` (Hint: "Subtotal")
- `swVip` o `chkVip` (Text: "Cliente VIP")
- `btnCalcular`
- `lblTotal`
- `lblDescuento` (opcional pero recomendado)

### Criterios de aceptación
- Muestra el descuento aplicado y el total final.
- La condición debe usar `OR`.

### Extra (opcional)
Mostrar un mensaje:
- "Descuento aplicado" / "Sin descuento"

---

## Ejercicio 3 — PIN válido Y confirmado (AND)

### Enunciado
Crea una app de “confirmación de PIN” que valide **dos cosas al mismo tiempo**:
1) El PIN debe tener exactamente **4 dígitos** (longitud = 4)  
2) El PIN y la confirmación deben ser **iguales**

### Entradas
- PIN
- Confirmar PIN

### Reglas
- Si `(length(PIN) = 4) AND (PIN = ConfirmarPIN)` → "PIN válido "
- Si no → "PIN inválido "

### UI mínima
- `txtPin` (Hint: "PIN (4 dígitos)")
- `txtPin2` (Hint: "Confirmar PIN")
- `btnValidar`
- `lblResultado`

### Criterios de aceptación
- Si cumple ambas condiciones, muestra “PIN válido”.
- Si falla cualquiera, muestra “PIN inválido”.
- Debe usar `AND`.

### Pista (bloques)
- Usa `length of text` para validar longitud.
- Usa comparación de texto `=` para validar igualdad.

---

## Ejercicio 4 — Acceso a evento: edad Y boleta (AND) con validación simple

### Enunciado
Crea una app que permita el acceso a un evento solo si se cumplen **dos condiciones**:
- Edad mínima: 18
- Tiene boleta: Sí/No (Switch o CheckBox)

### Entradas
- Edad (número)
- Tiene boleta (boolean)

### Reglas
- Si `edad >= 18` **Y** `tieneBoleta = true` → "Acceso permitido "
- Si no → "Acceso denegado"

### UI mínima
- `txtEdad` (Hint: "Edad")
- `swBoleta` o `chkBoleta` (Text: "Tengo boleta")
- `btnVerificar`
- `lblResultado`

### Criterios de aceptación
- El acceso solo se permite si ambas condiciones se cumplen.
- Debe usar `AND`.

### Extra (opcional)
Cambiar el fondo:
- Permitido → color “positivo”
- Denegado → color “alerta”
