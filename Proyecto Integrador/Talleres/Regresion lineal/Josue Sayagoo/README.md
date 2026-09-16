# Análisis de Consumo Energético y Variables Ambientales
Un análisis exploratorio y predictivo de un sistema basado en 5,000 registros, evaluando cómo las condiciones del entorno y la exigencia operativa impactan el gasto eléctrico.

---

## 1. Mapa de Calor de Correlaciones (Heatmap)

Este gráfico nos permite identificar matemáticamente qué variable (Temperatura, Humedad, Carga u Horas de Operación) tiene la relación más fuerte con el Consumo de Energía. Los colores más intensos indicarán una mayor dependencia.
<div align="center">
<img width="750" height="484" alt="image" src="https://github.com/user-attachments/assets/ea75d247-e082-4dba-b547-8e172e79897b" />
  
---

## 2. Relación Operativa vs Consumo de Energía

Al aislar la variable mecánica principal, este gráfico de dispersión ilustra la proporción directa entre el esfuerzo del sistema y el incremento en la demanda eléctrica. Nos ayuda a confirmar si la tendencia es estrictamente lineal.
<div align="center">
<img width="1783" height="983" alt="image" src="https://github.com/user-attachments/assets/e54c6d5f-ef85-4c6e-bc23-ac1a082715a8" />
<p>

---

## 3. Distribución de los residuos (Histograma)

Para entender el comportamiento general del sistema, este histograma muestra la frecuencia de los distintos niveles de residuos. Un sesgo hacia la derecha o picos anómalos podrían indicar momentos de estrés o sobrecarga que requieren optimización.
<div align="center">
<img width="925" height="425" alt="image" src="https://github.com/user-attachments/assets/fe934353-7d63-4fbc-b639-579eb9966161" />
<p>

---

## 4. Rendimiento del Modelo: Real vs. Predicción

Una vez entrenado el modelo de regresión, este gráfico evalúa su precisión comparando los valores reales registrados frente a las estimaciones calculadas. Mientras más se acerquen los puntos a la línea diagonal perfecta, mayor será la fiabilidad predictiva de nuestro algoritmo.
<div align="center">
<img width="747" height="427" alt="image" src="https://github.com/user-attachments/assets/1c2353ea-d58f-4b06-ae1c-1f8beabd4b40" />
<p>
---

## ¿Por qué son importantes estos gráficos?

En cualquier proyecto de ciencia de datos, los gráficos no son solo ilustraciones, sino herramientas de diagnóstico y validación. En este análisis, cada visualización cumple una función vital:

*   **Mapa de Calor de Correlaciones:** Es el punto de partida estadístico. Es importante porque resume en una sola imagen múltiples variables, permitiendo identificar de un vistazo (a través de la intensidad del color) cuáles factores ambientales u operativos "mueven la aguja" del consumo energético y cuáles pueden descartarse.
*   **Gráfico de Dispersión (Operación vs. Consumo):** Es crucial para la toma de decisiones metodológicas. Al confirmar visualmente que el consumo aumenta de manera proporcional al esfuerzo mecánico, se justifica matemáticamente el uso de modelos lineales (como la Regresión Lineal elegida).
*   **Histograma de Residuos:** Es la herramienta principal para auditar la "salud" del modelo. Los residuos son los errores de la predicción. Visualizar su distribución es importante porque permite detectar si el modelo tiene puntos ciegos, sesgos o si existen momentos de estrés operativo anómalo que las matemáticas no están logrando explicar.
*   **Rendimiento del Modelo (Real vs. Predicción):** Es la prueba de fuego y la mejor forma de comunicar el valor del### ¿Por qué son importantes estos gráficos?

Rendimiento del Modelo (Real vs. Predicción): Es la prueba de fuego y la mejor forma de comunicar el valor del proyecto a perfiles no técnicos. Demuestra visualmente la confiabilidad de las predicciones; la cercanía de los puntos a la línea diagonal certifica que el algoritmo está listo para ser utilizado en el entorno real y generar ahorros.
