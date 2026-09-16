
# 📊 Gráficas propuestas para el modelo de detección de riesgo estructural

## 1. Relación entre las características de las grietas y el nivel de riesgo

Esta gráfica permitirá analizar la relación entre las diferentes características obtenidas de las grietas y el nivel de riesgo registrado en la base de datos. Mediante un gráfico de dispersión se podrán observar posibles patrones entre los datos de entrada y el nivel de riesgo asociado a cada caso.

Su importancia radica en que permite identificar si determinadas características de las grietas presentan una relación con situaciones de mayor riesgo estructural. Además, este análisis sirve como una primera aproximación para determinar qué variables pueden ser útiles para el entrenamiento del modelo de Machine Learning.

**Tabla de datos utilizada:**

| Características de las grietas | Nivel de riesgo |
|---|---|
| Datos recopilados de las grietas | Nivel de riesgo registrado |
| Datos recopilados de las grietas | Nivel de riesgo registrado |
| Datos recopilados de las grietas | Nivel de riesgo registrado |

### Gráfica 1

<img width="1442" height="844" alt="image" src="https://github.com/user-attachments/assets/1c0a3ea2-1c3b-473f-828c-7941814fac04" />


---

## 2. Comparación entre el riesgo real y el riesgo predicho

Esta gráfica permite evaluar el comportamiento del modelo de Machine Learning mediante la comparación entre los valores de riesgo reales registrados en la base de datos y los valores de riesgo estimados por el modelo.

La comparación permite observar qué tan cercanas son las predicciones realizadas a los valores reales. De esta manera, se puede evaluar visualmente el desempeño del modelo y determinar si existe una correspondencia adecuada entre el riesgo conocido y el riesgo estimado para nuevos registros.

Esta gráfica es especialmente importante porque representa directamente el objetivo de utilizar el modelo: **estimar el nivel de riesgo a partir de las características obtenidas de las grietas y de la información disponible.**

**Tabla de datos utilizada:**

| Riesgo real | Riesgo predicho |
|---:|---:|
| Valor real | Predicción del modelo |
| Valor real | Predicción del modelo |
| Valor real | Predicción del modelo |

### Gráfica 2

<img width="851" height="647" alt="image" src="https://github.com/user-attachments/assets/5e0958f6-51c0-432e-a0d9-df2a0b182546" />


---

## 3. Importancia relativa de las características

Esta gráfica muestra la importancia relativa de las diferentes características utilizadas por el modelo para realizar sus predicciones.

Su finalidad es identificar cuáles de las variables de entrada tienen una mayor influencia dentro del proceso de predicción. Esto permite interpretar mejor el funcionamiento del modelo y conocer qué características de las grietas o del entorno tienen mayor relevancia para determinar el nivel de riesgo.

Además, esta información puede ser útil para orientar futuras recopilaciones de datos, ya que permite conocer cuáles características deberían ser medidas o registradas con mayor atención.

**Tabla de datos utilizada:**

| Característica | Importancia relativa |
|---|---:|
| Característica 1 | Valor calculado |
| Característica 2 | Valor calculado |
| Característica 3 | Valor calculado |
| Característica 4 | Valor calculado |

### Gráfica 3

<img width="907" height="608" alt="image" src="https://github.com/user-attachments/assets/53824fbe-0049-48f0-a5a6-c8e353b22744" />


---

# 🔎 Justificación general de la selección

Las tres gráficas fueron seleccionadas porque permiten observar diferentes etapas del análisis realizado mediante Machine Learning.

La **primera gráfica** permite estudiar la relación entre los datos recopilados y el nivel de riesgo, ayudando a identificar patrones en las características de las grietas.

La **segunda gráfica** permite evaluar directamente las predicciones realizadas por el modelo mediante la comparación entre los valores reales y los valores estimados.

Finalmente, la **tercera gráfica** permite interpretar el modelo identificando qué características poseen mayor importancia durante la predicción.

En conjunto, las tres gráficas permiten presentar el proceso desde el **análisis de los datos**, pasando por la **predicción del riesgo**, hasta la **interpretación de las características utilizadas por el modelo**.
