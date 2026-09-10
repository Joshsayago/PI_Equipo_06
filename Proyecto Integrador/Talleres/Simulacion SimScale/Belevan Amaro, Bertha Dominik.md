---

<div align="center">

## ⚙️ Simulación estructural de la carcasa

**Evaluación de esfuerzos en los puntos de fijación mediante SimScale**

</div>

### 📌 Justificación de la simulación

Se realizó una simulación estructural estática en **SimScale** para evaluar el comportamiento de la carcasa fabricada en **PLA**. El análisis se concentró en los cuatro puntos de fijación destinados a los tornillos, debido a que estas zonas mantienen unidas las partes del dispositivo y pueden presentar concentración de esfuerzos.

### 📊 Parámetros empleados

| Parámetro | Valor |
|:---|:---:|
| **Tipo de análisis** | Estático estructural |
| **Material de la carcasa** | PLA |
| **Carga total estimada** | 5 N |
| **Número de puntos de fijación** | 4 |
| **Fuerza aplicada por punto** | 1.25 N |
| **Dirección de la fuerza** | Eje Z negativo |
| **Aceleración de la gravedad** | 9.81 m/s² |
| **Nivel de finura de la malla** | 4 |
| **Resultado evaluado** | Esfuerzo de Von Mises |
| **Esfuerzo máximo obtenido** | 17.28 kPa |

### 🧮 Distribución de la fuerza

Se consideró una carga total de **5 N**, correspondiente al peso estimado de los componentes del dispositivo. Para simplificar el análisis, se asumió que esta carga se distribuye uniformemente entre los cuatro puntos de fijación:

$$
F_{\mathrm{tornillo}}
=
\frac{F_{\mathrm{total}}}{n}
=
\frac{5\,\mathrm{N}}{4}
=
\boxed{1.25\,\mathrm{N}}
$$

Por ello, se aplicó una fuerza de **1.25 N en dirección Z negativa** sobre cada uno de los cuatro puntos de fijación.

> **Nota:** La distribución uniforme representa una condición simplificada en la que los cuatro tornillos soportan la carga del dispositivo de manera equivalente.

### 🕸️ Configuración del mallado

Para el análisis se utilizó una **malla estándar con nivel de finura 4**, con el propósito de obtener una distribución adecuada de los esfuerzos sin incrementar excesivamente el costo computacional.

### 🖥️ Resultado de la simulación

<div align="center">

<img width="900" alt="Distribución del esfuerzo de Von Mises en la carcasa de PLA" src="https://github.com/user-attachments/assets/ad2d2dd1-c7f3-4213-a9d4-4e2ad5225659" />

*Figura 1. Distribución del esfuerzo de Von Mises en la carcasa de PLA.*

</div>

### 🔍 Interpretación de los resultados

La simulación mostró un esfuerzo máximo de Von Mises de aproximadamente:

$$
\sigma_{\mathrm{máx}}
=
17.28\,\mathrm{kPa}
=
0.01728\,\mathrm{MPa}
$$

La mayor parte de la carcasa presenta tonalidades azules, asociadas con niveles bajos de esfuerzo. Los incrementos se concentran principalmente alrededor de los puntos de fijación y sus zonas cercanas, debido a que allí se aplicaron las cargas y restricciones.

Bajo las condiciones simuladas, no se observa una zona crítica evidente frente a la carga total de **5 N**. Sin embargo, los resultados corresponden únicamente al material, la dirección de las cargas, las condiciones de fijación y el mallado establecidos en el modelo.

> ⚠️ **Alcance:** Esta simulación constituye una evaluación preliminar del diseño y no reemplaza las pruebas mecánicas realizadas sobre el prototipo físico.

---
