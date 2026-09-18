<div align="center">

# Análisis de la concentración máxima diaria de SO₂ durante 2023

### Aplicación de un modelo de regresión lineal múltiple

**Autora:** Bertha Dominik Belevan Amaro  
**Periodo analizado:** 1 de enero al 31 de diciembre de 2023  
**Fuente de datos:** AirData, U.S. Environmental Protection Agency (EPA)

<br>

<a href="https://colab.research.google.com/drive/1F7S03kBMQJXqDwyC29e1_V9tsNu30VTL#scrollTo=gIpXJySHvm7w">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir análisis en Google Colab">
</a>

</div>

---

## Resumen

Se analizaron 1774 registros de concentración máxima diaria de dióxido de azufre (SO₂) correspondientes a cinco estaciones de monitoreo durante 2023. Se realizó un análisis exploratorio y se ajustó un modelo de regresión lineal múltiple utilizando como predictores el número de observaciones diarias, la latitud y la elevación. El modelo obtuvo un MAE de 3.0310 ppb, un RMSE de 6.9383 ppb y un $R^2$ de prueba de 0.1182. Los resultados evidenciaron diferencias entre estaciones y una capacidad predictiva limitada para representar concentraciones extremas. El estudio permite reconocer el valor y las limitaciones de la regresión lineal en el análisis exploratorio de contaminantes atmosféricos.

**Palabras clave:** dióxido de azufre, calidad del aire, regresión lineal múltiple, contaminación atmosférica, Python.

---

## Introducción

El dióxido de azufre (SO₂) es un contaminante atmosférico gaseoso. Sus principales fuentes incluyen la combustión de combustibles fósiles en centrales eléctricas e instalaciones industriales, además de determinados procesos industriales y fuentes naturales [1]. La exposición de corta duración puede afectar el sistema respiratorio y dificultar la respiración, especialmente en personas con asma [1]. Asimismo, los óxidos de azufre pueden contribuir a la formación de partículas finas y lluvia ácida [1].

En este trabajo se analizaron los registros de concentración máxima diaria de SO₂ correspondientes exclusivamente al año **2023**. Los datos fueron obtenidos de AirData, plataforma de la Agencia de Protección Ambiental de los Estados Unidos (EPA) que permite acceder a datos recientes e históricos de calidad del aire [2]. Estos registros forman parte del Air Quality System (AQS), repositorio que reúne mediciones ambientales, información geográfica de las estaciones y elementos de control de calidad [3].

El propósito del estudio fue describir la distribución de las concentraciones, comparar los resultados entre estaciones y construir un modelo de **regresión lineal múltiple** para evaluar la relación entre la concentración máxima diaria de SO₂ y tres variables disponibles en el conjunto de datos: número de observaciones diarias, latitud y elevación de la estación.

### Objetivo general

Analizar la concentración máxima diaria de dióxido de azufre registrada durante 2023 mediante técnicas estadísticas y un modelo de regresión lineal múltiple.

### Objetivos específicos

- Examinar la estructura y distribución de los registros de SO₂.
- Comparar la concentración promedio entre las estaciones de monitoreo.
- Evaluar las correlaciones entre las variables numéricas.
- Construir un modelo de regresión lineal múltiple.
- Evaluar el modelo mediante MAE, MSE, RMSE y $R^2$.
- Analizar gráficamente los residuos y reconocer las limitaciones del modelo.

---

## Metodología

### Fuente y características de los datos

Se empleó un archivo CSV descargado de AirData de la EPA [2]. El conjunto utilizado contiene únicamente registros del año 2023 y conserva variables procedentes del sistema AQS [3].

| Característica | Descripción |
|---|---|
| Contaminante | Dióxido de azufre (SO₂) |
| Periodo | 01/01/2023–31/12/2023 |
| Registros utilizados | 1774 |
| Variables originales | 28 |
| Estaciones de monitoreo | 5 |
| Unidad | Partes por mil millones (ppb) |
| Variable dependiente | `Daily Max SO2 Concentration` |
| Variables independientes | `Daily Obs Count`, `Site Latitude` y `Elevation (m)` |
| División de datos | 70 % entrenamiento y 30 % prueba |
| Semilla de reproducción | `random_state=123` |

### Revisión de calidad de los datos

Las funciones `info()` y `describe()` se utilizaron para revisar los tipos de datos, la completitud y las estadísticas básicas. En lugar de reproducir las 28 columnas completas, se resumen los hallazgos relevantes para el modelo:

| Verificación | Resultado |
|---|---:|
| Registros totales | 1774 |
| Fechas distintas | 365 |
| Valores faltantes en la concentración de SO₂ | 0 |
| Valores faltantes en `Daily Obs Count` | 0 |
| Valores faltantes en `Site Latitude` | 0 |
| Valores faltantes en `Elevation (m)` | 0 |
| Unidades identificadas | Parts per billion |
| Estaciones identificadas | 5 |

Algunas columnas no utilizadas presentaron valores faltantes, como `CBSA Name`, `Dominant Source`, `Monitor Type`, `Networks` y `QA Primary Monitor?`. Debido a que las cuatro variables empleadas en el modelo estaban completas, no fue necesario aplicar imputación estadística.

### Herramientas

El procesamiento se realizó en Google Colab con Python y las bibliotecas `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` y `statsmodels`. La regresión se implementó mediante `LinearRegression` de `scikit-learn` [4], las métricas se calcularon siguiendo las funciones de evaluación para regresión de la misma biblioteca [5] y el análisis inferencial se complementó con mínimos cuadrados ordinarios de `statsmodels` [6].

### Preparación de los datos

El procedimiento fue el siguiente:

1. Se incorporó el archivo CSV al cuaderno de Google Colab.
2. La variable `Date` se convirtió al formato de fecha.
3. Se seleccionaron exclusivamente los registros de 2023.
4. Las variables del modelo se transformaron a formato numérico.
5. Se verificó la ausencia de valores faltantes en las variables seleccionadas.
6. Se realizaron gráficos exploratorios y una matriz de correlación.
7. Los datos se dividieron en entrenamiento y prueba.
8. Se ajustó el modelo y se evaluaron sus predicciones.
9. Se analizaron los residuos y se realizó un ajuste OLS.

### Variables del modelo

La variable dependiente fue la concentración máxima diaria de SO₂:

$$
y = \text{Daily Max SO2 Concentration}
$$

Las variables independientes fueron:

- $x_1$: número de observaciones diarias (`Daily Obs Count`).
- $x_2$: latitud de la estación (`Site Latitude`).
- $x_3$: elevación de la estación en metros (`Elevation (m)`).

No se incluyó `Daily AQI Value` porque presentó una correlación de **0.998** con la concentración de SO₂ y se deriva de la medición del contaminante. Su uso habría generado una capacidad explicativa artificialmente elevada.

Tampoco se incluyó `Percent Complete`, porque su correlación con `Daily Obs Count` fue prácticamente perfecta. `Site Longitude` fue descartada para reducir la redundancia espacial con `Site Latitude`.

### Modelo de regresión lineal múltiple

La forma general del modelo fue:

$$
\widehat{SO}_2 =
\beta_0 +
\beta_1(\text{Daily Obs Count}) +
\beta_2(\text{Site Latitude}) +
\beta_3(\text{Elevation})
$$

donde:

- $\widehat{SO}_2$ es la concentración máxima diaria estimada.
- $\beta_0$ es el intercepto.
- $\beta_1$, $\beta_2$ y $\beta_3$ son los coeficientes de las variables predictoras.

Los 1774 registros se dividieron aleatoriamente en:

| Conjunto | Registros | Proporción |
|---|---:|---:|
| Entrenamiento | 1241 | 70 % |
| Prueba | 533 | 30 % |

Se utilizó `random_state=123` para que la división de los datos pueda reproducirse.

### Hipótesis estadística

Para evaluar la significancia global del modelo OLS se consideraron las siguientes hipótesis:

$$
H_0: \beta_1=\beta_2=\beta_3=0
$$

$$
H_1: \text{al menos uno de los coeficientes es diferente de cero}
$$

Se utilizó un nivel de significancia de $\alpha=0.05$. Si el valor $p$ del estadístico $F$ es menor que 0.05, se rechaza la hipótesis nula y se concluye que el modelo presenta significancia estadística global.

### Métricas de evaluación

El error absoluto medio se calculó mediante:

$$
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
\left|y_i-\widehat{y}_i\right|
$$

El error cuadrático medio se calculó mediante:

$$
MSE =
\frac{1}{n}
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
$$

La raíz del error cuadrático medio fue:

$$
RMSE =
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
}
$$

El coeficiente de determinación se calculó mediante:

$$
R^2 =
1-
\frac{
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
}{
\sum_{i=1}^{n}
\left(y_i-\overline{y}\right)^2
}
$$

### Evaluación de los supuestos

El ajuste lineal supone una relación aproximadamente lineal entre las variables, independencia de los errores, varianza relativamente constante y residuos aproximadamente normales. La evaluación gráfica de los residuos permite identificar patrones, valores atípicos y desviaciones importantes de estos supuestos [7].

En este estudio se revisaron:

- La distribución de los residuos mediante un histograma y una curva de densidad.
- Los residuos frente a los valores predichos.
- Los residuos frente a cada variable independiente.
- La concentración observada frente a la concentración predicha.

### Reproducibilidad

El análisis completo se encuentra disponible en Google Colab. El cuaderno contiene la preparación de los datos, la exploración estadística, la construcción del modelo, las métricas, las gráficas y el resumen OLS. La semilla `random_state=123` permite reproducir la misma división de entrenamiento y prueba.

<div align="center">

<a href="https://colab.research.google.com/drive/1F7S03kBMQJXqDwyC29e1_V9tsNu30VTL#scrollTo=gIpXJySHvm7w">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir análisis reproducible en Google Colab">
</a>

</div>

---

## Resultados

### Análisis exploratorio

La matriz de relaciones permitió observar la distribución de las variables y la concentración de los datos en determinados valores de latitud y elevación. Esto se debe a que los registros proceden de cinco estaciones fijas.

<div align="center">

<img width="750" alt="Relaciones entre las variables seleccionadas" src="https://github.com/user-attachments/assets/618d87fc-1841-4ff1-9e79-4250a660f5c8" />

**Figura 1. Relaciones entre las variables seleccionadas.**

</div>

### Distribución de la concentración

<div align="center">

<img width="950" alt="Histograma y densidad de la concentración máxima diaria de SO2" src="https://github.com/user-attachments/assets/73c4d9df-a1d0-4f8f-bbe7-1b7d99267b86" />

**Figura 2. Histograma y densidad de la concentración máxima diaria de SO₂.**

</div>

La distribución presentó una marcada asimetría positiva. La mayoría de las observaciones se concentró en valores bajos, pero se identificaron algunos registros elevados que extendieron la cola derecha de la distribución.

| Estadístico | Resultado |
|---|---:|
| Media | 2.894 ppb |
| Mediana | 1.400 ppb |
| Desviación estándar | 6.216 ppb |
| Mínimo registrado | −0.500 ppb |
| Máximo registrado | 72.700 ppb |

La diferencia entre la media y la mediana confirma la influencia de los valores altos sobre el promedio.

### Comparación entre estaciones

<div align="center">

<img width="850" alt="Concentración promedio de SO2 por estación" src="https://github.com/user-attachments/assets/1d72377a-32b9-426f-8f77-f8952dd5c78b" />

**Figura 3. Concentración máxima diaria promedio de SO₂ por estación durante 2023.**

</div>

| Posición | Estación | Registros | Promedio | Máximo |
|---:|---|---:|---:|---:|
| 1 | Lhoist, Montevallo Plant | 363 | 7.413 ppb | 72.700 ppb |
| 2 | North Birmingham | 362 | 2.392 ppb | 17.500 ppb |
| 3 | CHICKASAW | 330 | 1.939 ppb | 25.100 ppb |
| 4 | Ward, Sumter Co. | 356 | 1.630 ppb | 6.400 ppb |
| 5 | Fairfield | 363 | 0.984 ppb | 12.600 ppb |

La estación **Lhoist, Montevallo Plant** presentó el mayor promedio y el máximo más elevado. Esta diferencia sugiere una importante variación espacial entre los puntos de monitoreo.

### Matriz de correlación

<div align="center">

<img width="850" alt="Matriz de correlación" src="https://github.com/user-attachments/assets/88ae069f-bece-4f1f-bea8-bbd88c7db2b8" />

**Figura 4. Matriz de correlación de las variables numéricas.**

</div>

Los principales resultados fueron:

- Concentración de SO₂ y AQI: **0.998**.
- Número de observaciones y porcentaje de completitud: aproximadamente **1.000**.
- Latitud y longitud: **0.805**.
- Concentración de SO₂ y elevación: **−0.217**.
- Concentración de SO₂ y latitud: **0.063**.
- Concentración de SO₂ y número de observaciones: **−0.011**.

La concentración mostró relaciones lineales débiles con las variables finalmente utilizadas. La relación más visible fue una correlación negativa débil con la elevación.

### Relación entre predictores y concentración

<div align="center">

<img width="1000" alt="Variables predictoras frente a la concentración de SO2" src="https://github.com/user-attachments/assets/47598515-4f74-4774-aaeb-bd3c105cf550" />

**Figura 5. Relación entre las variables predictoras y la concentración máxima diaria de SO₂.**

</div>

Los gráficos muestran agrupamientos correspondientes a las características fijas de las estaciones. También muestran valores extremos, especialmente en una de las combinaciones de latitud y elevación.

### Coeficientes del modelo entrenado

El modelo obtenido con el conjunto de entrenamiento fue:

$$
\widehat{SO}_2 =
-65.1690
+0.0798(\text{Daily Obs Count})
+2.1130(\text{Site Latitude})
-0.0341(\text{Elevation})
$$

| Parámetro | Coeficiente |
|---|---:|
| Intercepto | −65.1690 |
| Daily Obs Count | 0.0798 |
| Site Latitude | 2.1130 |
| Elevation (m) | −0.0341 |

Manteniendo constantes las demás variables, el coeficiente de elevación indica una disminución estimada de aproximadamente **0.0341 ppb** por cada metro adicional. Sin embargo, los coeficientes representan asociaciones estadísticas y no demuestran causalidad.

### Evaluación predictiva

| Métrica | Resultado |
|---|---:|
| MAE | 3.0310 ppb |
| MSE | 48.1395 ppb² |
| RMSE | 6.9383 ppb |
| $R^2$ de prueba | 0.1182 |

El MAE indica que las predicciones se alejaron de los valores observados en aproximadamente **3.03 ppb**, en promedio. El RMSE fue mayor debido a que penaliza más los errores grandes.

El valor de $R^2=0.1182$ indica que el modelo explicó aproximadamente el **11.82 %** de la variabilidad del conjunto de prueba. Por ello, su capacidad predictiva fue limitada.

<div align="center">

<img width="650" alt="Concentración observada frente a concentración predicha" src="https://github.com/user-attachments/assets/28353e80-71dc-4860-a944-8549a79069d7" />

**Figura 6. Comparación entre las concentraciones observadas y predichas.**

</div>

La línea roja representa una predicción perfecta. Los valores estimados se concentraron aproximadamente entre 1 y 7 ppb, mientras que algunos valores observados alcanzaron cerca de 70 ppb. Por lo tanto, el modelo subestimó los episodios de mayor concentración.

### Diagnóstico de residuos

El residuo se definió como:

$$
e_i = y_i-\widehat{y}_i
$$

<div align="center">

<img width="950" alt="Distribución de residuos y residuos frente a valores predichos" src="https://github.com/user-attachments/assets/4bdb630a-23b4-409a-8b1f-091451d585bb" />

**Figura 7. Distribución de los residuos y residuos frente a los valores predichos.**

</div>

La distribución de los residuos presentó asimetría positiva y varios errores elevados. Además, la dispersión de los residuos no fue uniforme. Según el enfoque de diagnóstico mediante residuos, la presencia de patrones o cambios en la dispersión puede señalar deficiencias del modelo [7]. En este caso, los resultados indican que los supuestos de normalidad y varianza constante no se cumplen completamente.

### Resultados del modelo OLS

El ajuste OLS realizado con los 1774 registros produjo los siguientes resultados:

| Variable | Coeficiente | Error estándar | Estadístico $t$ | Valor $p$ |
|---|---:|---:|---:|---:|
| Constante | −71.4491 | 6.1117 | −11.690 | < 0.001 |
| Daily Obs Count | 0.1179 | 0.0810 | 1.456 | 0.146 |
| Site Latitude | 2.2922 | 0.1832 | 12.515 | < 0.001 |
| Elevation (m) | −0.0375 | 0.0024 | −15.675 | < 0.001 |

El modelo OLS obtuvo:

| Indicador | Resultado |
|---|---:|
| $R^2$ | 0.1258 |
| $R^2$ ajustado | 0.1243 |
| Estadístico $F$ | 84.87 |
| Valor $p$ del modelo | < 0.001 |

En este ajuste, la latitud y la elevación presentaron valores $p$ menores que 0.05. El número de observaciones diarias no fue estadísticamente significativo al nivel de 5 %.

---

## Discusión

Los resultados muestran que la concentración máxima diaria de SO₂ varió considerablemente entre las estaciones. La estación Lhoist, Montevallo Plant presentó tanto el promedio como el máximo más elevados. Esto indica que la ubicación de la estación constituye un factor relevante para interpretar las mediciones.

Aunque el modelo general fue estadísticamente significativo, su capacidad explicativa fue baja. El $R^2$ de prueba mostró que las tres variables incluidas no representan la mayor parte de la variación diaria del contaminante.

La concentración atmosférica de SO₂ puede depender de factores que no están incluidos en el dataset utilizado, tales como:

- Intensidad y ubicación de fuentes de emisión.
- Velocidad y dirección del viento.
- Temperatura y estabilidad atmosférica.
- Precipitación.
- Hora de ocurrencia de los máximos.
- Cambios operativos de instalaciones industriales.

Asimismo, los residuos elevados muestran que una regresión lineal múltiple no reproduce adecuadamente los episodios extremos. Las variables de latitud y elevación también permanecen constantes para cada estación, por lo que parte del modelo refleja diferencias espaciales entre sitios y no necesariamente variaciones diarias.

Por estas razones, el modelo es útil como ejercicio exploratorio y comparativo, pero no debe emplearse por sí solo para pronosticar episodios elevados ni para determinar el cumplimiento de una norma ambiental. Esta precaución también es coherente con la finalidad de AQS como repositorio para evaluaciones, modelamiento y elaboración de reportes de calidad del aire [3].

### Recomendaciones para futuros análisis

- Incorporar velocidad y dirección del viento, temperatura, humedad y precipitación.
- Añadir información sobre la distancia y actividad de las fuentes de emisión.
- Evaluar una transformación logarítmica de la concentración para reducir la influencia de la asimetría.
- Comparar la regresión lineal con modelos robustos y no lineales.
- Aplicar una validación que respete el orden temporal de los datos.
- Analizar cada estación por separado para distinguir el efecto espacial del comportamiento diario.
- Evaluar los valores extremos antes de decidir si deben conservarse, transformarse o analizarse por separado.

---

## Conclusiones

1. Se analizaron **1774 registros** de cinco estaciones, correspondientes únicamente al año 2023.

2. La concentración promedio general fue **2.894 ppb**, mientras que el máximo registrado fue **72.700 ppb**.

3. Lhoist, Montevallo Plant presentó el mayor promedio, con **7.413 ppb**, y el máximo más elevado del conjunto.

4. La distribución de la concentración presentó una fuerte asimetría positiva debido a la presencia de valores extremos.

5. El modelo de regresión lineal múltiple obtuvo un MAE de **3.0310 ppb**, un RMSE de **6.9383 ppb** y un $R^2$ de prueba de **0.1182**.

6. El modelo explicó solamente una parte reducida de la variabilidad y subestimó las concentraciones más elevadas.

7. En el ajuste OLS, la latitud y la elevación fueron estadísticamente significativas, mientras que el número de observaciones diarias no presentó significancia al nivel de 5 %.

8. Se requieren variables meteorológicas y datos sobre fuentes de emisión para construir un modelo con mayor capacidad explicativa.

### Limitaciones

- El estudio comprende solamente el año 2023.
- Se analizaron cinco estaciones de monitoreo.
- El modelo utiliza únicamente tres variables predictoras.
- No se incluyeron variables meteorológicas ni información directa sobre emisiones.
- La regresión lineal no representa correctamente los episodios extremos.
- Las asociaciones obtenidas no demuestran relaciones causales.

---

## Disponibilidad de datos y código

El procedimiento, el código y las salidas gráficas pueden consultarse en el siguiente cuaderno:

**Google Colab:** https://colab.research.google.com/drive/1F7S03kBMQJXqDwyC29e1_V9tsNu30VTL#scrollTo=gIpXJySHvm7w

El conjunto utilizado corresponde a los datos diarios de SO₂ descargados desde AirData [2]. Para garantizar la reproducibilidad, el cuaderno conserva el filtro exclusivo para 2023 y la semilla utilizada en la división de los datos.

---

## Referencias

[1] U.S. Environmental Protection Agency, “Sulfur Dioxide Basics,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/so2-pollution/sulfur-dioxide-basics. [Accedido: 18-sep-2026].

[2] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data. [Accedido: 18-sep-2026].

[3] U.S. Environmental Protection Agency, “Air Quality System,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/aqs. [Accedido: 18-sep-2026].

[4] Scikit-learn developers, “LinearRegression,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html. [Accedido: 18-sep-2026].

[5] Scikit-learn developers, “Regression metrics,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/model_evaluation.html#regression-metrics. [Accedido: 18-sep-2026].

[6] Statsmodels developers, “Ordinary Least Squares,” *Statsmodels Documentation*. [En línea]. Disponible en: https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLS.html. [Accedido: 18-sep-2026].

[7] National Institute of Standards and Technology, “How can I tell if a model fits my data?,” *NIST/SEMATECH e-Handbook of Statistical Methods*. [En línea]. Disponible en: https://www.itl.nist.gov/div898/handbook/pmd/section4/pmd44.htm. [Accedido: 18-sep-2026].

---

<div align="center">

**Análisis elaborado en Python y Google Colab**

</div>
