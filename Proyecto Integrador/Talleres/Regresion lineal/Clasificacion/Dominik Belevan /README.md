<div align="center">

# Análisis y regresión lineal de la concentración de SO₂ durante 2023

### Análisis de la concentración máxima diaria registrada por estaciones de monitoreo

**Autora:** Bertha Dominik Belevan Amaro  
**Curso:** Proyecto Integrador  
**Año de análisis:** 2023  

<br>

<a href="https://colab.research.google.com/drive/1WSb4f0r2F-1EuT-o_7wPmXYGSETjca-I#scrollTo=_AYrzcN9PRBN">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir análisis en Google Colab">
</a>

</div>

---

## Índice

1. [Introducción](#introducción)
2. [Objetivos](#objetivos)
3. [Metodología](#metodología)
4. [Resultados](#resultados)
5. [Discusión](#discusión)
6. [Conclusiones](#conclusiones)
7. [Limitaciones](#limitaciones)
8. [Código empleado](#código-empleado)
9. [Referencias](#referencias)

---

## Introducción

El dióxido de azufre (SO₂) es un contaminante atmosférico gaseoso producido principalmente por la combustión de materiales que contienen azufre y por determinados procesos industriales. Su presencia en el aire puede afectar la salud respiratoria de la población y contribuir a distintos problemas ambientales.

En este trabajo se analizaron los registros de concentración máxima diaria de SO₂ correspondientes exclusivamente al año **2023**. Los datos proceden del sistema **Air Quality System (AQS)** de la Agencia de Protección Ambiental de los Estados Unidos (EPA).

El análisis comprende la revisión y limpieza de los datos, la comparación entre estaciones, la evaluación de la variación mensual y diaria, y la aplicación de un modelo de regresión lineal. El propósito del modelo es determinar si existe una tendencia temporal general en las concentraciones registradas durante 2023.

---

## Objetivos

### Objetivo general

Analizar el comportamiento temporal de la concentración máxima diaria de dióxido de azufre registrada durante el año 2023 mediante técnicas estadísticas, gráficas y un modelo de regresión lineal.

### Objetivos específicos

- Preparar y filtrar los registros correspondientes exclusivamente al año 2023.
- Identificar las estaciones con mayores concentraciones promedio de SO₂.
- Analizar la variación diaria y mensual de las concentraciones.
- Ajustar un modelo de regresión lineal para estimar la tendencia temporal.
- Evaluar el desempeño del modelo mediante las métricas MAE, RMSE y $R^2$.
- Interpretar los resultados y reconocer las principales limitaciones del modelo.

---

## Metodología

### Fuente de los datos

Se utilizó un archivo en formato CSV descargado de la plataforma AirData de la EPA. El conjunto de datos contiene mediciones diarias de SO₂ registradas por distintas estaciones de monitoreo.

Para este análisis se trabajó solamente con los registros comprendidos entre el **1 de enero y el 31 de diciembre de 2023**.

### Resumen del conjunto de datos

| Característica | Resultado |
|---|---:|
| Periodo analizado | 01/01/2023 – 31/12/2023 |
| Número de registros | 1774 |
| Número de columnas | 28 |
| Estaciones identificadas | 5 |
| Unidad de concentración | ppb |
| Variable principal | Concentración máxima diaria de SO₂ |

> **Nota:** ppb significa partes por mil millones.

### Herramientas utilizadas

El procesamiento y análisis se realizó en Google Colab mediante Python y las siguientes bibliotecas:

- `pandas`: lectura, organización y transformación de datos.
- `numpy`: operaciones numéricas.
- `matplotlib`: elaboración de gráficos.
- `seaborn`: diseño y presentación visual.
- `scikit-learn`: división de los datos, regresión lineal y métricas de evaluación.

### Preparación de los datos

El procedimiento de preparación incluyó:

1. Carga del archivo CSV.
2. Conversión de la columna de fecha al formato `datetime`.
3. Filtrado de los registros correspondientes únicamente a 2023.
4. Conversión de la concentración de SO₂ a formato numérico.
5. Eliminación de registros sin fecha, estación o concentración.
6. Agrupación de las observaciones por fecha, estación y mes.
7. Creación de una variable temporal numérica para la regresión.

### Variable analizada

La variable principal fue:

`Daily Max SO2 Concentration`

Esta variable representa la concentración máxima diaria de dióxido de azufre registrada por cada estación y se expresa en **ppb**.

### Promedio diario entre estaciones

Debido a que podían existir mediciones de diferentes estaciones para una misma fecha, se calculó la concentración máxima diaria promedio entre las estaciones disponibles:

$$
\overline{SO}_{2,t} =
\frac{1}{n_t}
\sum_{i=1}^{n_t} SO_{2,i,t}
$$

donde:

- $SO_{2,i,t}$ es la concentración máxima diaria registrada en la estación $i$ durante el día $t$.
- $n_t$ es el número de estaciones disponibles durante el día $t$.
- $\overline{SO}_{2,t}$ es la concentración máxima diaria promedio entre estaciones.

Este promedio facilita el análisis general, pero **no constituye por sí solo una métrica regulatoria de cumplimiento**.

### Regresión lineal

Para evaluar la tendencia temporal se empleó el siguiente modelo:

$$
\widehat{SO}_2 = \beta_0 + \beta_1t
$$

donde:

- $\widehat{SO}_2$ es la concentración estimada de dióxido de azufre.
- $\beta_0$ es el intercepto del modelo.
- $\beta_1$ representa el cambio promedio estimado por día.
- $t$ es el número de días transcurridos desde el 1 de enero de 2023.

Para evaluar la capacidad predictiva, los datos se dividieron en:

- **80 % para entrenamiento.**
- **20 % para prueba.**

Se utilizó `random_state=42` para obtener resultados reproducibles.

### Métricas de evaluación

#### Error absoluto medio

El MAE representa el error promedio absoluto entre los valores observados y estimados:

$$
MAE =
\frac{1}{n}
\sum_{i=1}^{n}
\left|y_i-\widehat{y}_i\right|
$$

#### Raíz del error cuadrático medio

El RMSE penaliza con mayor intensidad los errores grandes:

$$
RMSE =
\sqrt{
\frac{1}{n}
\sum_{i=1}^{n}
\left(y_i-\widehat{y}_i\right)^2
}
$$

#### Coeficiente de determinación

El coeficiente de determinación indica qué proporción de la variabilidad de los datos es explicada por el modelo:

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

Un valor de $R^2$ cercano a 1 indica que el modelo explica gran parte de la variabilidad. Un valor cercano a 0 indica una capacidad explicativa limitada.

---

## Resultados

### Estadísticas generales

| Indicador | Resultado |
|---|---:|
| Promedio diario general | 2.863 ppb |
| Máximo promedio diario | 17.160 ppb |
| Intercepto del modelo | 1.9161 ppb |
| Pendiente temporal | 0.005204 ppb/día |
| $R^2$ descriptivo | 0.0389 |
| MAE de prueba | 1.8704 ppb |
| RMSE de prueba | 2.5619 ppb |
| $R^2$ de prueba | 0.0784 |

### Concentración promedio por estación

La estación **Lhoist, Montevallo Plant** presentó el promedio más elevado, con aproximadamente **7.413 ppb**. Las demás estaciones mostraron concentraciones promedio considerablemente menores.

| Posición | Estación | Promedio de SO₂ |
|---:|---|---:|
| 1 | Lhoist, Montevallo Plant | 7.413 ppb |
| 2 | North Birmingham | 2.392 ppb |
| 3 | CHICKASAW | 1.939 ppb |
| 4 | Ward, Sumter Co. | 1.630 ppb |
| 5 | Fairfield | 0.984 ppb |

<p align="center">
  <img src="https://github.com/user-attachments/assets/b47a3349-8465-41a0-a53b-bbb160c86974" width="850" alt="Concentración promedio de SO2 por estación">
</p>

**Interpretación:** la diferencia observada entre estaciones demuestra que la ubicación del punto de monitoreo influye considerablemente en los niveles registrados. Estas diferencias podrían estar relacionadas con la cercanía a fuentes de emisión, condiciones meteorológicas, actividad industrial o características locales.

### Evolución diaria de la concentración

<p align="center">
  <img src="https://github.com/user-attachments/assets/b556f8eb-a135-4a5d-8a1f-45346aed03d6" width="950" alt="Evolución diaria de la concentración promedio de SO2">
</p>

La serie temporal presenta una concentración generalmente baja, pero con diferentes picos durante el año. El máximo promedio diario fue aproximadamente **17.160 ppb**.

Los picos demuestran que la concentración no aumentó de forma constante. En su lugar, se produjeron incrementos puntuales que podrían estar relacionados con emisiones locales o variaciones en las condiciones atmosféricas.

### Concentración promedio mensual

<p align="center">
  <img src="https://github.com/user-attachments/assets/33cf1170-7eb6-4cd8-a638-b7d23385aa12" width="850" alt="Concentración mensual promedio de SO2">
</p>

El mes con mayor concentración promedio fue **septiembre**, con aproximadamente **4.873 ppb**, seguido de **noviembre**, con aproximadamente **4.071 ppb**.

| Mes destacado | Promedio aproximado |
|---|---:|
| Septiembre | 4.873 ppb |
| Noviembre | 4.071 ppb |

Este comportamiento muestra que existió variabilidad mensual durante 2023. Sin embargo, con la información disponible no es posible atribuir directamente estos aumentos a una causa específica.

### Tendencia mediante regresión lineal

El modelo ajustado con todos los promedios diarios fue:

$$
\widehat{SO}_2 = 1.9161 + 0.005204t
$$

<p align="center">
  <img src="https://github.com/user-attachments/assets/985f590e-a91b-4ffb-b2bc-cd61b4f504dd" width="950" alt="Regresión lineal de la concentración diaria promedio de SO2">
</p>

La pendiente positiva de **0.005204 ppb por día** indica una ligera tendencia ascendente durante 2023. Sin embargo, el coeficiente de determinación descriptivo fue:

$$
R^2 = 0.0389
$$

Por lo tanto, la variable temporal explica únicamente alrededor del **3.89 %** de la variabilidad observada. Esto indica que, aunque la recta presenta una pendiente positiva, la tendencia es débil.

> Una pendiente positiva no significa necesariamente que exista un incremento ambiental constante o estadísticamente significativo.

### Valores observados y estimados

<p align="center">
  <img src="https://github.com/user-attachments/assets/228d215a-9a50-489b-a781-fd07c7a98d40" width="650" alt="Comparación entre valores observados y estimados">
</p>

La línea roja representa la situación ideal en la que el valor estimado es exactamente igual al observado.

Los puntos alejados de esta línea indican errores de estimación. El modelo concentra la mayoría de sus predicciones en valores intermedios y no reproduce correctamente varios de los picos de concentración.

### Evaluación del modelo

| Métrica | Resultado | Interpretación |
|---|---:|---|
| MAE | 1.8704 ppb | Error absoluto promedio del modelo |
| RMSE | 2.5619 ppb | Evidencia errores mayores en algunos registros |
| $R^2$ de prueba | 0.0784 | Capacidad explicativa limitada |

El RMSE fue mayor que el MAE debido a que esta métrica penaliza más los errores grandes. Esto concuerda con la presencia de días con concentraciones elevadas que no fueron reproducidas adecuadamente por la regresión.

---

## Discusión

Los resultados indican que las concentraciones máximas diarias de SO₂ presentaron una alta variabilidad durante 2023. Además, se identificaron diferencias notables entre estaciones, especialmente en **Lhoist, Montevallo Plant**, cuyo promedio fue superior al de los demás puntos de monitoreo.

La regresión lineal presentó una pendiente positiva, pero su bajo coeficiente de determinación indica que el paso del tiempo no explica adecuadamente las variaciones observadas. Esto ocurre porque las concentraciones atmosféricas pueden depender de numerosos factores adicionales, como:

- Velocidad y dirección del viento.
- Temperatura ambiental.
- Precipitación.
- Estabilidad atmosférica.
- Ubicación de las estaciones.
- Distancia respecto de fuentes industriales.
- Cambios en la intensidad de las emisiones.
- Disponibilidad diaria de datos por estación.

Asimismo, el gráfico de valores observados y estimados muestra que el modelo tiene dificultades para representar los episodios de concentración elevada. Una regresión lineal simple permite resumir la tendencia general, pero no describe completamente el comportamiento irregular de la contaminación atmosférica.

Los resultados deben interpretarse como un análisis exploratorio de los registros disponibles y no como una evaluación directa del cumplimiento de una norma de calidad del aire.

---

## Conclusiones

1. El conjunto analizado contiene **1774 registros**, **28 columnas** y datos de **5 estaciones** correspondientes exclusivamente a 2023.

2. La concentración máxima diaria promedio general fue aproximadamente **2.863 ppb**, mientras que el máximo promedio diario fue **17.160 ppb**.

3. La estación **Lhoist, Montevallo Plant** presentó el mayor promedio, con aproximadamente **7.413 ppb**.

4. **Septiembre** fue el mes con mayor concentración promedio, seguido por noviembre.

5. La regresión lineal mostró una pendiente positiva de **0.005204 ppb por día**, lo que representa una ligera tendencia ascendente.

6. El valor descriptivo de $R^2=0.0389$ demuestra que el tiempo explica solo una pequeña proporción de la variabilidad observada.

7. En el conjunto de prueba se obtuvo un MAE de **1.8704 ppb**, un RMSE de **2.5619 ppb** y un $R^2$ de **0.0784**.

8. La regresión lineal simple es útil para visualizar una tendencia general, pero no es suficiente para explicar los cambios diarios ni los picos de concentración de SO₂.

---

## Limitaciones

- El análisis considera únicamente información del año 2023.
- Se utilizó una sola variable predictora: el tiempo.
- No se incorporaron variables meteorológicas ni datos directos sobre fuentes de emisión.
- La cantidad de mediciones disponibles puede variar entre estaciones y fechas.
- Los promedios diarios entre estaciones pueden ocultar diferencias espaciales importantes.
- Los valores elevados pueden influir considerablemente en el ajuste del modelo.
- El análisis no demuestra causalidad entre el tiempo y las concentraciones de SO₂.

Como continuación del estudio, podrían incorporarse variables meteorológicas, modelos no lineales y métodos específicos para series temporales.

---

## Código empleado

El análisis completo también se encuentra disponible en Google Colab:

<a href="https://colab.research.google.com/drive/1WSb4f0r2F-1EuT-o_7wPmXYGSETjca-I#scrollTo=_AYrzcN9PRBN">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Abrir análisis en Google Colab">
</a>

<details>
<summary><b>Ver código completo en Python</b></summary>

```python
# ============================================================
# ANÁLISIS Y REGRESIÓN LINEAL DE SO2 — AÑO 2023
# ============================================================

# 1. Importación de bibliotecas

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from google.colab import files
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error
from sklearn.metrics import mean_squared_error
from sklearn.metrics import r2_score

sns.set_theme(style="whitegrid")


# 2. Subir el archivo CSV

uploaded = files.upload()

nombre_archivo = next(iter(uploaded))

df = pd.read_csv(nombre_archivo)

print("Archivo cargado:", nombre_archivo)
print("Dimensiones originales:", df.shape)

display(df.head())


# 3. Revisión de las columnas

print("Columnas disponibles:")

for columna in df.columns:
    print("-", columna)


# 4. Preparación de los datos

df["Date"] = pd.to_datetime(
    df["Date"],
    errors="coerce"
)

df["Daily Max SO2 Concentration"] = pd.to_numeric(
    df["Daily Max SO2 Concentration"],
    errors="coerce"
)

df_2023 = df[
    (df["Date"].dt.year == 2023)
].copy()

df_2023 = df_2023.dropna(
    subset=[
        "Date",
        "Site Name",
        "Daily Max SO2 Concentration"
    ]
)

print("Número de registros de 2023:", len(df_2023))
print("Número de columnas:", len(df_2023.columns))
print("Número de estaciones:", df_2023["Site Name"].nunique())
print("Fecha inicial:", df_2023["Date"].min())
print("Fecha final:", df_2023["Date"].max())
print("Unidades:", df_2023["Units"].dropna().unique())


# 5. Estadísticas descriptivas

estadisticas = df_2023[
    "Daily Max SO2 Concentration"
].describe()

display(estadisticas)


# 6. Concentración promedio por estación

promedio_estacion = (
    df_2023
    .groupby("Site Name")["Daily Max SO2 Concentration"]
    .mean()
    .sort_values(ascending=False)
)

display(promedio_estacion)

plt.figure(figsize=(11, 5))

sns.barplot(
    x=promedio_estacion.values,
    y=promedio_estacion.index,
    color="#4C78A8"
)

plt.title(
    "Concentración máxima diaria media de SO₂ por estación, 2023"
)

plt.xlabel("SO₂ (ppb)")
plt.ylabel("Estación")
plt.tight_layout()
plt.show()


# 7. Promedio diario entre estaciones

promedio_diario = (
    df_2023
    .groupby("Date", as_index=False)[
        "Daily Max SO2 Concentration"
    ]
    .mean()
)

promedio_diario = promedio_diario.sort_values("Date")

promedio_diario = promedio_diario.rename(
    columns={
        "Daily Max SO2 Concentration": "SO2_promedio"
    }
)

print(
    "Promedio diario general:",
    promedio_diario["SO2_promedio"].mean()
)

print(
    "Máximo promedio diario:",
    promedio_diario["SO2_promedio"].max()
)


# 8. Serie temporal diaria

plt.figure(figsize=(12, 5))

plt.plot(
    promedio_diario["Date"],
    promedio_diario["SO2_promedio"],
    color="#3B73B9",
    linewidth=1.3
)

plt.title(
    "Evolución de la concentración máxima diaria promedio de SO₂, 2023"
)

plt.xlabel("Fecha")
plt.ylabel("SO₂ promedio entre estaciones (ppb)")
plt.tight_layout()
plt.show()


# 9. Promedio mensual

promedio_diario["Mes"] = (
    promedio_diario["Date"]
    .dt.month
)

promedio_mensual = (
    promedio_diario
    .groupby("Mes", as_index=False)["SO2_promedio"]
    .mean()
)

promedio_mensual["Mes"] = (
    promedio_mensual["Mes"]
    .astype(str)
    .str.zfill(2)
)

display(promedio_mensual)

plt.figure(figsize=(11, 5))

sns.barplot(
    data=promedio_mensual,
    x="Mes",
    y="SO2_promedio",
    color="#67B7B2"
)

plt.title(
    "Concentración máxima diaria promedio de SO₂ por mes, 2023"
)

plt.xlabel("Mes")
plt.ylabel("SO₂ (ppb)")
plt.tight_layout()
plt.show()


# 10. Variable temporal

fecha_inicial = pd.Timestamp("2023-01-01")

promedio_diario["Dias"] = (
    promedio_diario["Date"] - fecha_inicial
).dt.days


# 11. Regresión lineal descriptiva con todos los datos

X_total = promedio_diario[["Dias"]]
y_total = promedio_diario["SO2_promedio"]

modelo_total = LinearRegression()
modelo_total.fit(X_total, y_total)

promedio_diario["SO2_estimado"] = (
    modelo_total.predict(X_total)
)

intercepto = modelo_total.intercept_
pendiente = modelo_total.coef_[0]
r2_total = modelo_total.score(X_total, y_total)

print(f"Intercepto: {intercepto:.4f}")
print(f"Pendiente: {pendiente:.6f} ppb/día")
print(f"R² descriptivo: {r2_total:.4f}")

print(
    f"Modelo: SO₂ estimado = "
    f"{intercepto:.4f} + "
    f"{pendiente:.6f}t"
)


# 12. Gráfico de regresión temporal

plt.figure(figsize=(12, 5))

plt.scatter(
    promedio_diario["Date"],
    promedio_diario["SO2_promedio"],
    alpha=0.55,
    s=20,
    label="Promedio diario observado"
)

plt.plot(
    promedio_diario["Date"],
    promedio_diario["SO2_estimado"],
    color="#EF4E4E",
    linewidth=2.5,
    label="Regresión lineal"
)

plt.title(
    "Regresión lineal de la concentración diaria promedio de SO₂, 2023"
)

plt.xlabel("Fecha")
plt.ylabel("SO₂ promedio entre estaciones (ppb)")
plt.legend()
plt.tight_layout()
plt.show()


# 13. División en entrenamiento y prueba

X = promedio_diario[["Dias"]]
y = promedio_diario["SO2_promedio"]

X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.20,
    random_state=42
)


# 14. Entrenamiento del modelo

modelo = LinearRegression()

modelo.fit(
    X_train,
    y_train
)

y_pred = modelo.predict(X_test)


# 15. Evaluación del modelo

mae = mean_absolute_error(
    y_test,
    y_pred
)

rmse = np.sqrt(
    mean_squared_error(
        y_test,
        y_pred
    )
)

r2 = r2_score(
    y_test,
    y_pred
)

print(f"MAE: {mae:.4f} ppb")
print(f"RMSE: {rmse:.4f} ppb")
print(f"R² de prueba: {r2:.4f}")


# 16. Valores observados y estimados

plt.figure(figsize=(7, 6))

plt.scatter(
    y_test,
    y_pred,
    color="#58A65C",
    alpha=0.70
)

limite_minimo = min(
    y_test.min(),
    y_pred.min()
)

limite_maximo = max(
    y_test.max(),
    y_pred.max()
)

plt.plot(
    [limite_minimo, limite_maximo],
    [limite_minimo, limite_maximo],
    color="#FF4E50",
    linestyle="--",
    label="Predicción ideal"
)

plt.title(
    "Valores observados y estimados en el conjunto de prueba"
)

plt.xlabel("SO₂ observado (ppb)")
plt.ylabel("SO₂ estimado (ppb)")
plt.legend()
plt.tight_layout()
plt.show()
```

</details>

---

## Referencias

[1] U.S. Environmental Protection Agency, “Sulfur Dioxide Basics,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/so2-pollution/sulfur-dioxide-basics. [Accedido: 18-sep-2026].

[2] U.S. Environmental Protection Agency, “AirData: Air Quality Data Collected at Outdoor Monitors Across the US,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/outdoor-air-quality-data. [Accedido: 18-sep-2026].

[3] U.S. Environmental Protection Agency, “Air Quality System,” *EPA*. [En línea]. Disponible en: https://www.epa.gov/aqs. [Accedido: 18-sep-2026].

[4] The pandas development team, “pandas documentation,” *pandas*. [En línea]. Disponible en: https://pandas.pydata.org/docs/. [Accedido: 18-sep-2026].

[5] Scikit-learn developers, “LinearRegression,” *scikit-learn documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html. [Accedido: 18-sep-2026].

[6] Scikit-learn developers, “Regression metrics,” *scikit-learn documentation*. [En línea]. Disponible en: https://scikit-learn.org/stable/modules/model_evaluation.html#regression-metrics. [Accedido: 18-sep-2026].

---

<div align="center">

**Análisis elaborado con Python y Google Colab**

**Datos analizados: año 2023**

</div>
</div>
