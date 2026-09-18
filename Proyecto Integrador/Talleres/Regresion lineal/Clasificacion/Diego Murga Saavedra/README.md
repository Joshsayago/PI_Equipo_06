# PM2.5 en Albuquerque, Nuevo México — 2023

## 1. Introducción

La contaminación del aire puede analizarse mediante diferentes contaminantes presentes en la atmósfera. Uno de ellos es el **PM2.5**, compuesto por partículas finas con un diámetro igual o menor a 2.5 µm. Debido a su pequeño tamaño, estas partículas pueden ingresar al sistema respiratorio y afectar la salud de las personas [1].

Otro indicador utilizado para evaluar la calidad del aire es el **Air Quality Index (AQI)** o Índice de Calidad del Aire. Este índice representa mediante un valor numérico el nivel de contaminación presente en el aire, donde valores mayores indican una peor calidad del aire [2].

En este trabajo se utilizó el archivo `ad_viz_plotval_data.csv`, el cual contiene información de calidad del aire correspondiente al año **2023** para el área de **Albuquerque, Nuevo México**.

El conjunto de datos contiene **3,804 registros y 22 variables**, correspondientes a diferentes estaciones de monitoreo.

El objetivo del trabajo fue aplicar un modelo de **regresión lineal múltiple** para analizar la relación entre diferentes variables disponibles en el conjunto de datos y la concentración media diaria de **PM2.5**.

Las variables utilizadas como predictoras fueron:

* `Daily AQI Value`
* `Site ID`
* `Site Latitude`
* `Site Longitude`

La variable que se desea predecir fue:

* `Daily Mean PM2.5 Concentration`

---

## 2. Metodología

### 2.1. Exploración de los datos

Inicialmente se cargó el conjunto de datos mediante la biblioteca **Pandas** y se revisaron las dimensiones, columnas, tipos de datos y estadísticas descriptivas.

El dataset contiene:

* **3804 registros**
* **22 columnas**
* **6 estaciones de monitoreo**
* **0 valores nulos**
* **0 filas duplicadas**

Las estaciones presentes fueron:

* DEL NORTE HIGH SCHOOL
* JEFFERSON
* SOUTH VALLEY
* Foothills
* NORTH VALLEY
* San Jose

La variable `Daily Mean PM2.5 Concentration` presentó los siguientes valores:

| Estadístico         | PM2.5 |
| ------------------- | ----: |
| Registros           |  3804 |
| Media               |  6.01 |
| Desviación estándar |  3.71 |
| Mínimo              |  0.00 |
| Primer cuartil      |  3.70 |
| Mediana             |  5.00 |
| Tercer cuartil      |  7.20 |
| Máximo              | 44.30 |

Por otro lado, `Daily AQI Value` presentó una media aproximada de **31.35**, con un valor mínimo de **0** y un máximo de **123**.

### 2.2. Variables utilizadas

La variable dependiente seleccionada fue:

* **`Daily Mean PM2.5 Concentration`**: concentración media diaria de material particulado PM2.5.

Las variables independientes seleccionadas fueron:

1. **`Daily AQI Value`**: índice diario de calidad del aire.
2. **`Site ID`**: identificador de la estación de monitoreo.
3. **`Site Latitude`**: ubicación geográfica de la estación respecto a la latitud.
4. **`Site Longitude`**: ubicación geográfica de la estación respecto a la longitud.

### 2.3. Matriz de correlación

Para identificar la relación existente entre las variables numéricas seleccionadas se calculó una matriz de correlación.

La mayor relación se encontró entre:

`Daily Mean PM2.5 Concentration` y `Daily AQI Value`.

El coeficiente obtenido fue aproximadamente:

```math
r = 0.9582
```

Este valor cercano a 1 representa una **relación lineal positiva fuerte**.

Esto significa que, dentro de los datos analizados, los valores de PM2.5 tienden a aumentar conforme aumenta el AQI.

### 2.4. División de los datos

Para construir el modelo, los datos fueron divididos mediante `train_test_split()`.

Se utilizó:

* **70 % para entrenamiento**
* **30 % para prueba**
* `random_state = 123`

De los 3804 registros disponibles:

* **2662 registros** fueron utilizados para entrenamiento.
* **1142 registros** fueron utilizados para prueba.

Esta separación permite entrenar el modelo con una parte de los datos y posteriormente evaluar su comportamiento con datos que no fueron utilizados durante el entrenamiento.

### 2.5. Entrenamiento del modelo

Se utilizó `LinearRegression()` de la biblioteca **Scikit-learn**.

Después del entrenamiento se obtuvieron aproximadamente los siguientes coeficientes:

| Variable        | Coeficiente |
| --------------- | ----------: |
| Daily AQI Value |    0.244260 |
| Site ID         |    0.000206 |
| Site Latitude   |   -2.263241 |
| Site Longitude  |    3.987292 |

El intercepto obtenido fue aproximadamente:

```math
-71568.68
```

El coeficiente correspondiente a `Daily AQI Value` fue positivo, indicando que un incremento de una unidad en el AQI se relaciona, manteniendo constantes las demás variables, con un incremento aproximado de **0.244 µg/m³** en el PM2.5 estimado.

---

## 3. Resultados

### 3.1. Distribución del PM2.5

El histograma de la concentración media diaria de PM2.5 mostró que la mayor cantidad de observaciones se encuentra en valores bajos.

La media fue aproximadamente:

```math
6.01\ \mu g/m^3
```

Mientras que el valor máximo observado fue:

```math
44.3\ \mu g/m^3
```
La distribución presenta algunos valores elevados con menor frecuencia.

<p align = center>
  <img width="704" height="393" alt="image" src="https://github.com/user-attachments/assets/5e41febe-d491-4e90-a0c6-2b2ad6b7f6d3" />
  <br>
  <em>Figura 1. Distribución de la concentración media diaria de PM2.5.</em>
</p>

### 3.2. Correlación entre variables

La matriz de correlación mostró que `Daily AQI Value` presenta la relación más alta con PM2.5.

La correlación fue:

```math
r = 0.9582
```

Por otro lado, las variables relacionadas con la localización geográfica presentan relaciones menores:

* `Site ID`: aproximadamente **0.118**
* `Site Latitude`: aproximadamente **-0.270**
* `Site Longitude`: aproximadamente **-0.345**

Por lo tanto, el AQI es la variable que presenta la asociación lineal más fuerte con PM2.5.

<p align = center>
  <img width="985" height="818" alt="image" src="https://github.com/user-attachments/assets/03c9a288-bc5c-4a4c-a453-eceb8162d496" />
  <br>
  <em>Figura 2. Matriz de correlación entre las variables analizadas.</em>
</p>

<p align = center>
  <img width="1790" height="990" alt="image" src="https://github.com/user-attachments/assets/049bc2f5-d547-4091-8023-f5b86457da68" />
  <br>
  <em>Figura 3. Relación entre las variables predictoras y la concentración de PM2.5.</em>
</p>

### 3.3. Valores reales frente a valores predichos

Luego del entrenamiento del modelo se realizaron predicciones utilizando los **1142 registros de prueba**.

Al comparar gráficamente los valores reales de PM2.5 con los valores predichos se observa que una gran cantidad de puntos se encuentra próxima a una tendencia diagonal.

Esto indica que las predicciones generadas por el modelo se encuentran generalmente próximas a los valores reales.

<p align = center>
  <img width="760" height="573" alt="image" src="https://github.com/user-attachments/assets/967a0622-6fa3-4abd-b62c-c17c50928c76" />
  <br>
  <em>Figura 4. Comparación entre los valores reales y predichos de PM2.5.</em>
</p>

### 3.4. Error cuadrático medio

Para evaluar la diferencia entre los valores reales y los predichos se utilizó el **Mean Squared Error (MSE)**.

El resultado fue:

```math
MSE = 0.7662
```

Un valor pequeño de MSE indica que, en general, las predicciones realizadas por el modelo presentan errores reducidos.

También se obtuvo:

```math
RMSE = 0.8753
```

y:

```math
MAE = 0.6207
```

El MAE indica que la diferencia absoluta promedio entre el valor real de PM2.5 y el valor predicho es aproximadamente **0.62 µg/m³**.

### 3.5. Coeficiente de determinación

El coeficiente de determinación obtenido con el conjunto de prueba fue:

```math
R^2 = 0.9317
```

Esto significa que aproximadamente el **93.17 % de la variación de PM2.5** presente en el conjunto de prueba puede ser representada por el modelo lineal utilizado.

Para los datos de entrenamiento se obtuvo:

```math
R^2 = 0.9160
```

La similitud entre ambos valores indica que el modelo presenta un comportamiento consistente entre los datos utilizados para entrenar y los utilizados para probar.

### 3.6. Análisis de residuos

Los residuos representan la diferencia entre los valores reales y los valores estimados por el modelo:

```math
Residuo = Valor\ real - Valor\ predicho
```

Mediante el histograma de residuos se puede observar que gran parte de los errores se encuentra próxima a cero.

También se realizó un gráfico de residuos frente a valores predichos para comprobar visualmente si existe algún patrón en los errores.

Aunque la mayoría se encuentra alrededor de cero, aparecen algunos valores más alejados, principalmente asociados a observaciones con concentraciones mayores de PM2.5.

<p align = center>
  <img width="768" height="575" alt="image" src="https://github.com/user-attachments/assets/43291b75-83d0-48eb-b6b8-65bcf986426f" />
  <br>
  <em>Figura 5. Distribución de los residuos del modelo.</em>
</p>

<p align = center>
  <img width="768" height="576" alt="image" src="https://github.com/user-attachments/assets/f4cbb0af-23f8-4a3c-bb43-31c5fe10971b" />
  <br>
  <em>Figura 6. Residuos frente a los valores predichos por el modelo.</em>
</p>

---

## 4. Discusión

Los resultados muestran que el modelo de regresión lineal presenta un buen ajuste para los datos estudiados.

La variable con mayor relación con la concentración media diaria de PM2.5 fue `Daily AQI Value`, con una correlación de aproximadamente **0.9582**.

El modelo obtuvo un **R² de 0.9317** sobre los datos de prueba y un **MSE de 0.7662**, mostrando que las predicciones se encuentran generalmente próximas a los valores reales.

Sin embargo, la relación entre PM2.5 y AQI debe interpretarse con precaución. El AQI es un indicador que puede calcularse utilizando concentraciones de contaminantes como PM2.5. Por ello, resulta esperable encontrar una relación elevada entre ambas variables.

Por otro lado, variables como `Site ID`, latitud y longitud presentan una relación menor con la concentración de PM2.5. Estas variables permiten diferenciar las estaciones y sus ubicaciones, pero por sí solas no explican directamente los cambios diarios en la contaminación.

Para futuros modelos sería conveniente incorporar variables ambientales como temperatura, humedad, velocidad del viento o precipitación, ya que podrían aportar información adicional sobre las causas de las variaciones observadas en PM2.5.

---

## 5. Conclusiones

El análisis permitió aplicar un modelo de **regresión lineal múltiple** a un conjunto de 3804 registros de calidad del aire correspondientes al área de Albuquerque durante el año 2023.

La variable que presentó la mayor relación con la concentración diaria de PM2.5 fue `Daily AQI Value`, alcanzando una correlación aproximada de **0.9582**.

El modelo desarrollado obtuvo un coeficiente de determinación de **0.9317** con los datos de prueba, indicando un alto nivel de ajuste.

Asimismo, se obtuvo un MSE de **0.7662**, un RMSE de **0.8753** y un MAE de **0.6207**.

Los gráficos de valores reales frente a predichos y el análisis de residuos permitieron comprobar visualmente el comportamiento del modelo.

---

## 6. Referencias

[1] U.S. Environmental Protection Agency, “Particulate Matter (PM) Basics,” *U.S. EPA*. [En línea]. Disponible en: https://www.epa.gov/pm-pollution/particulate-matter-pm-basics

[2] U.S. Environmental Protection Agency, “AQI Basics,” *AirNow*. [En línea]. Disponible en: https://www.airnow.gov/aqi/aqi-basics/

[3] U.S. Environmental Protection Agency, “Outdoor Air Quality Data,” *U.S. EPA*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data

[4] Scikit-learn Developers, “LinearRegression,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html

[5] U.S. Environmental Protection Agency, *ad_viz_plotval_data.csv*, datos de calidad del aire, Albuquerque, Nuevo México, 2023.
