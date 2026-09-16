<div align="center">

# 📈 Taller de Regresión Lineal

### Análisis y predicción del consumo de energía

**Estudiante:** Bertha Dominik Belevan Amaro  
**Equipo:** Equipo 06  
**Curso:** Proyecto Integrador  

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Machine_Learning-6C63FF?style=for-the-badge)

<br>

<a href="https://colab.research.google.com/drive/1N3gLh6GmySgBYrM4U-EsZVXT7k-K6eYn#scrollTo=dKlxlU3CZszk">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir en Google Colab">
</a>

</div>

---

## 📌 Descripción del trabajo

En este taller se aplicó un modelo de **regresión lineal múltiple** para analizar y predecir el consumo de energía a partir de diferentes variables operativas y ambientales.

El análisis permitió identificar la relación entre las variables, construir un modelo predictivo, comparar los valores reales con los valores estimados y reconocer cuáles características presentan una mayor influencia en los resultados.

---

## 🎯 Objetivo

Construir un modelo de regresión lineal capaz de estimar el **consumo de energía** mediante las siguientes variables:

- Temperatura.
- Horas de operación.
- Carga.
- Humedad.

---

## 📂 Descripción de los datos

El conjunto de datos utilizado contiene **5000 observaciones** y no presenta valores nulos.

| Tipo | Variable | Descripción |
|:---:|:---|:---|
| Entrada | `Temperatura` | Temperatura registrada durante la operación |
| Entrada | `Horas_Operacion` | Cantidad de horas de funcionamiento |
| Entrada | `Carga` | Nivel de carga del sistema |
| Entrada | `Humedad` | Humedad registrada |
| Salida | `Consumo_Energia` | Consumo de energía que se desea predecir |



# 📊 Resultados gráficos

## 1. Consumo de energía real vs. predicción

<div align="center">

<img width="700" alt="Consumo de energía real frente al consumo predicho" src="https://github.com/user-attachments/assets/1928ff3d-8417-41d2-8a76-4240876b6dfc" />

</div>

### 🔎 ¿Qué representa?

La gráfica compara los valores reales del consumo de energía con los valores calculados por el modelo de regresión lineal.

- El eje horizontal muestra el **consumo de energía real**.
- El eje vertical muestra el **consumo de energía predicho**.
- Cada punto corresponde a una observación del conjunto de evaluación.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque permite observar directamente qué tan cercanas son las predicciones del modelo a los valores reales. También representa visualmente el objetivo principal del modelo de regresión lineal.

### ⭐ ¿Por qué es importante?

Es importante porque permite evaluar visualmente la capacidad predictiva del modelo. Los puntos presentan una tendencia diagonal ascendente, lo cual indica una relación positiva entre los valores reales y los predichos.

### 🛠️ ¿Para qué sirve?

Sirve para comprobar si el modelo realiza predicciones razonables. Cuanto más cerca se encuentren los puntos de una línea diagonal imaginaria, mejor será el ajuste del modelo.

> **Interpretación:** la concentración de los puntos alrededor de una tendencia diagonal indica que el modelo logra representar adecuadamente el comportamiento general del consumo de energía, aunque existen pequeñas diferencias entre algunos valores reales y predichos.

---

## 2. Importancia relativa de las características

<div align="center">

<img width="700" alt="Importancia relativa de las características" src="https://github.com/user-attachments/assets/a05efb73-bfc8-42a1-9f02-209660379440" />

</div>

### 🔎 ¿Qué representa?

La gráfica muestra la importancia relativa de las características `X1`, `X2`, `X3`, `X4`, `X5` y `X6` en el modelo predictivo complementario de árbol de decisión.

Las barras de mayor longitud corresponden a las variables que aportan más información al modelo.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque presenta de manera clara, visual y ordenada cuánto aporta cada característica al resultado de la predicción.

### ⭐ ¿Por qué es importante?

Es importante porque demuestra que no todas las variables tienen la misma influencia.

| Característica | Importancia aproximada | Nivel de influencia |
|:---:|:---:|:---|
| X2 | **53.7 %** | Muy alta |
| X1 | **26.9 %** | Alta |
| X3 | **11.1 %** | Moderada |
| X4 | **3.8 %** | Baja |
| X6 | **3.3 %** | Baja |
| X5 | **1.2 %** | Muy baja |

### 🛠️ ¿Para qué sirve?

Sirve para identificar las variables más relevantes, reducir información innecesaria y comprender en cuáles características se apoya principalmente el modelo para realizar predicciones.

> **Nota metodológica:** esta gráfica corresponde a un modelo complementario de **árbol de decisión** aplicado a datos generados durante el taller. No representa directamente los coeficientes de la regresión lineal del consumo de energía.

---

## 3. Matriz de correlación

<div align="center">

<img width="700" alt="Matriz de correlación de las variables" src="https://github.com/user-attachments/assets/f2756db4-a269-4478-90f5-8517e1e46b9a" />

</div>

### 🔎 ¿Qué representa?

La matriz muestra la relación existente entre la temperatura, las horas de operación, la carga, la humedad y el consumo de energía.

Los valores cercanos a `1` indican una relación positiva fuerte, mientras que los valores cercanos a `0` indican una relación débil.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque reúne todas las relaciones entre las variables en una sola representación. Además, la escala de colores facilita la comparación e identificación de las relaciones más importantes.

### ⭐ ¿Por qué es importante?

Es importante porque permite reconocer cuáles variables están más asociadas con el consumo energético.

| Variable | Correlación con el consumo | Interpretación |
|:---|:---:|:---|
| Horas de operación | **0.8434** | Relación positiva fuerte |
| Carga | **0.3366** | Relación positiva moderada |
| Temperatura | **0.0978** | Relación positiva débil |
| Humedad | **0.0627** | Relación positiva débil |

### 🛠️ ¿Para qué sirve?

Sirve para seleccionar las variables que pueden aportar más información al modelo y comprender mejor el comportamiento del conjunto de datos.

> **Interpretación:** las horas de operación constituyen la variable más relacionada con el consumo de energía. Esto indica que, generalmente, cuando aumentan las horas de funcionamiento, también aumenta el consumo energético.

> **Importante:** una correlación elevada indica asociación entre variables, pero no demuestra por sí sola una relación de causa y efecto.

---

## 🧠 Comparación de los resultados

| Gráfica | Información principal | Utilidad |
|:---|:---|:---|
| Real vs. predicho | Compara las predicciones con los datos reales | Evaluar visualmente el ajuste |
| Importancia de características | Muestra cuánto aporta cada característica | Identificar las variables relevantes |
| Matriz de correlación | Presenta la relación entre las variables | Reconocer asociaciones con el consumo |

---

## 🔍 Principales hallazgos

- Las **horas de operación** presentan la correlación más alta con el consumo de energía: **0.8434**.
- El coeficiente de las horas de operación también es el mayor del modelo: **1.6688**.
- La **carga** presenta una relación positiva moderada con el consumo.
- La temperatura y la humedad tienen una relación positiva, pero considerablemente menor.
- La gráfica de valores reales y predichos presenta una tendencia diagonal definida.
- No todas las variables aportan la misma cantidad de información a un modelo predictivo.

---

## ⚠️ Limitaciones

Aunque el modelo presenta una tendencia adecuada, las predicciones no son completamente exactas. El consumo de energía puede depender de otras variables que no fueron incluidas en el conjunto de datos.

Además, la correlación entre dos variables no significa necesariamente que una sea la causa directa de la otra.

Como mejoras futuras se podría:

- Incorporar nuevas variables relacionadas con el consumo.
- Comparar los resultados con otros modelos predictivos.
- Analizar con mayor detalle los errores o residuos.
- Aplicar validación cruzada.
- Evaluar el modelo con métricas como MAE, RMSE y R².

---

## ✅ Conclusión

El análisis permitió construir un modelo de regresión lineal múltiple para estimar el consumo de energía a partir de la temperatura, las horas de operación, la carga y la humedad.

La matriz de correlación y los coeficientes del modelo indican que las **horas de operación** son la variable con mayor relación e influencia estimada sobre el consumo energético. La comparación entre los valores reales y predichos presenta una tendencia diagonal, lo que demuestra que el modelo logra representar el comportamiento general de los datos.

El análisis complementario de importancia de características también permitió comprobar que las variables no aportan información en la misma proporción. En conjunto, las herramientas aplicadas facilitaron la interpretación de los datos y la comprensión del funcionamiento de los modelos predictivos.

---

## 🔗 Acceso al trabajo completo

El procedimiento, el código y los resultados pueden revisarse en el siguiente cuaderno:

<div align="center">

### 📓 [Abrir el proyecto en Google Colab](https://colab.research.google.com/drive/1N3gLh6GmySgBYrM4U-EsZVXT7k-K6eYn#scrollTo=dKlxlU3CZszk)

</div>

---

<div align="center">

## 🛠️ Herramientas utilizadas

`Python` • `Google Colab` • `Pandas` • `NumPy`  
`Matplotlib` • `Seaborn` • `Scikit-learn` • `Statsmodels`

<br>

### Proyecto Integrador — Equipo 06

**Bertha Dominik Belevan Amaro**

</div>
