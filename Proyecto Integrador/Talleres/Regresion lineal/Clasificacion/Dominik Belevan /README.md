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

## Índice

1. [Introducción](#introducción)
2. [Metodología](#metodología)
3. [Resultados](#resultados)
4. [Discusión](#discusión)
5. [Conclusiones](#conclusiones)
6. [Referencias](#referencias)

---

## Introducción

El dióxido de azufre (SO₂) es un contaminante atmosférico gaseoso generado principalmente por la combustión de materiales que contienen azufre y por determinados procesos industriales. Su monitoreo permite estudiar la calidad del aire e identificar variaciones entre diferentes estaciones de medición.

En este trabajo se analizaron los registros de concentración máxima diaria de SO₂ correspondientes exclusivamente al año **2023**. Los datos fueron obtenidos de la plataforma AirData de la Agencia de Protección Ambiental de los Estados Unidos (EPA) y contienen información procedente de cinco estaciones de monitoreo.

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

Se empleó un archivo CSV descargado de AirData de la EPA. El conjunto utilizado contiene únicamente registros del año 2023.

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

### Herramientas utilizadas

El procesamiento se realizó en Google Colab mediante Python y las siguientes bibliotecas:

- `pandas`: organización y procesamiento de los datos.
- `numpy`: operaciones numéricas.
- `matplotlib`: elaboración de gráficos.
- `seaborn`: visualización estadística.
- `scikit-learn`: construcción y evaluación de la regresión.
- `statsmodels`: análisis mediante mínimos cuadrados ordinarios.

### Preparación de los datos

El procedimiento aplicado fue el siguiente:

1. Se incorporó el archivo CSV al cuaderno de Google Colab.
2. La variable `Date` se convirtió al formato de fecha.
3. Se seleccionaron exclusivamente los registros de 2023.
4. Las variables del modelo se transformaron a formato numérico.
5. Se verificó la ausencia de valores faltantes en las variables seleccionadas.
6. Se realizaron gráficos exploratorios y una matriz de correlación.
7. Los datos se dividieron en entrenamiento y prueba.
8. Se ajustó el modelo de regresión lineal múltiple.
9. Se calcularon las métricas de evaluación.
10. Se analizaron los residuos y se realizó un ajuste OLS.

### Variables del modelo

La variable dependiente fue la concentración máxima diaria de SO₂:

$$
y = \text{Daily Max SO2 Concentration}
$$

Las variables independientes fueron:

- $x_1$: número de observaciones diarias (`Daily Obs Count`).
- $x_2$: latitud de la estación (`Site Latitude`).
- $x_3$: elevación de la estación en metros (`Elevation (m)`).

No se incluyó `Daily AQI Value` porque presentó una correlación de **0.998** con la concentración de SO₂ y se deriva de la medición del contaminante. Su uso podría producir una capacidad explicativa artificialmente elevada.

Tampoco se incluyó `Percent Complete`, porque su correlación con `Daily Obs Count` fue prácticamente perfecta. `Site Longitude` fue descartada para reducir la redundancia espacial con `Site Latitude`.

### Modelo de regresión lineal múltiple

La forma general del modelo empleado fue:

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

Se empleó `random_state=123` para obtener resultados reproducibles.

### Métricas de evaluación

#### Error absoluto medio

El MAE representa el promedio de los errores absolutos:

$$
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
\left|y_i-\widehat{y}_i\right|
$$

#### Error cuadrático medio

El MSE representa el promedio de los errores elevados al cuadrado:

$$
MSE =
\frac{1}{n}
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
$$

#### Raíz del error cuadrático medio

El RMSE expresa el error en las mismas unidades que la concentración:

$$
RMSE =
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
}
$$

#### Coeficiente de determinación

El coeficiente de determinación representa la proporción de la variabilidad explicada por el modelo:

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

La estación **Lhoist, Montevallo Plant** presentó el mayor promedio y el máximo más elevado. Esta diferencia evidencia una importante variación espacial entre los puntos de monitoreo.

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

Manteniendo constantes las demás variables, el coeficiente de elevación indica una disminución estimada de aproximadamente **0.0341 ppb** por cada metro adicional. Sin embargo, estos coeficientes representan asociaciones estadísticas y no demuestran causalidad.

### Evaluación predictiva

| Métrica | Resultado |
|---|---:|
| MAE | 3.0310 ppb |
| MSE | 48.1395 ppb² |
| RMSE | 6.9383 ppb |
| $R^2$ de prueba | 0.1182 |

El MAE indica que las predicciones se alejaron de los valores observados en aproximadamente **3.03 ppb**, en promedio. El RMSE fue mayor debido a que penaliza con mayor intensidad los errores grandes.

El valor de $R^2=0.1182$ indica que el modelo explicó aproximadamente el **11.82 %** de la variabilidad del conjunto de prueba. Por lo tanto, su capacidad predictiva fue limitada.

<div align="center">

<img width="650" alt="Concentración observada frente a concentración predicha" src="https://github.com/user-attachments/assets/28353e80-71dc-4860-a944-8549a79069d7" />

**Figura 6. Comparación entre las concentraciones observadas y predichas.**

</div>

La línea roja representa una predicción perfecta. Los valores estimados se concentraron aproximadamente entre 1 y 7 ppb, mientras que algunos valores observados alcanzaron cerca de 70 ppb. Por lo tanto, el modelo subestimó los episodios de mayor concentración.

### Diagnóstico de residuos

El residuo de cada observación se definió como:

$$
e_i = y_i-\widehat{y}_i
$$

<div align="center">

<img width="950" alt="Distribución de residuos y residuos frente a valores predichos" src="https://github.com/user-attachments/assets/4bdb630a-23b4-409a-8b1f-091451d585bb" />

**Figura 7. Distribución de los residuos y residuos frente a los valores predichos.**

</div>

La distribución de los residuos presentó asimetría positiva y varios errores elevados. Además, la dispersión de los residuos no fue uniforme. Esto indica que los supuestos de normalidad y varianza constante no se cumplen completamente.

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

La concentración atmosférica de SO₂ puede depender de factores que no están incluidos en el conjunto de datos utilizado, tales como:

- Intensidad y ubicación de las fuentes de emisión.
- Velocidad y dirección del viento.
- Temperatura y estabilidad atmosférica.
- Precipitación.
- Hora de ocurrencia de las concentraciones máximas.
- Cambios operativos de las instalaciones industriales.

Asimismo, los residuos elevados muestran que la regresión lineal múltiple no reproduce adecuadamente los episodios extremos. Las variables de latitud y elevación permanecen constantes para cada estación, por lo que parte del modelo refleja diferencias espaciales entre sitios y no necesariamente variaciones diarias.

Por estas razones, el modelo es útil como ejercicio exploratorio y comparativo, pero no debe emplearse por sí solo para pronosticar episodios elevados ni para determinar el cumplimiento de una norma ambiental.

---

## Conclusiones

1. Se analizaron **1774 registros** procedentes de cinco estaciones y correspondientes exclusivamente al año 2023.

2. La concentración promedio general fue **2.894 ppb**, mientras que el máximo registrado fue **72.700 ppb**.

3. Lhoist, Montevallo Plant presentó el mayor promedio, con **7.413 ppb**, y el máximo más elevado del conjunto.

4. La distribución de la concentración presentó una fuerte asimetría positiva debido a la presencia de valores extremos.

5. El modelo de regresión lineal múltiple obtuvo un MAE de **3.0310 ppb**, un RMSE de **6.9383 ppb** y un $R^2$ de prueba de **0.1182**.

6. El modelo explicó solamente una parte reducida de la variabilidad y subestimó las concentraciones más elevadas.

7. En el ajuste OLS, la latitud y la elevación fueron estadísticamente significativas, mientras que el número de observaciones diarias no presentó significancia al nivel de 5 %.

8. Se requieren variables meteorológicas y datos sobre las fuentes de emisión para construir un modelo con mayor capacidad explicativa.

### Limitaciones

- El estudio comprende solamente el año 2023.
- Se analizaron cinco estaciones de monitoreo.
- El modelo utiliza únicamente tres variables predictoras.
- No se incluyeron variables meteorológicas ni información directa sobre emisiones.
- La regresión lineal no representa correctamente los episodios extremos.
- Las asociaciones obtenidas no demuestran relaciones causales.

---

## Referencias

[1] U.S. Environmental Protection Agency, “Sulfur Dioxide Basics,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/so2-pollution/sulfur-dioxide-basics. [Accedido: 18-sep-2026].

[2] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data. [Accedido: 18-sep-2026].

[3] U.S. Environmental Protection Agency, “Air Quality System,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/aqs. [Accedido: 18-sep-2026].

[4] Scikit-learn developers, “LinearRegression,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html. [Accedido: 18-sep-2026].

[5] Scikit-learn developers, “Regression metrics,” *Scikit-learn Documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/model_evaluation.html#regression-metrics. [Accedido: 18-sep-2026].

[6] Statsmodels developers, “Ordinary Least Squares,” *Statsmodels Documentation*. [En línea]. Disponible en: https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLS.html. [Accedido: 18-sep-2026].

---

<div align="center">

**Análisis elaborado en Python y Google Colab**

[**Abrir cuaderno completo en Google Colab**](https://colab.research.google.com/drive/1F7S03kBMQJXqDwyC29e1_V9tsNu30VTL#scrollTo=gIpXJySHvm7w)

</div>
