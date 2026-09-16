<div align="center">

# Taller de Regresión Lineal y Modelos Predictivos

### Análisis y predicción del consumo de energía

**Estudiante:** Mónica Huamán Bernal
**Equipo:** Equipo 06
**Curso:** Proyecto Integrador

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?style=for-the-badge\&logo=googlecolab\&logoColor=white)
 
</div>

---

## 1. Descripción

En este taller se desarrolló un análisis de datos orientado a comprender el comportamiento del **consumo de energía** y explorar herramientas de modelamiento predictivo.

El trabajo comprende un análisis exploratorio mediante estadística descriptiva, visualizaciones y análisis de correlaciones. Posteriormente, se implementó un modelo de **Regresión Lineal** para realizar predicciones y analizar sus errores.

Como ejercicio complementario, se trabajó con un conjunto de datos sintético para implementar un **Árbol de Decisión**, evaluando su desempeño mediante el Error Cuadrático Medio (MSE) y analizando la importancia de las variables utilizadas por el modelo.
---

## 2. Herramientas y librerías

El desarrollo se realizó en **Google Colab** utilizando Python.

| Herramienta / librería | Uso                                  |
| :--------------------- | :----------------------------------- |
| `NumPy`                | Operaciones numéricas                |
| `Pandas`               | Manipulación y análisis de datos     |
| `Matplotlib`           | Visualización de datos               |
| `Seaborn`              | Visualización estadística            |
| `Scikit-learn`         | Construcción y evaluación de modelos |
| `Statsmodels`          | Análisis estadístico                 |

**Principales funciones y modelos utilizados:**

`LinearRegression` · `train_test_split` · `DecisionTreeRegressor` · `make_regression` · `mean_squared_error` · `OLS`

---

# 3. Exploración de los datos

Como primera etapa se realizó una exploración del conjunto de datos mediante:

* Visualización de las primeras observaciones.
* Información general de las variables.
* Estadística descriptiva.
* Análisis gráfico de las relaciones entre variables.
* Matriz de correlación.

Este proceso permitió obtener una primera aproximación al comportamiento de los datos antes de construir los modelos predictivos.

---

## 3.1 Distribución del consumo de energía

Se analizó la distribución de la variable `Consumo_Energia` mediante un histograma acompañado de una estimación de densidad.

<div align="center">

<img width="695" height="351" alt="image" src="https://github.com/user-attachments/assets/0be905b1-cb68-4e22-89a1-c7b7100e40ab" />
<img width="576" height="413" alt="image" src="https://github.com/user-attachments/assets/0369e533-0642-4e5e-ac41-75e43df9b2f0" />



</div>

**Interpretación**

El gráfico permite observar la distribución de los valores de consumo de energía y reconocer la concentración general de los datos.

*Este análisis exploratorio permite conocer el comportamiento de la variable antes de aplicar los modelos predictivos.*

---

# 4. Modelo de Regresión Lineal

Se implementó un modelo de **Regresión Lineal** mediante `LinearRegression`.

El conjunto de datos fue dividido en:

| Conjunto      | Proporción |
| :------------ | :--------: |
| Entrenamiento |  **70 %**  |
| Prueba        |  **30 %**  |

La división se realizó utilizando `train_test_split` con `random_state=123`, con el objetivo de mantener la reproducibilidad del experimento.

Las variables independientes fueron utilizadas como entrada y `Consumo_Energia` como variable objetivo. De esta manera, el modelo busca establecer una relación matemática entre las variables de entrada y el consumo de energía para generar predicciones.

---

# 5. Análisis de los residuos

Los residuos representan la diferencia entre los valores reales y los valores predichos por el modelo:

```text
eᵢ = yᵢ − ŷᵢ
```

donde:

* `yᵢ` representa el valor real.
* `ŷᵢ` representa el valor predicho.
* `eᵢ` representa el residuo.

Para analizar estos errores se utilizó un gráfico de residuos frente a los valores predichos.

<div align="center">

<img width="854" height="687" alt="image" src="https://github.com/user-attachments/assets/8dc5aa35-f5a5-42f3-91d0-8b4def57f4a6" />

</div>

**Interpretación**

El gráfico permite observar la distribución de los errores del modelo respecto a los valores predichos.

La ausencia de patrones evidentes en los residuos puede indicar que el modelo no deja una estructura clara sin explicar. Sin embargo, esta evaluación debe complementarse con otras métricas y análisis estadísticos.

---

# 6. Árbol de Decisión

Como ejercicio complementario se generó un conjunto de datos sintético mediante `make_regression`.

Se utilizaron:

* **100 observaciones**
* **6 variables predictoras**
* **3 variables informativas**
* **Ruido = 20**
* `random_state = 20`

Las variables predictoras fueron denominadas `X1`, `X2`, `X3`, `X4`, `X5` y `X6`.

Posteriormente se implementó el modelo:

```python
DecisionTreeRegressor(max_depth=5, random_state=10)
```

El modelo permitió realizar predicciones sobre la variable objetivo y evaluar su desempeño mediante el **Error Cuadrático Medio (MSE)**.

---

## 6.1 Importancia de las variables

El Árbol de Decisión permite obtener una medida de la importancia de cada variable mediante:

```python
tree_model.feature_importances_
```

<div align="center">

<img width="907" height="609" alt="image" src="https://github.com/user-attachments/assets/c1fb309e-83ce-47df-922b-9f52d0e4fbc1" />


</div>

**Interpretación**

El gráfico muestra la importancia relativa de las variables `X1` a `X6` dentro del modelo.

Esta información permite identificar cuáles variables presentan una mayor contribución en las decisiones realizadas por el árbol.

> *Nota: este resultado corresponde al conjunto de datos sintético utilizado en el ejercicio complementario y no directamente al conjunto de datos de consumo de energía.*

---

# 7. Comparación de los modelos

| Característica    | Regresión Lineal     | Árbol de Decisión            |
| :---------------- | :------------------- | :--------------------------- |
| Tipo de modelo    | Lineal               | Basado en reglas de decisión |
| Datos utilizados  | Consumo de energía   | Datos sintéticos             |
| Variable objetivo | `Consumo_Energia`    | Variable `y`                 |
| Predicción        | Sí                   | Sí                           |
| Evaluación        | Análisis de residuos | MSE                          |
| Interpretación    | Coeficientes         | Importancia de variables     |
| Librería          | Scikit-learn         | Scikit-learn                 |

La comparación permitió reconocer diferentes estrategias para abordar problemas de predicción y las distintas formas de interpretar los resultados obtenidos.

---

# 9. Análisis estadístico adicional

Finalmente, se utilizó `statsmodels` para ajustar un modelo mediante **OLS (Ordinary Least Squares)**.

El resumen estadístico generado permitió complementar el análisis realizado con `scikit-learn`, proporcionando información adicional sobre el modelo y sus variables.

Este procedimiento permitió relacionar el enfoque de aprendizaje automático con herramientas de estadística inferencial.

---

# 10. Principales aprendizajes

* Importancia del **análisis exploratorio** antes de construir un modelo.
* Uso de gráficos para comprender el comportamiento de los datos.
* Aplicación de la **Regresión Lineal** para realizar predicciones.
* Interpretación de los **residuos** de un modelo.
* Aplicación de **Árboles de Decisión** para problemas de regresión.
* Interpretación de la **importancia de las variables**.
* Evaluación del error mediante el **MSE**.
* Uso complementario de `scikit-learn` y `statsmodels`.

---

# 11. Conclusiones

El desarrollo del taller permitió aplicar un flujo básico de análisis y modelamiento predictivo, comenzando por la exploración de los datos y continuando con la construcción y evaluación de modelos.

La **Regresión Lineal** permitió trabajar directamente con el conjunto de datos relacionado con el consumo de energía, mientras que el **Árbol de Decisión** permitió explorar un enfoque diferente mediante un conjunto de datos sintético.

El análisis de los residuos y de la importancia de las variables permitió complementar las predicciones con información sobre el comportamiento y la interpretación de los modelos.

En conjunto, el taller permitió comprender de manera práctica cómo las herramientas de análisis estadístico y aprendizaje automático pueden utilizarse para estudiar datos y construir modelos predictivos.
# 12. Código

El código completo utilizado para el desarrollo del taller se encuentra disponible en Google Colab.

<div align="center">

[Abrir proyecto en Google Colab][(https://colab.research.google.com/drive/1LAjpfEdVM_ZxRvdusQJ1LAQmscdhbhcp?authuser=1#scrollTo=KNK-rJK2qpEn)](https://colab.research.google.com/drive/11AuGiA9RQU85YKpOPQVKpLI2hEEK1x2M)

</div>

<div align="center">

Proyecto Integrador — Equipo 06

Python · Google Colab · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Statsmodels

</div>

