## Introducción
El dióxido de nitrógeno (NO₂) es un gas altamente reactivo y uno de los principales contaminantes atmosféricos, vinculado principalmente a emisiones vehiculares e industriales. Para comunicar eficazmente el riesgo que este gas representa para la salud pública, la Agencia de Protección Ambiental (EPA) utiliza el Índice de Calidad del Aire (AQI). El presente informe tiene como objetivo analizar y cuantificar la relación estadística entre la concentración máxima diaria de NO₂ y el valor diario del AQI. Mediante un modelo de regresión lineal aplicado a registros de los años 2022 y 2023, este estudio busca demostrar la proporción en la que las variaciones de este contaminante impactan directamente en las métricas de calidad del aire.

## Metodología
El desarrollo de este análisis se estructuró en las siguientes fases técnicas y de procesamiento:

*   **Origen de los Datos:** Se utilizó un conjunto de datos históricos públicos extraídos del portal *AirData* de la Agencia de Protección Ambiental de Estados Unidos (US EPA). El archivo fuente compila las mediciones diarias de concentración del contaminante y sus índices asociados de monitoreo.
*   **Herramientas y Entorno:** El análisis computacional se ejecutó en el entorno de Google Colab. Se empleó Python como lenguaje principal, utilizando la librería `pandas` para la manipulación y estructuración de datos, `scikit-learn` para la construcción del modelo de regresión, y el conjunto de `matplotlib` y `seaborn` para la visualización de métricas de desempeño y diagnóstico estadístico de residuos.
*   **Procesamiento y Filtrado:** El conjunto de datos original fue filtrado para aislar de manera exclusiva los registros comprendidos entre el 1 de enero de 2022 y el 31 de diciembre de 2023. Posteriormente, se realizó una limpieza de datos eliminando aquellas filas con valores nulos o incompletos en las variables de interés, garantizando así la solidez matemática del análisis.
*   **Desarrollo y Evaluación del Modelo:** Se implementó un algoritmo de Regresión Lineal Simple en el cual la Concentración Máxima Diaria de NO₂ se definió como la variable independiente (X) y el Valor Diario del AQI como la variable dependiente (Y). Para validar la capacidad de predicción del modelo de manera rigurosa, el conjunto de datos se dividió aleatoriamente, destinando el 70% de las observaciones para el entrenamiento del algoritmo y reservando el 30% restante para las pruebas de validación de los datos no vistos.
## Resultados

El análisis de los datos extraídos arrojó resultados estadísticos contundentes que validan la relación directa entre las mediciones del contaminante y el índice reportado. A continuación, se detalla la interpretación de los gráficos y métricas generadas:

**1. Análisis de Correlación Exploratorio**
<p align = center>
<img width="956" height="874" alt="image" src="https://github.com/user-attachments/assets/21c8b11e-b0d8-4402-8caf-1024a299c8ac" />
El mapa de calor de correlación permitió filtrar el ruido del conjunto de datos y enfocarse en las variables cuantitativas más relevantes. Se observa una correlación positiva casi perfecta entre la `Daily Max NO2 Concentration` y el `Daily AQI Value`. Otras variables, como el conteo de observaciones (`Daily Obs Count`) o la elevación del sitio (`Elevation (m)`), mostraron coeficientes de correlación cercanos a cero frente al AQI, confirmando que no influyen en el cálculo de este índice.

**2. Relación de Variables Múltiples contra el AQI**
<p align = center>
<img width="1788" height="990" alt="image" src="https://github.com/user-attachments/assets/9aceb607-b301-4c2f-9785-a6a1295a7e05" />


Para corroborar visualmente los hallazgos del mapa de calor, se graficaron cuatro variables independientes contra el AQI real. Como se evidencia en la primera subtrama, los puntos de la concentración de NO₂ forman una línea recta ascendente muy clara. Por el contrario, las otras tres variables (observaciones, porcentaje completo y elevación) muestran nubes de puntos horizontales y dispersas, lo que reafirma la decisión de construir el modelo predictivo exclusivamente basándonos en la concentración de NO₂.

**3. Desempeño del Modelo Predictivo**
Al entrenar el modelo de Regresión Lineal Simple con el 70% de los datos y validarlo con el 30% restante, se obtuvieron las siguientes métricas:
* **Coeficiente de determinación (R²):** 0.9979
* **Coeficiente (Pendiente):** 0.9437
* **Intercepción:** -0.4592
<p align = center>
<img width="790" height="590" alt="image" src="https://github.com/user-attachments/assets/495db06d-bb69-4821-ae88-27f29dd31b96" />


El valor de R² indica que el modelo logra explicar el 99.79% de la varianza en los datos. Visualmente, esto se confirma en el gráfico de valores reales versus predichos, donde las predicciones del modelo (puntos morados) se alinean de manera casi milimétrica sobre la "Meta ideal" (línea roja de 45°). Esto demuestra que el margen de error de predicción es mínimo en todas las escalas evaluadas.

**4. Diagnóstico y Validación Estadística de los Errores (Residuos)**
Para garantizar que el modelo matemático sea robusto y no producto de la casualidad, se analizaron sus residuos (la diferencia entre el valor real y la predicción) a través de dos pruebas visuales:
<p align = center>
<img width="790" height="490" alt="image" src="https://github.com/user-attachments/assets/94ddd0ea-bbe9-451f-975c-def2f94ef114" />


**Normalidad de los errores:** El histograma de densidad de kernel muestra una distribución normal perfecta (forma de campana de Gauss) centrada exactamente en el valor 0. Esto significa que la inmensa mayoría de las predicciones del modelo fueron exactas o tuvieron errores minúsculos, validando matemáticamente la confiabilidad de la regresión.
<p align = center>
<img width="874" height="594" alt="image" src="https://github.com/user-attachments/assets/a5ae43d3-f90f-4bde-bb64-a5a71959c6c8" />


**Homocedasticidad:** El gráfico de dispersión de los residuos frente a los valores predichos exhibe una distribución completamente aleatoria alrededor de la línea horizontal de error cero (Y=0). Al no observarse patrones en forma de cono, embudo o curvas, se confirma que la varianza de los errores es constante en todo el espectro de datos, cumpliendo así con las asunciones teóricas de la regresión lineal.

---

## Discusión

El modelo de regresión lineal aplicado demostró una eficacia predictiva excepcional (R² = 0.9979) al evaluar el impacto de la concentración diaria de NO₂ sobre el AQI. Desde una perspectiva técnica, este nivel de precisión casi absoluto es un resultado esperado y lógico. El Índice de Calidad del Aire (AQI) no es una variable aleatoria o empírica, sino un indicador estandarizado que las agencias gubernamentales calculan matemáticamente a partir de las concentraciones de los contaminantes. En la práctica, nuestro modelo de *machine learning* ha logrado "hacer ingeniería inversa" a la fórmula exacta que utiliza la EPA para asignar el índice de riesgo basado en el NO₂.

Además, las pruebas de diagnóstico de residuos (normalidad y homocedasticidad) superaron todos los criterios estadísticos, lo que descarta cualquier sesgo algorítmico en las predicciones. Este análisis demuestra cómo herramientas computacionales simples, pero bien calibradas, pueden mapear relaciones exactas en bases de datos ambientales masivas, permitiendo predecir alertas de salud pública (como el AQI) de manera instantánea a partir de las lecturas directas de los sensores de calidad del aire.

---

## Referencias

[1] U.S. Environmental Protection Agency, "AirData," EPA, Washington, D.C., 2026. [Online]. Available: https://www.epa.gov/outdoor-air-quality-data.
[2] F. Pedregosa *et al.*, "Scikit-learn: Machine Learning in Python," *J. Mach. Learn. Res.*, vol. 12, pp. 2825–2830, 2011.
[3] J. D. Hunter, "Matplotlib: A 2D graphics environment," *Comput. Sci. Eng.*, vol. 9, no. 3, pp. 90-95, 2007.
[4] M. L. Waskom, "Seaborn: statistical data visualization," *J. Open Source Softw.*, vol. 6, no. 60, p. 3021, 2021.
