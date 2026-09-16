<div align="center">

# 📈 Taller de Regresión Lineal

### Análisis y predicción del consumo de energía

**Estudiante:** Bertha Dominik Belevan Amaro  
**Equipo:** Equipo 06  
**Curso:** Proyecto Integrador

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Machine-Learning-6C63FF?style=for-the-badge)

</div>

---

## 📌 Descripción del trabajo

En este taller se aplicaron herramientas de **regresión lineal y análisis predictivo** para estudiar el consumo de energía a partir de diferentes variables.

El análisis permitió identificar la relación existente entre los datos, comparar los valores reales con los valores predichos y determinar cuáles características tienen mayor influencia en los resultados del modelo.

---

## 📊 Trabajo realizado

Durante el desarrollo del taller se trabajaron los siguientes puntos:

- **Análisis de correlación:** permitió identificar la relación entre las variables y determinar cuáles están más asociadas con el consumo de energía.
- **Valores reales vs. predichos:** permitió comparar las predicciones generadas por el modelo con los datos reales.
- **Importancia de las características:** permitió reconocer las variables que aportan mayor información al modelo predictivo.
- **Interpretación de resultados:** permitió evaluar visualmente el comportamiento y la utilidad de los modelos desarrollados.

---

# 📉 Resultados gráficos

## 1. Consumo de energía real vs. predicción

<div align="center">

<img width="700" alt="Consumo de energía real frente al consumo predicho" src="https://github.com/user-attachments/assets/1928ff3d-8417-41d2-8a76-4240876b6dfc" />

</div>

### 🔎 ¿Qué representa?

La gráfica compara los valores reales del consumo de energía con los valores calculados por el modelo de regresión lineal.

Cada punto representa una observación:

- El eje horizontal muestra el **consumo de energía real**.
- El eje vertical muestra el **consumo de energía predicho**.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque permite observar directamente qué tan cercanas son las predicciones del modelo a los valores reales. Además, muestra de forma clara el funcionamiento principal de la regresión lineal.

### ⭐ ¿Por qué es importante?

Es importante porque permite evaluar visualmente la capacidad predictiva del modelo. Los puntos presentan una tendencia diagonal ascendente, lo cual indica que existe una buena relación entre los valores reales y los valores predichos.

### 🛠️ ¿Para qué sirve?

Sirve para comprobar si el modelo realiza predicciones adecuadas. Cuanto más cerca se encuentren los puntos de una línea diagonal imaginaria, mayor será la precisión del modelo.

> **Interpretación:** la concentración de los puntos alrededor de una tendencia diagonal indica que el modelo logra representar de manera adecuada el comportamiento general del consumo de energía.

---

## 2. Importancia relativa de las características

<div align="center">

<img width="700" alt="Importancia relativa de las características" src="https://github.com/user-attachments/assets/a05efb73-bfc8-42a1-9f02-209660379440" />

</div>

### 🔎 ¿Qué representa?

La gráfica muestra la importancia relativa de las características `X1`, `X2`, `X3`, `X4`, `X5` y `X6` dentro del modelo predictivo complementario.

Las barras más largas representan las variables con mayor influencia en las predicciones.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque permite comparar de forma rápida, visual y ordenada cuánto aporta cada característica al modelo.

### ⭐ ¿Por qué es importante?

Es importante porque demuestra que no todas las variables influyen de la misma manera. En este caso:

- `X2` es la característica con mayor importancia.
- `X1` ocupa el segundo lugar.
- `X3` presenta una influencia menor, pero todavía relevante.
- `X4`, `X5` y `X6` tienen una participación reducida.

### 🛠️ ¿Para qué sirve?

Sirve para seleccionar las variables más relevantes, reducir información innecesaria y comprender en qué características se apoya principalmente el modelo para realizar sus predicciones.

> **Nota:** esta gráfica corresponde al modelo complementario de **árbol de decisión** desarrollado durante el taller. No representa directamente los coeficientes de la regresión lineal.

---

## 3. Matriz de correlación

<div align="center">

<img width="700" alt="Matriz de correlación de las variables" src="https://github.com/user-attachments/assets/f2756db4-a269-4478-90f5-8517e1e46b9a" />

</div>

### 🔎 ¿Qué representa?

La matriz muestra la relación existente entre las siguientes variables:

- Temperatura.
- Horas de operación.
- Carga.
- Humedad.
- Consumo de energía.

Los valores cercanos a `1` indican una relación positiva fuerte, mientras que los valores cercanos a `0` representan una relación débil.

### 💡 ¿Por qué elegí esta imagen?

Elegí esta imagen porque reúne todas las relaciones entre las variables en una sola representación y utiliza colores para facilitar su interpretación.

### ⭐ ¿Por qué es importante?

Es importante porque permite identificar cuáles variables están más asociadas con el consumo energético.

| Variable | Correlación con el consumo | Interpretación |
|:---|:---:|:---|
| Horas de operación | **0.84** | Relación positiva fuerte |
| Carga | **0.34** | Relación positiva moderada |
| Temperatura | **0.098** | Relación positiva débil |
| Humedad | **0.063** | Relación positiva débil |

### 🛠️ ¿Para qué sirve?

Sirve para seleccionar las variables que pueden aportar más información al modelo de regresión lineal y para comprender mejor el comportamiento de los datos.

> **Interpretación:** las horas de operación son la variable más relacionada con el consumo de energía. Esto indica que, generalmente, cuando aumentan las horas de funcionamiento, también aumenta el consumo energético.

---

## 🧠 Comparación de las gráficas

| Gráfica | Información principal | Utilidad |
|:---|:---|:---|
| Real vs. predicho | Compara las predicciones con los datos reales | Evaluar el ajuste del modelo |
| Importancia de características | Muestra cuánto influye cada variable | Seleccionar las variables más relevantes |
| Matriz de correlación | Presenta la relación entre las variables | Identificar asociaciones con el consumo |

---

## ✅ Conclusión

Las tres gráficas seleccionadas permiten analizar el problema desde diferentes perspectivas.

La comparación entre los valores reales y predichos muestra que el modelo logra representar adecuadamente la tendencia del consumo de energía. El análisis de importancia permite reconocer las características que más aportan a un modelo predictivo complementario. Finalmente, la matriz de correlación demuestra que las **horas de operación**, con un valor de **0.84**, son la variable con mayor relación con el consumo energético.

En conjunto, estos resultados permiten comprender el comportamiento de los datos, evaluar el modelo y reconocer las variables más relevantes para realizar predicciones.

---

<div align="center">

### 🛠️ Herramientas utilizadas

`Python` • `Google Colab` • `Pandas` • `NumPy` • `Matplotlib` • `Seaborn` • `Scikit-learn`

<br>

**Proyecto Integrador — Equipo 06**

</div>
