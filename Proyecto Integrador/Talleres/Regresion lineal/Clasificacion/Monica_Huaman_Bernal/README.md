<div align="center">

# Taller de Regresión Lineal y Modelos Predictivos

### Análisis de la concentración de monóxido de carbono (CO)

**Estudiante:** Mónica Huamán Bernal  
**Equipo:** Equipo 06  
**Curso:** Proyecto Integrador

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-3B4F7D?style=for-the-badge&logo=python&logoColor=white)

</div>

---

## 1. Introducción
El **monóxido de carbono (CO)** es un contaminante atmosférico asociado principalmente a procesos de combustión. Su presencia en el aire puede representar un riesgo para la salud humana, por lo que el monitoreo de sus concentraciones permite caracterizar la calidad del aire y analizar su comportamiento en diferentes lugares y periodos.

En el presente trabajo se realizó un análisis estadístico de datos de calidad del aire correspondientes al **monóxido de carbono (CO)** en el área metropolitana de **Birmingham-Hoover, Alabama, Estados Unidos**, durante el periodo comprendido entre el **1 de enero de 2022 y el 31 de diciembre de 2023**. El conjunto de datos contiene **1876 observaciones**, provenientes de los sitios de monitoreo *North Birmingham*, *Fairfield* y *Arkadelphia/Near Road*. Los datos fueron obtenidos de la plataforma **AirData de la U.S. Environmental Protection Agency (EPA)** [1].

El objetivo principal fue analizar la relación entre la **concentración máxima diaria de CO**, utilizada como variable dependiente, y diferentes características disponibles en el conjunto de datos. Para ello, se realizó una exploración inicial de las variables, un análisis de correlación y posteriormente se construyó un **modelo de regresión lineal múltiple**.

La finalidad del análisis fue determinar qué variables podían utilizarse como predictores de la concentración máxima diaria de CO y evaluar el comportamiento estadístico y la capacidad explicativa del modelo obtenido.

### 1.1. Características del estudio

| Elemento | Descripción |
|---|---|
| **Contaminante** | Monóxido de carbono (CO) |
| **País** | Estados Unidos |
| **Estado** | Alabama |
| **Área metropolitana** | Birmingham-Hoover, Alabama |
| **Periodo de estudio** | 2022–2023 |
| **Número de observaciones** | 1876 |
| **Número de variables originales** | 28 |
| **Sitios de monitoreo** | North Birmingham, Fairfield y Arkadelphia/Near Road |
| **Variable dependiente** | `Daily Max CO Concentration` |
| **Variables independientes seleccionadas** | `Daily Obs Count`, `Site Latitude` y `Elevation (m)` |
| **Método estadístico** | Regresión lineal múltiple |
| **División de los datos** | 70 % entrenamiento y 30 % prueba |
| **Fuente de datos** | U.S. Environmental Protection Agency (EPA), AirData [1] |

---

## 2. Metodología

### 2.1. Descripción y carga de los datos

Los datos utilizados corresponden a registros de calidad del aire para el contaminante **monóxido de carbono (CO)** durante el periodo **2022–2023**, en el área metropolitana de **Birmingham-Hoover, Alabama, Estados Unidos**.

El conjunto de datos contiene **28 variables y 1876 observaciones**. Entre las variables disponibles se encuentran la fecha de medición, identificación del sitio, concentración máxima diaria de CO, valor diario del índice de calidad del aire (AQI), número de observaciones diarias, porcentaje de completitud, coordenadas geográficas, elevación y características relacionadas con las estaciones de monitoreo.

Los datos fueron importados a Python mediante la función `read_csv()` de la biblioteca **Pandas**:

    df = pd.read_csv('/content/CO_daily_aqs_data_downloaded_2026-09-17 21_16_44.csv')

Para realizar una primera revisión del conjunto de datos se utilizaron las funciones `head()`, `info()` y `describe()`. Estas permitieron observar las primeras filas, identificar los tipos de datos y valores faltantes, y obtener estadísticas descriptivas de las variables numéricas.

### 2.2. Exploración de los datos

Se realizó un análisis exploratorio con el objetivo de conocer las características de las variables y observar posibles relaciones entre ellas.

En primer lugar, se utilizó la función `pairplot()` de **Seaborn** para representar gráficamente las relaciones entre las variables del conjunto de datos:

    sns.pairplot(df)

Asimismo, se analizó la distribución de la variable dependiente, **Daily Max CO Concentration**, mediante un histograma:

    df['Daily Max CO Concentration'].plot.hist(bins=25, figsize=(8,4))

También se elaboró una gráfica de densidad:

    df['Daily Max CO Concentration'].plot.density()

Estas representaciones permitieron observar la distribución de las concentraciones de CO registradas antes de realizar el modelamiento.

### 2.3. Análisis de correlación y selección de variables

Para estudiar las relaciones lineales entre las variables cuantitativas, se seleccionaron las columnas numéricas mediante:

    numeric_df = df.select_dtypes(include=[np.number])

Posteriormente, se calculó la matriz de correlación utilizando la función `corr()`:

    numeric_df.corr().round(3)

La matriz de correlación también fue representada mediante un mapa de calor:

    sns.heatmap(numeric_df.corr(), annot=True, linewidths=2)

El análisis permitió identificar relaciones fuertes entre algunas variables. Entre las principales correlaciones observadas se encontraron:

- **Daily Max CO Concentration – Daily AQI Value:** 0.992
- **Daily Obs Count – Percent Complete:** 1.000
- **Site Latitude – Site Longitude:** 0.986

Debido a estas relaciones, se evaluó la posible redundancia entre los predictores antes de construir el modelo.

La variable **Daily AQI Value** no fue incorporada al modelo final debido a su relación extremadamente alta con la concentración de CO. Incluir una variable tan estrechamente relacionada con la variable dependiente podría producir un modelo con una capacidad explicativa artificialmente elevada.

Asimismo, **Percent Complete** fue descartada debido a su correlación perfecta con **Daily Obs Count**, mientras que **Site Longitude** fue excluida debido a su elevada correlación con **Site Latitude**.

Finalmente, se estableció como variable dependiente:

**`Daily Max CO Concentration`**

y como variables independientes:

| Variable | Descripción |
|---|---|
| `Daily Obs Count` | Número de observaciones utilizadas en el registro diario |
| `Site Latitude` | Latitud geográfica del sitio de monitoreo |
| `Elevation (m)` | Elevación del sitio de monitoreo en metros |

Antes del ajuste del modelo se verificó que estas tres variables predictoras no presentaran valores faltantes.

### 2.4. División de los datos

Para evaluar el comportamiento del modelo con observaciones que no fueran utilizadas durante su entrenamiento, el conjunto de datos se dividió en un **70 % para entrenamiento y 30 % para prueba** mediante la función `train_test_split()` de **scikit-learn**.

    from sklearn.model_selection import train_test_split

    X_train, X_test, y_train, y_test = train_test_split(
        X,
        y,
        test_size=0.3,
        random_state=123
    )

La división produjo:

- **1313 observaciones para entrenamiento**
- **563 observaciones para prueba**

Se utilizó `random_state=123` para garantizar que la división pudiera reproducirse.

### 2.5. Construcción del modelo de regresión lineal

Se empleó un modelo de **regresión lineal múltiple**, debido a que se buscó estudiar la relación entre una variable dependiente y tres variables independientes.

La variable dependiente fue:

    y = df['Daily Max CO Concentration']

y las variables predictoras fueron:

    X = df[
        [
            'Daily Obs Count',
            'Site Latitude',
            'Elevation (m)'
        ]
    ]

El modelo fue implementado mediante `LinearRegression()` de **scikit-learn**:

    from sklearn.linear_model import LinearRegression

    lm = LinearRegression()
    lm.fit(X_train, y_train)

La forma general del modelo de regresión utilizado fue:

**CO estimado = β₀ + β₁(Daily Obs Count) + β₂(Site Latitude) + β₃(Elevation)**

donde:

- **CO estimado** representa la concentración máxima diaria de CO estimada por el modelo.
- **β₀** representa el intercepto.
- **β₁**, **β₂** y **β₃** representan los coeficientes asociados a cada variable predictora.

A partir del ajuste se obtuvieron los coeficientes del modelo. También se calcularon los errores estándar y los estadísticos *t* de los coeficientes como parte del análisis estadístico.

### 2.6. Predicción y evaluación del modelo

Una vez entrenado el modelo, se generaron predicciones para el conjunto de prueba mediante la función `predict()`:

    predictions = lm.predict(X_test)

El desempeño predictivo del modelo se evaluó mediante las siguientes métricas:

- **MAE (Mean Absolute Error):** mide el error absoluto promedio entre los valores observados y los valores predichos.
- **MSE (Mean Squared Error):** calcula el promedio de los errores al cuadrado.
- **RMSE (Root Mean Squared Error):** corresponde a la raíz cuadrada del MSE y permite expresar el error en las mismas unidades de la variable dependiente.
- **R² (coeficiente de determinación):** indica la proporción de la variabilidad de la variable dependiente explicada por el modelo.

Las métricas fueron calculadas mediante funciones de `sklearn.metrics`.

También se realizó una comparación gráfica entre los valores reales y los valores predichos de la concentración de CO.

### 2.7. Análisis y diagnóstico de residuos

Se realizó un análisis de los **residuos** con el propósito de evaluar el comportamiento de los errores del modelo.

El residuo de cada observación se calculó como:

$$
e_i = y_i-\widehat{y}_i
$$

donde **yᵢ** representa el valor observado y **ŷᵢ** representa el valor predicho por el modelo.
Para analizar los residuos se utilizaron:

- Histograma de residuos.
- Residuos frente a los valores predichos.
- Residuos frente al número de observaciones.
- Residuos frente a la latitud.
- Residuos frente a la elevación.

Estas representaciones permitieron evaluar visualmente la distribución de los errores, la presencia de patrones sistemáticos y posibles agrupamientos en los residuos.

Finalmente, se utilizó la biblioteca **Statsmodels** para realizar un ajuste mediante **mínimos cuadrados ordinarios (OLS, Ordinary Least Squares)** y obtener pruebas estadísticas adicionales:

    import statsmodels.api as sm

    Xs = sm.add_constant(X)

    stat_model = sm.OLS(y, Xs)
    stat_result = stat_model.fit()

    print(stat_result.summary())

El resumen estadístico obtenido mediante OLS permitió analizar:

- $R^2$ y $R^2$ ajustado.
- Estadístico **F** y su valor *p*.
- Coeficientes de regresión.
- Errores estándar.
- Estadísticos *t*.
- Valores *p* de los coeficientes.
- Intervalos de confianza.
- Estadísticas de diagnóstico de los residuos, incluyendo **Durbin-Watson**, **Jarque-Bera**, asimetría y curtosis.

Estos resultados fueron utilizados posteriormente para evaluar la significancia estadística del modelo y analizar sus principales características.

---

## 3. Resultados

### 3.1. Análisis exploratorio

#### Distribución de la concentración de CO

**Figura 1. Histograma de la concentración máxima diaria de CO.**

<div align="center">

<img width="695" height="351" alt="image" src="https://github.com/user-attachments/assets/8b7ece28-a395-4c0a-b65f-fa4d227e01f6" />


</div>

**Figura 2. Distribución de densidad de la concentración máxima diaria de CO.**

<div align="center">

<img width="567" height="413" alt="image" src="https://github.com/user-attachments/assets/88364e22-6eee-421a-a97d-a9d0d9760190" />



</div>

#### Relaciones entre las variables

**Figura 3. Pairplot de la variable dependiente y las variables predictoras seleccionadas.**

<div align="center">

<img width="985" height="986" alt="image" src="https://github.com/user-attachments/assets/82adaa17-41eb-45fa-8770-b07e9c2492b5" />


</div>

**Figura 4. Matriz de correlación de las variables numéricas.**

<div align="center">

<img width="820" height="539" alt="image" src="https://github.com/user-attachments/assets/4f5b5c58-bb02-455f-88d6-dd5a5c1cafc0" />

</div>

### 3.2. Relación entre las variables predictoras y la concentración de CO

**Figura 5. Relación entre el número de observaciones y la concentración máxima diaria de CO.**

<div align="center">

<img width="562" height="543" alt="image" src="https://github.com/user-attachments/assets/ee978289-3513-48a0-96f3-25bd31bdc024" />


</div>

**Figura 6. Relación entre la latitud y la concentración máxima diaria de CO.**

<div align="center">

<img width="565" height="537" alt="image" src="https://github.com/user-attachments/assets/c38f0913-ad05-469e-ac7a-100ca2aea69a" />


</div>

**Figura 7. Relación entre la elevación y la concentración máxima diaria de CO.**

<div align="center">

<img width="550" height="537" alt="image" src="https://github.com/user-attachments/assets/58e5444d-2125-4d5b-9240-73b65a89cb52" />


</div>

### 3.3. Coeficientes del modelo

**Figura 8. Coeficientes obtenidos para las variables independientes del modelo de regresión lineal.**

<div align="center">

<img width="586" height="157" alt="image" src="https://github.com/user-attachments/assets/5ec861fe-3cba-4cef-a729-61b1fec90708" />


</div>

### 3.4. Evaluación predictiva

Los valores obtenidos para las métricas de evaluación del modelo fueron:

| Métrica | Resultado |
|---|---:|
| MAE | 0.1353 |
| MSE | 0.0295 |
| RMSE | 0.1717 |
| R² | 0.2146 |

**Figura 9. Comparación entre los valores reales y los valores predichos de la concentración de CO.**

<div align="center">

<img width="707" height="409" alt="image" src="https://github.com/user-attachments/assets/747fdbda-052e-4e34-ab9b-e362841affe8" />


</div>

### 3.5. Diagnóstico de residuos

**Figura 10. Histograma de los residuos del modelo.**

<div align="center">

<img width="684" height="407" alt="image" src="https://github.com/user-attachments/assets/25164b3e-efbe-4c7b-9444-2665b762e343" />

</div>

**Figura 11. Residuos frente a los valores predichos.**

<div align="center">

<img width="863" height="640" alt="image" src="https://github.com/user-attachments/assets/ef132c5b-64c6-451d-be0f-4bf1b1b6ddee" />


</div>

**Figura 12. Residuos frente al número de observaciones.**

<div align="center">

<img width="708" height="407" alt="image" src="https://github.com/user-attachments/assets/c9543e49-112d-492b-b60a-883a062cc8b2" />

</div>

**Figura 13. Residuos frente a la latitud.**

<div align="center">

<img width="708" height="407" alt="image" src="https://github.com/user-attachments/assets/fddf98e1-8f56-449d-b0d5-7e2b583d4c77" />


</div>

**Figura 14. Residuos frente a la elevación.**

<div align="center">

<img width="716" height="408" alt="image" src="https://github.com/user-attachments/assets/b3190fd1-04a0-49d3-9c05-b7de2854d53e" />


</div>

### 3.6. Resultados estadísticos del modelo OLS

El modelo de regresión lineal múltiple ajustado mediante OLS presentó los siguientes resultados:

| Variable | Coeficiente | Error estándar | Estadístico t | Valor p |
|---|---:|---:|---:|---:|
| Constante | -97.5640 | 6.104 | -15.984 | < 0.001 |
| Daily Obs Count | 0.0033 | 0.001 | 2.305 | 0.021 |
| Site Latitude | 2.7626 | 0.176 | 15.663 | < 0.001 |
| Elevation (m) | 0.0289 | 0.002 | 14.456 | < 0.001 |

El modelo presentó un **R² de 0.141** y un **R² ajustado de 0.139**. El estadístico F fue **102.2**, con un valor p de **2.69 × 10⁻⁶¹**.

---

## 4. Discusión

Los resultados muestran que las variables seleccionadas presentan una relación estadísticamente significativa con la concentración máxima diaria de CO dentro del modelo OLS. Sin embargo, el valor de R² obtenido (0.141) indica que una proporción limitada de la variabilidad de la concentración de CO es explicada por las variables incluidas.

Asimismo, el análisis de residuos evidenció desviaciones respecto a la normalidad y una posible autocorrelación, por lo que los resultados deben interpretarse considerando las características temporales y espaciales de los datos. La exclusión de Daily AQI Value también fue relevante para evitar que una variable altamente relacionada con la concentración de CO dominara el modelo.
---

## 5. Conclusiones

1. Se analizó un conjunto de datos de calidad del aire correspondiente al **monóxido de carbono (CO)** en el área metropolitana de **Birmingham-Hoover, Alabama, Estados Unidos**, durante los años **2022 y 2023**, con un total de **1876 observaciones**.

2. A partir del análisis exploratorio y de correlación se seleccionaron como variables predictoras **Daily Obs Count**, **Site Latitude** y **Elevation (m)**, utilizando **Daily Max CO Concentration** como variable dependiente.

3. El análisis de correlación permitió identificar relaciones muy elevadas entre algunas variables. Por ello, **Daily AQI Value**, **Percent Complete** y **Site Longitude** no fueron incorporadas al modelo final debido a su elevada relación con otras variables del conjunto de datos.

4. El modelo de regresión lineal múltiple obtuvo un **R² de 0.141** mediante el análisis OLS sobre el conjunto completo de datos. En el conjunto de prueba se obtuvo un **R² de 0.2146**, junto con un **RMSE de 0.1717**.

5. En el modelo OLS, las variables **Daily Obs Count**, **Site Latitude** y **Elevation (m)** presentaron valores p inferiores a 0.05, indicando una asociación estadísticamente significativa con la concentración máxima diaria de CO dentro del modelo.

6. El análisis de residuos mostró desviaciones respecto al supuesto de normalidad y un valor de Durbin-Watson de **1.010**, lo que sugiere la posible presencia de autocorrelación positiva.

7. En conjunto, el análisis permitió identificar relaciones estadísticas entre las características de los sitios de monitoreo y la concentración máxima diaria de CO, aunque las variables seleccionadas explican solo una parte de la variabilidad observada.
---

## 6. Referencias

[1] U.S. Environmental Protection Agency, “AirData,” U.S. EPA. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data/airdata. [Accessed: Sep. 17, 2026].

---

## 7. Código

El código completo utilizado para el procesamiento de los datos, análisis exploratorio, construcción del modelo de regresión lineal y evaluación estadística se encuentra disponible en Google Colab.

<div align="center">

### 💻 Proyecto en Google Colab

<(https://colab.research.google.com/drive/11AuGiA9RQU85YKpOPQVKpLI2hEEK1x2M?usp=sharing)>
  <img src="https://img.shields.io/badge/Abrir%20en-Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Abrir en Google Colab">
</a>

<br><br>

**Proyecto Integrador — Equipo 06**

</div>
