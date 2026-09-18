# Análisis de la concentración diaria de Ozono — EPA 2022–2023

## 1. Introducción

La calidad del aire puede analizarse mediante diferentes contaminantes atmosféricos. Uno de ellos es el **ozono (O₃)**, cuya concentración puede variar dependiendo de factores temporales, geográficos y de las condiciones presentes en la zona de monitoreo.

En este trabajo se utilizaron datos diarios de calidad del aire obtenidos de la **U.S. Environmental Protection Agency (EPA)** correspondientes al periodo comprendido entre el **1 de enero de 2022 y el 31 de diciembre de 2023**.

El conjunto de datos contiene **10 136 registros y 28 variables**, correspondientes a mediciones realizadas en diferentes estaciones de monitoreo.

El objetivo del trabajo fue aplicar un modelo de **regresión lineal múltiple** para analizar la relación entre diferentes variables disponibles en el conjunto de datos y la **concentración máxima diaria de ozono**.

La variable que se desea predecir es:

* `Daily Max Ozone Concentration`

Las variables utilizadas como predictoras fueron:

* `Daily AQI Value`
* `Site Latitude`
* `Site Longitude`
* `Elevation (m)`
* `Year`
* `Month`
* `DayOfYear`

---

# 2. Metodología

## 2.1. Obtención y exploración de los datos

Los datos fueron obtenidos mediante el conjunto de datos de calidad del aire exterior proporcionado por la **U.S. Environmental Protection Agency (EPA)**.

Inicialmente se cargó el archivo CSV utilizando la biblioteca **Pandas** y se realizó una exploración general de la información disponible.

El conjunto de datos utilizado presenta:

* **10 136 registros**
* **28 columnas**
* Periodo: **2022–2023**
* Fecha inicial: **01/01/2022**
* Fecha final: **31/12/2023**
* **20 estaciones de monitoreo** identificadas mediante `Site ID`

También se revisaron los tipos de datos, las estadísticas descriptivas y la presencia de valores nulos.

La variable objetivo `Daily Max Ozone Concentration` presentó los siguientes valores descriptivos:

| Estadístico         |   Valor |
| ------------------- | ------: |
| Registros           |  10 136 |
| Media               | 0.04124 |
| Desviación estándar | 0.01041 |
| Mínimo              |   0.000 |
| Primer cuartil      |   0.034 |
| Mediana             |   0.041 |
| Tercer cuartil      |   0.048 |
| Máximo              |   0.082 |

El valor medio del `Daily AQI Value` fue aproximadamente **39.26**, con un mínimo de **0** y un máximo de **140**.

---

## 2.2. Preparación de los datos

La columna `Date` fue convertida al formato de fecha mediante Pandas.

A partir de esta variable se generaron tres variables temporales:

* `Year`: año de la medición.
* `Month`: mes de la medición.
* `DayOfYear`: día del año.

Estas variables permitieron incorporar información temporal al modelo de regresión.

Posteriormente, se seleccionaron las variables independientes y la variable dependiente.

### Variable dependiente

**`Daily Max Ozone Concentration`**

Representa la concentración máxima diaria de ozono registrada en el conjunto de datos.

### Variables independientes

**`Daily AQI Value`**

Representa el valor diario del índice de calidad del aire disponible en el registro.

**`Site Latitude`**

Representa la latitud geográfica de la estación de monitoreo.

**`Site Longitude`**

Representa la longitud geográfica de la estación de monitoreo.

**`Elevation (m)`**

Representa la elevación de la estación de monitoreo en metros.

**`Year`**

Representa el año en que se realizó la medición.

**`Month`**

Representa el mes correspondiente a la medición.

**`DayOfYear`**

Representa el número de día dentro del año.

Los registros que presentaban valores nulos en las variables utilizadas para el modelo fueron eliminados antes del entrenamiento.

---

## 2.3. Análisis de correlación

Para analizar la relación lineal entre las variables numéricas se calculó una **matriz de correlación**.

El coeficiente de correlación entre `Daily Max Ozone Concentration` y `Daily AQI Value` fue aproximadamente:

```text
r = 0.9474
```

Este resultado representa una relación lineal positiva fuerte dentro de los datos analizados.

Las demás variables presentaron relaciones menores con la concentración máxima diaria de ozono.

Los coeficientes de correlación con la variable objetivo fueron:

| Variable        | Correlación |
| --------------- | ----------: |
| Daily AQI Value |      0.9474 |
| Year            |      0.1533 |
| Site Latitude   |      0.0880 |
| Elevation (m)   |      0.0832 |
| Site Longitude  |      0.0751 |
| DayOfYear       |     -0.1059 |
| Month           |     -0.1130 |

La correlación permite identificar asociaciones lineales, pero no implica por sí misma una relación causal entre las variables.

---

## 2.4. División de los datos

Para construir y evaluar el modelo se utilizó la función `train_test_split()` de **Scikit-learn**.

Se utilizó la siguiente distribución:

* **70 % para entrenamiento**
* **30 % para prueba**
* `random_state = 123`

Después de eliminar los registros con valores faltantes en las variables utilizadas, se obtuvieron:

* **10 136 registros** para el modelo.
* **7 095 registros** para entrenamiento.
* **3 041 registros** para prueba.

Esta separación permite entrenar el modelo utilizando una parte de los datos y evaluar posteriormente su comportamiento utilizando registros que no participaron directamente en el entrenamiento.

---

## 2.5. Entrenamiento del modelo

Se utilizó un modelo de **regresión lineal múltiple** mediante la clase `LinearRegression()` de la biblioteca Scikit-learn.

El modelo utiliza las siete variables seleccionadas para estimar:

`Daily Max Ozone Concentration`

Los coeficientes obtenidos fueron:

| Variable        | Coeficiente |
| --------------- | ----------: |
| Daily AQI Value |   0.0007697 |
| Site Latitude   |   0.0000131 |
| Site Longitude  |   0.0001878 |
| Elevation (m)   | 0.000000357 |
| Year            |   0.0002985 |
| Month           |  -0.0006025 |
| DayOfYear       |   0.0000184 |

El intercepto obtenido fue aproximadamente:

```text
-0.57625
```

Los coeficientes representan la variación estimada de la variable objetivo asociada a un cambio de una unidad en cada variable predictora, manteniendo constantes las demás variables del modelo.

---

# 3. Resultados

## 3.1. Distribución de la concentración de ozono

La primera gráfica muestra la distribución de los valores de `Daily Max Ozone Concentration`.

La mayor concentración de observaciones se encuentra alrededor de los valores centrales de la distribución, mientras que los valores más elevados presentan una menor frecuencia.

La concentración máxima registrada en los datos analizados fue de **0.082**, mientras que la media fue aproximadamente **0.04124**.

<p align="center">
  <img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/919bd49b-323a-46a5-80e6-d468a84bd242" />

  <br>
  <em>Figura 1. Distribución de la concentración máxima diaria de ozono.</em>
</p>

---

## 3.2. Matriz de correlación

La matriz de correlación permite observar las relaciones lineales entre las variables utilizadas en el análisis.

La relación más alta con la concentración máxima diaria de ozono corresponde a `Daily AQI Value`, con un coeficiente de aproximadamente **0.9474**.

Esto indica que, dentro del conjunto de datos analizado, los registros con valores mayores de AQI tienden a presentar también mayores valores de concentración máxima diaria de ozono.

<p align="center">
  <img width="1021" height="790" alt="image" src="https://github.com/user-attachments/assets/a0985547-f6f6-451b-bfa0-4bc932081ff4" />

  <br>
  <em>Figura 2. Matriz de correlación de las variables utilizadas.</em>
</p>

---

## 3.3. Relación entre las variables predictoras y el ozono

Para complementar el análisis de correlación se visualizaron las relaciones entre las variables predictoras y la concentración máxima diaria de ozono.

Estas gráficas permiten observar visualmente cómo se distribuyen los registros y si existe alguna tendencia entre las variables independientes y la variable objetivo.

La relación más evidente corresponde a `Daily AQI Value`, debido a la alta correlación positiva encontrada anteriormente.

<p align="center">
  <img width="987" height="690" alt="image" src="https://github.com/user-attachments/assets/5a18a8fd-3e2c-4e3f-8d50-27070af6c717" />

  <br>
  <em>Figura 3. Relación entre las variables predictoras y la concentración máxima diaria de ozono.</em>
</p>

---

## 3.4. Valores reales frente a valores predichos

Después del entrenamiento del modelo se realizaron predicciones utilizando los **3 041 registros de prueba**.

La siguiente gráfica compara los valores reales de concentración de ozono con los valores estimados por el modelo.

Los puntos cercanos a la línea diagonal representan predicciones próximas a los valores reales. La dispersión de los puntos permite visualizar el nivel de ajuste alcanzado por el modelo.

<p align="center">
  <img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/4f56a24f-9a08-46fa-911a-95c3a146af71" />

  <br>
  <em>Figura 4. Comparación entre los valores reales y los valores predichos de ozono.</em>
</p>

---

## 3.5. Análisis de residuos

Los residuos representan la diferencia entre el valor real y el valor predicho por el modelo.

El análisis de residuos permite identificar visualmente posibles patrones en los errores de predicción. Una distribución de residuos alrededor de cero, sin patrones claramente definidos, es consistente con un comportamiento adecuado del modelo para los datos utilizados.

<p align="center">
  <img width="988" height="690" alt="image" src="https://github.com/user-attachments/assets/af16daa5-4541-47a4-b1ed-2f9c8fedf81b" />

  <br>
  <em>Figura 5. Análisis de los residuos del modelo de regresión lineal.</em>
</p>

---

## 3.6. Métricas del modelo

Para evaluar el rendimiento del modelo se utilizaron las métricas **MSE**, **RMSE**, **MAE** y **R²**.

Los resultados obtenidos sobre los datos de prueba fueron:

| Métrica |  Resultado |
| ------- | ---------: |
| MSE     | 0.00001072 |
| RMSE    |    0.00327 |
| MAE     |    0.00228 |
| R²      |     0.8987 |

El modelo obtuvo un **R² de aproximadamente 0.8987** sobre los datos de prueba. Esto significa que el modelo explica aproximadamente el **89.87 % de la variabilidad observada** en la concentración máxima diaria de ozono dentro de este conjunto de prueba.

El valor de RMSE fue aproximadamente **0.00327**, mientras que el MAE fue **0.00228**.

En los datos de entrenamiento se obtuvo un R² de aproximadamente **0.8982**, mientras que en los datos de prueba fue **0.8987**.

La cercanía entre ambos valores permite observar que el rendimiento obtenido en entrenamiento y prueba fue similar.

---

# 4. Discusión

Los resultados muestran una relación lineal elevada entre `Daily AQI Value` y `Daily Max Ozone Concentration`, con una correlación aproximada de **0.9474**.

Esta variable también presentó el mayor coeficiente dentro de la matriz de correlación respecto a la variable objetivo. Sin embargo, la correlación no debe interpretarse como una relación causal, ya que el AQI es un indicador construido a partir de información relacionada con la calidad del aire.

Las variables temporales y geográficas presentaron relaciones lineales considerablemente menores. Esto indica que, dentro de la estructura utilizada en este modelo, estas variables aportan información adicional, pero presentan una asociación individual menor con la concentración de ozono.

El modelo de regresión lineal múltiple alcanzó un R² de **0.8987** sobre los datos de prueba. Las gráficas de valores reales frente a predichos y de residuos permiten complementar la evaluación numérica del modelo.

Para futuros análisis podría ser útil incorporar otras variables ambientales que permitan representar mejor las condiciones que influyen en la concentración de ozono, siempre que estas se encuentren disponibles en el conjunto de datos.

---

# 5. Conclusiones

El análisis permitió aplicar un modelo de **regresión lineal múltiple** a datos diarios de calidad del aire de la EPA correspondientes al periodo **2022–2023**.

Se trabajó con **10 136 registros** y se utilizaron siete variables predictoras para estimar la `Daily Max Ozone Concentration`.

La variable que presentó la mayor relación lineal con la concentración máxima diaria de ozono fue `Daily AQI Value`, con una correlación aproximada de **0.9474**.

El modelo obtuvo un **R² de 0.8987** sobre los datos de prueba, además de un **MSE de 0.00001072**, un **RMSE de 0.00327** y un **MAE de 0.00228**.

El análisis gráfico permitió observar la distribución de los datos, las relaciones entre las variables, la comparación entre valores reales y predichos y el comportamiento de los residuos.

En conjunto, el procedimiento permitió aplicar las principales etapas de un análisis de regresión: exploración de datos, preparación de variables, análisis de correlación, división de los datos, entrenamiento del modelo, generación de predicciones y evaluación mediante métricas.

---

# 6. Referencias

[1] U.S. Environmental Protection Agency, “Outdoor Air Quality Data,” *U.S. Environmental Protection Agency*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data

[2] U.S. Environmental Protection Agency, “Ozone Pollution,” *U.S. Environmental Protection Agency*. [En línea]. Disponible en: https://www.epa.gov/ozone-pollution

[3] U.S. Environmental Protection Agency, “Air Quality Index (AQI) Basics,” *AirNow*. [En línea]. Disponible en: https://www.airnow.gov/aqi/aqi-basics/

[4] Scikit-learn Developers, “LinearRegression,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html

[5] Scikit-learn Developers, “train_test_split,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html

[6] U.S. Environmental Protection Agency, *Ozone Daily Data*, datos de calidad del aire correspondientes al periodo 2022–2023.
