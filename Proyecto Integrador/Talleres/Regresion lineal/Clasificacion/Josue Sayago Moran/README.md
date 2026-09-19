# Análisis de Regresión Múltiple: Dióxido de Nitrógeno (NO2) en Birmingham-Hoover, ALABAMA — (2022-2023)

## 1. Introducción

La contaminación del aire puede analizarse mediante diferentes contaminantes presentes en la atmósfera. Uno de los más críticos es el Dióxido de Nitrógeno (NO₂), un gas altamente reactivo vinculado principalmente a emisiones vehiculares e industriales. La exposición a niveles altos de NO₂ puede irritar las vías respiratorias y agravar enfermedades respiratorias.

Otro indicador estandarizado utilizado para comunicar los riesgos a la salud pública es el Air Quality Index (AQI) o Índice de Calidad del Aire. Este índice representa mediante un valor numérico el nivel de contaminación presente, donde valores mayores indican una calidad del aire más perjudicial.

En este trabajo se utilizó el archivo "NO2_daily_aqs_data_downloaded_2026-09-18 16_44_06_2.csv", el cual contiene información de monitoreo de la calidad del aire correspondiente a los años 2022 y 2023 para el área estadística metropolitana de Birmingham-Hoover, Alabama. 

El objetivo de este trabajo fue aplicar un modelo de regresión lineal múltiple para analizar la relación entre diferentes variables geográficas y de calidad del aire disponibles en el conjunto de datos, para predecir la concentración máxima diaria de NO₂.

Las variables utilizadas como predictoras fueron:
* Daily AQI Value
* Site ID
* Site Latitude
* Site Longitude

La variable que se desea predecir (dependiente) fue:
* Daily Max NO2 Concentration

## 2. Metodología

### Exploración de los datos

Inicialmente, se cargó el conjunto de datos mediante la biblioteca Pandas en Python y se revisaron las dimensiones, columnas, valores nulos y estadísticas descriptivas tras filtrar los años 2022 y 2023.

El dataset analizado contiene:
* 1,317 registros
* 28 columnas
* 2 estaciones de monitoreo
* 0 valores nulos (en las variables de interés)
* 0 filas duplicadas

Las estaciones de monitoreo presentes fueron:
* North Birmingham
* Arkadelphia/Near Road

La variable objetivo, Daily Max NO2 Concentration, presentó los siguientes valores (en partes por billón - ppb):

| Estadístico | PM2.5 (NO₂) |
| :--- | :--- |
| Registros | 1317 |
| Media | 19.92 |
| Desviación estándar | 8.99 |
| Mínimo | 1.90 |
| Primer cuartil | 12.80 |
| Mediana | 18.90 |
| Tercer cuartil | 26.30 |
| Máximo | 50.30 |

Por otro lado, la variable predictora Daily AQI Value presentó una media de 18.34, con un valor mínimo de 1 y un valor máximo de 47.

### Variables 

* **Daily Max NO2 Concentration (Dependiente):** Concentración máxima diaria reportada de dióxido de nitrógeno.
* **Daily AQI Value (Independiente):** Índice diario de calidad del aire.
* **Site ID (Independiente):** Identificador numérico único de la estación de monitoreo.
* **Site Latitude (Independiente):** Ubicación geográfica (latitud) de la estación.
* **Site Longitude (Independiente):** Ubicación geográfica (longitud) de la estación.


### Análisis Exploratorio
Como paso metodológico previo al modelado, se calculó una matriz de correlación de Pearson y se generó una matriz de dispersión múltiple (Pairplot) utilizando la librería Seaborn. Este procedimiento tuvo como fin identificar gráficamente la relación matemática entre las variables seleccionadas y comprobar sus distribuciones.
Para construir y validar el modelo predictivo, los datos fueron divididos aleatoriamente mediante la función train_test_split(. Se utilizó la siguiente proporción:
* 70 % de los datos para entrenamiento (921 registros).
* 30 % de los datos para prueba (396 registros).
* random_state = 123.
Esta separación es una práctica estándar que permite entrenar al algoritmo con un fragmento histórico y evaluar objetivamente su capacidad de predicción frente a datos desconocidos.

Asimismo,se utilizó la clase LinearRegression() proveniente de la biblioteca Scikit-learn. Tras concluir la fase de entrenamiento con los 921 registros, se obtuvieron los siguientes coeficientes para la ecuación de regresión múltiple:

| Variable Predictora | Coeficiente |
| :--- | :--- |
| Daily AQI Value | 1.055002 |
| Site ID | -0.000010 |
| Site Latitude | 0.000000 |
| Site Longitude | 0.000000 |

El intercepto obtenido de la regresión fue aproximadamente: **104.6756**

El coeficiente principal correspondiente a Daily AQI Value es fuertemente positivo (1.055). Esto indica que, manteniendo constantes los factores geográficos, un incremento de una unidad en el Índice de Calidad del Aire se relaciona matemáticamente con un incremento aproximado de 1.055 ppb en la concentración máxima de NO₂ estimada. Los coeficientes de latitud y longitud tienden a cero debido a la cercanía geográfica de las únicas dos estaciones analizadas en la región.
## Resultados

El análisis de los datos extraídos arrojó resultados estadísticos contundentes que validan la relación directa entre las mediciones del contaminante y el índice reportado. A continuación, se detalla la interpretación de los gráficos y métricas generadas:

**1. Análisis de Correlación**
<p align = center>
<img width="956" height="874" alt="image" src="https://github.com/user-attachments/assets/21c8b11e-b0d8-4402-8caf-1024a299c8ac" />
  <p align = center>
  <img width="1231" height="1231" alt="image" src="https://github.com/user-attachments/assets/eede9071-900d-4b06-943d-cd181454dfa4" />
</p>

El mapa de calor de correlación permitió filtrar el ruido del conjunto de datos y enfocarse en las variables cuantitativas más relevantes. Se observa una correlación positiva casi perfecta entre la Daily Max NO2 Concentration y el Daily AQI Value. Otras variables, como el conteo de observaciones (Daily Obs Count) o la elevación del sitio (Elevation (m)), mostraron coeficientes de correlación cercanos a cero frente al AQI, confirmando que no influyen en el cálculo de este índice. 
Por otro lado, en la matriz de dispersión (Pairplot), los histogramas revelaron la naturaleza discreta de las variables espaciales (Site ID, Latitud, Longitud), confirmando visualmente la existencia de solo dos estaciones fijas. Los diagramas de dispersión del AQI versus el NO₂ mostraron una línea recta ascendente perfecta, evidenciando una dependencia total.



**2. Relación de Variables Múltiples contra el AQI**
<p align = center>
<img width="1788" height="990" alt="image" src="https://github.com/user-attachments/assets/9aceb607-b301-4c2f-9785-a6a1295a7e05" />
</p>

Para corroborar visualmente los hallazgos del mapa de calor, se graficaron cuatro variables independientes contra el AQI real. Como se evidencia en la primera subtrama, los puntos de la concentración de NO₂ forman una línea recta ascendente muy clara. Por el contrario, las otras tres variables (observaciones, porcentaje completo y elevación) muestran nubes de puntos horizontales y dispersas, lo que reafirma la decisión de construir el modelo predictivo exclusivamente basándonos en la concentración de NO₂.

**3. Desempeño del Modelo Predictivo**
Al entrenar el modelo de Regresión Lineal Simple con el 70% de los datos y validarlo con el 30% restante, se obtuvieron las siguientes métricas:
* **Coeficiente de determinación (R²):** 0.9979
* **Coeficiente (Pendiente):** 0.9437
* **Intercepción:** -0.4592
<p align = center>
<img width="790" height="590" alt="image" src="https://github.com/user-attachments/assets/495db06d-bb69-4821-ae88-27f29dd31b96" />
</p>

El valor de R² indica que el modelo logra explicar el 99.79% de la varianza en los datos. Visualmente, esto se confirma en el gráfico de valores reales versus predichos, donde las predicciones del modelo (puntos morados) se alinean de manera casi milimétrica sobre la "Meta ideal" (línea roja de 45°). Esto demuestra que el margen de error de predicción es mínimo en todas las escalas evaluadas.

**4. Diagnóstico y Validación Estadística de los Errores (Residuos)**
Para garantizar que el modelo matemático sea robusto y no producto de la casualidad, se analizaron sus residuos (la diferencia entre el valor real y la predicción) a través de dos pruebas visuales:
<p align = center>
<img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/94ddd0ea-bbe9-451f-975c-def2f94ef114" />
</p>

**Normalidad de los errores:** El histograma de densidad de kernel muestra una distribución normal perfecta (forma de campana de Gauss) centrada exactamente en el valor 0. Esto significa que la inmensa mayoría de las predicciones del modelo fueron exactas o tuvieron errores minúsculos, validando matemáticamente la confiabilidad de la regresión.
<p align = center>
<img width="874" height="594" alt="image" src="https://github.com/user-attachments/assets/a5ae43d3-f90f-4bde-bb64-a5a71959c6c8" />
</p>

**Homocedasticidad:** El gráfico de dispersión de los residuos frente a los valores predichos exhibe una distribución completamente aleatoria alrededor de la línea horizontal de error cero (Y=0). Al no observarse patrones en forma de cono, embudo o curvas, se confirma que la varianza de los errores es constante en todo el espectro de datos, cumpliendo así con las asunciones teóricas de la regresión lineal.

---

## Discusión

El modelo de regresión lineal aplicado demostró una eficacia predictiva excepcional (R² = 0.9979) al evaluar el impacto de la concentración diaria de NO₂ sobre el AQI. Desde una perspectiva técnica, este nivel de precisión casi absoluto es un resultado esperado y lógico. El Índice de Calidad del Aire (AQI) no es una variable aleatoria o empírica, sino un indicador estandarizado que las agencias gubernamentales calculan matemáticamente a partir de las concentraciones de los contaminantes. En la práctica, nuestro modelo de *machine learning* ha logrado "hacer ingeniería inversa" a la fórmula exacta que utiliza la EPA para asignar el índice de riesgo basado en el NO₂.

Además, las pruebas de diagnóstico de residuos (normalidad y homocedasticidad) superaron todos los criterios estadísticos, lo que descarta cualquier sesgo algorítmico en las predicciones. Este análisis demuestra cómo herramientas computacionales simples, pero bien calibradas, pueden mapear relaciones exactas en bases de datos ambientales masivas, permitiendo predecir alertas de salud pública (como el AQI) de manera instantánea a partir de las lecturas directas de los sensores de calidad del aire.

---

## 5. Referencias

[1] U.S. Environmental Protection Agency, "Air Quality System (AQS) Data Dictionary," EPA, Washington, D.C., 2023. [Online]. Available: https://www.epa.gov/aqs
[2] U.S. Environmental Protection Agency, "AirData," EPA, Washington, D.C., 2026. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data
[3] F. Pedregosa *et al.*, "Scikit-learn: Machine Learning in Python," *J. Mach. Learn. Res.*, vol. 12, pp. 2825–2830, 2011.
