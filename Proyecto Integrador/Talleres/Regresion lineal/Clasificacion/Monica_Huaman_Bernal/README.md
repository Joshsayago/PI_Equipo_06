# Análisis de la concentración de monóxido de carbono (CO)

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

$$
\widehat{CO}
=
\beta_0
+
\beta_1(\text{Daily Obs Count})
+
\beta_2(\text{Site Latitude})
+
\beta_3(\text{Elevation})
$$

donde:

- $\widehat{CO}$ representa la concentración máxima diaria de CO estimada.
- $\beta_0$ representa el intercepto.
- $\beta_1$, $\beta_2$ y $\beta_3$ representan los coeficientes asociados a cada variable predictora.

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

donde $y_i$ representa el valor observado y $\widehat{y}_i$ el valor predicho por el modelo.

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

<<img width="695" height="351" alt="image" src="https://github.com/user-attachments/assets/8b7ece28-a395-4c0a-b65f-fa4d227e01f6" />
 />

</div>

**Figura 2. Distribución de densidad de la concentración máxima diaria de CO.**

<div align="center">

<img width="854" height="687" alt="Figura 2. Densidad de la concentración máxima diaria de CO" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

#### Relaciones entre las variables

**Figura 3. Matriz de relaciones entre las variables del conjunto de datos.**

<div align="center">

<img width="854" height="687" alt="Figura 3. Pairplot del conjunto de datos" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 4. Matriz de correlación de las variables numéricas.**

<div align="center">

<img width="854" height="687" alt="Figura 4. Matriz de correlación" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

### 3.2. Relación entre las variables predictoras y la concentración de CO

**Figura 5. Relación entre el número de observaciones y la concentración máxima diaria de CO.**

<div align="center">

<img width="854" height="687" alt="Figura 5. Número de observaciones vs. concentración de CO" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 6. Relación entre la latitud y la concentración máxima diaria de CO.**

<div align="center">

<img width="854" height="687" alt="Figura 6. Latitud vs. concentración de CO" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 7. Relación entre la elevación y la concentración máxima diaria de CO.**

<div align="center">

<img width="854" height="687" alt="Figura 7. Elevación vs. concentración de CO" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

### 3.3. Coeficientes del modelo

**Figura 8. Coeficientes obtenidos para las variables independientes del modelo de regresión lineal.**

<div align="center">

<img width="854" height="687" alt="Figura 8. Coeficientes del modelo" src="PEGAR_AQUÍ_LA_IMAGEN" />

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

<img width="854" height="687" alt="Figura 9. Valores reales vs. valores predichos" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

### 3.5. Diagnóstico de residuos

**Figura 10. Histograma de los residuos del modelo.**

<div align="center">

<img width="854" height="687" alt="Figura 10. Histograma de residuos" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 11. Residuos frente a los valores predichos.**

<div align="center">

<img width="854" height="687" alt="Figura 11. Residuos vs. valores predichos" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 12. Residuos frente al número de observaciones.**

<div align="center">

<img width="854" height="687" alt="Figura 12. Residuos vs. número de observaciones" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 13. Residuos frente a la latitud.**

<div align="center">

<img width="854" height="687" alt="Figura 13. Residuos vs. latitud" src="PEGAR_AQUÍ_LA_IMAGEN" />

</div>

**Figura 14. Residuos frente a la elevación.**

<div align="center">

<img width="854" height="687" alt="Figura 14. Residuos vs. elevación" src="PEGAR_AQUÍ_LA_IMAGEN" />

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

Los resultados obtenidos serán interpretados considerando el comportamiento de las variables predictoras, la capacidad explicativa del modelo, las métricas de predicción y los resultados del análisis de residuos.

---

## 5. Conclusiones

A partir del análisis realizado se establecerán las principales conclusiones respecto a la relación entre las variables seleccionadas y la concentración máxima diaria de CO.

---

## 6. Referencias

[1] U.S. Environmental Protection Agency, “AirData,” U.S. EPA. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data/airdata. [Accessed: Sep. 17, 2026].
