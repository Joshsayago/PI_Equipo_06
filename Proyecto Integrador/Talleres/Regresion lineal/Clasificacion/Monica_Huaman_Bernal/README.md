# Análisis de la concentración de monóxido de carbono (CO)

## 1. Introducción

El **monóxido de carbono (CO)** es un contaminante atmosférico asociado principalmente a procesos de combustión. Su presencia en el aire puede representar un riesgo para la salud humana, por lo que el monitoreo de sus concentraciones permite caracterizar la calidad del aire y analizar su comportamiento en diferentes lugares y periodos.

En el presente trabajo se realizó un análisis estadístico de datos de calidad del aire correspondientes al **monóxido de carbono (CO)** en el área metropolitana de **Birmingham-Hoover, Alabama, Estados Unidos**, durante el periodo comprendido entre el **1 de enero de 2022 y el 31 de diciembre de 2023**. El conjunto de datos contiene **1876 observaciones**, provenientes de los sitios de monitoreo *North Birmingham*, *Fairfield* y *Arkadelphia/Near Road*.

El objetivo principal fue analizar la relación entre la **concentración máxima diaria de CO**, utilizada como variable dependiente, y diferentes características disponibles en el conjunto de datos. Para ello, se realizó una exploración inicial de las variables, un análisis de correlación y posteriormente se construyó un **modelo de regresión lineal múltiple**.

La finalidad del análisis fue determinar qué variables podían utilizarse como predictores de la concentración máxima diaria de CO y evaluar el comportamiento estadístico y la capacidad explicativa del modelo obtenido.

---

## 2. Metodología

### 2.1. Descripción y carga de los datos

Los datos utilizados corresponden a registros de calidad del aire para el contaminante **monóxido de carbono (CO)** durante el periodo **2022–2023**, en el área metropolitana de **Birmingham-Hoover, Alabama, Estados Unidos**.

El conjunto de datos contiene **28 variables y 1876 observaciones**. Entre las variables disponibles se encuentran la fecha de medición, identificación del sitio, concentración máxima diaria de CO, valor diario del índice de calidad del aire (AQI), número de observaciones diarias, porcentaje de completitud, coordenadas geográficas, elevación y características relacionadas con las estaciones de monitoreo.

Los datos fueron importados a Python mediante la función `read_csv()` de la biblioteca **Pandas**:

```python
df = pd.read_csv('/content/CO_daily_aqs_data_downloaded_2026-09-17 21_16_44.csv')
