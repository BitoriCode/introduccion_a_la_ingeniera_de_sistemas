# Clase 3 — App Inventor (Programación secuencial)

## Reglas de la clase
- NO usar condicionales (`if`) en estos ejercicios.
- Mantener nombres claros:
  - TextBox: `txt...`
  - Button: `btn...`
  - Label: `lbl...`
- Estructura recomendada en bloques:
  1) Leer entradas (TextBox.Text)
  2) Calcular resultados (operaciones)
  3) Mostrar resultados (Label.Text)
  4)  resultado visible

---

## Ejercicio 1 — Calculadora de viaje (tiempo y costo)

### Objetivo
Calcular **tiempo estimado** y **costo de gasolina** de un viaje a partir de datos básicos.

### Entradas (usuario)
- Distancia (km)
- Velocidad promedio (km/h)
- Consumo del carro (km por litro)
- Precio de gasolina por litro

### Salidas (app)
- Tiempo estimado (horas)
- Litros estimados
- Costo del viaje

### Fórmulas
- `tiempo = distancia / velocidad`
- `litros = distancia / consumo`
- `costo = litros * precio_litro`

### UI mínima (Diseñador)
- `txtDistancia`, `txtVelocidad`, `txtConsumo`, `txtPrecioLitro`
- `btnCalcular`
- `lblReporte`

### Criterios de aceptación
- Al presionar **Calcular**, la app muestra un reporte con las 3 salidas.
- El reporte debe incluir texto descriptivo, por ejemplo:
  - `Tiempo (h): ...`
  - `Litros: ...`
  - `Costo: ...`

### Extra (opcional)
Mostrar el reporte en 3 líneas dentro del mismo Label.

---

## Ejercicio 2 — Conversor de temperatura extendido (C → F y K)

### Objetivo
Convertir una temperatura ingresada en **Celsius** a **Fahrenheit** y **Kelvin**.

### Entrada
- Celsius (C)

### Salidas
- Fahrenheit (F)
- Kelvin (K)

### Fórmulas
- `F = (C * 9/5) + 32`
- `K = C + 273.15`

### UI mínima (Diseñador)
- `txtCelsius`
- `btnConvertir`
- `lblFahrenheit`
- `lblKelvin` (o un solo `lblReporte`)

### Criterios de aceptación
- Al presionar **Convertir**, se muestran F y K correctamente.
- La salida debe incluir etiquetas (texto) para que se entienda el valor.

### Extra (opcional)
Mostrar también el valor original (C) en el reporte.

---

## Ejercicio 3 — Nómina simple (salario neto)

### Objetivo
Calcular el salario **bruto**, el **descuento** y el salario **neto**.

### Entradas
- Horas trabajadas
- Valor por hora
- Porcentaje de descuento (ej: 8 para 8%)

### Salidas
- Salario bruto
- Descuento
- Salario neto

### Fórmulas
- `bruto = horas * valor_hora`
- `descuento = bruto * (porcentaje / 100)`
- `neto = bruto - descuento`

### UI mínima (Diseñador)
- `txtHoras`, `txtValorHora`, `txtPorcentaje`
- `btnCalcular`
- `lblResumen`

### Criterios de aceptación
- Al presionar **Calcular**, se muestra un resumen con los 3 valores.
- El porcentaje debe aplicarse como porcentaje real (dividido entre 100).

### Extra (opcional)
Agregar un segundo Label que muestre el cálculo paso a paso (bruto → descuento → neto).

