# 📊 Análisis de Consumo Energético y Variables Ambientales
E análisis exploratorio y predictivo de un sistema basado en 5,000 registros, evaluando cómo las condiciones del entorno y la exigencia operativa impactan el gasto eléctrico.

---

## 1. Mapa de Calor de Correlaciones (Heatmap)

Este gráfico nos permite identificar matemáticamente qué variable (Temperatura, Humedad, Carga u Horas de Operación) tiene la relación más fuerte con el Consumo de Energía. Los colores más intensos indicarán una mayor dependencia.

<img width="750" height="484" alt="image" src="https://github.com/user-attachments/assets/ea75d247-e082-4dba-b547-8e172e79897b" />

---

## 2. Relación Operativa vs Consumo de Energía

Al aislar la variable mecánica principal, este gráfico de dispersión ilustra la proporción directa entre el esfuerzo del sistema y el incremento en la demanda eléctrica. Nos ayuda a confirmar si la tendencia es estrictamente lineal.

<img width="1783" height="983" alt="image" src="https://github.com/user-attachments/assets/e54c6d5f-ef85-4c6e-bc23-ac1a082715a8" />


---

## 3. Distribución de los residuos (Histograma)

Para entender el comportamiento general del sistema, este histograma muestra la frecuencia de los distintos niveles de residuos. Un sesgo hacia la derecha o picos anómalos podrían indicar momentos de estrés o sobrecarga que requieren optimización.

<img width="925" height="425" alt="image" src="https://github.com/user-attachments/assets/fe934353-7d63-4fbc-b639-579eb9966161" />


---

## 4. Rendimiento del Modelo: Real vs. Predicción

Una vez entrenado el modelo de regresión, este gráfico evalúa su precisión comparando los valores reales registrados frente a las estimaciones calculadas. Mientras más se acerquen los puntos a la línea diagonal perfecta, mayor será la fiabilidad predictiva de nuestro algoritmo.

<img width="747" height="427" alt="image" src="https://github.com/user-attachments/assets/1c2353ea-d58f-4b06-ae1c-1f8beabd4b40" />

---

## 5. Recomendaciones de Implementación

* **Despliegue en Producción:** Se recomienda utilizar la **Regresión Lineal Múltiple**, ya que ofrece una mayor precisión global ($R^2 = 0.88$) con menor margen de error promedio.
* **Palancas de Control:** Las variables de mayor peso predictivo son `Carga` y `Horas_Operacion`. Reprogramar turnos de alta carga fuera de las horas de mayor temperatura ambiental reducirá los picos indeseados de consumo.
