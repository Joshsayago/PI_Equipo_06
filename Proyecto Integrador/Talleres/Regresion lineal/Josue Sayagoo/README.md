# Análisis de Datos: Predicción de Consumo de Energía

## 1. Resumen Estadístico de la Data
El conjunto de datos consta de 5000 registros sin valores nulos, lo que representa una base sólida y limpia para el modelamiento predictivo. 

| Variable | Conteo | Rango Mínimo | Rango Máximo | Observación |
| :--- | :--- | :--- | :--- | :--- |
| **Temperatura** | 5000 | 18.0 | 35.0 | Variable ambiental clave. |
| **Humedad** | 5000 | 40.0 | 90.0 | Condicionante de estrés térmico. |
| **Carga** | 5000 | 30.0 | 100.0 | Exigencia mecánica directa. |
| **Horas_Operacion** | 5000 | 2.0 | 12.0 | Tiempo de uso continuo. |
| **Consumo_Energia** | 5000 | 9.1 | 42.6 | **Variable Objetivo (Dependiente)** |

---

## 2. Análisis Visual: Los 4 Gráficos Clave

### Gráfico 1: Matriz de Dispersión General (Pairplot)
Este gráfico es el punto de partida crítico. Nos permite observar a simple vista las relaciones bivariadas entre todas las características ambientales/operativas y nuestra variable objetivo. Las diagonales confirman que las variables no presentan sesgos extremos.

![Matriz de Dispersión](pairplot.png)

### Gráfico 2: Mapa de Calor de Correlaciones (Heatmap)
El mapa de calor cuantifica lo observado en la dispersión. Al observar los coeficientes de correlación de Pearson, podemos identificar matemáticamente qué parámetro (por ejemplo, la Carga o la Temperatura) impacta con mayor fuerza el consumo energético antes de entrenar el modelo.

![Mapa de Calor de Correlaciones](heatmap.png)

### Gráfico 3: Distribución del Consumo de Energía
Es vital entender cómo se distribuye el esfuerzo energético. Este histograma nos confirma si el consumo tiene un comportamiento simétrico o si presenta picos anómalos que deban ser tratados.

![Distribución de Consumo](distribucion_consumo.png)

### Gráfico 4: Regresión Operativa (Carga vs. Consumo)
Aislando la variable operativa de mayor impacto, este gráfico de dispersión con línea de tendencia nos muestra visualmente la proporción directa entre el esfuerzo exigido al sistema y el salto en el gasto eléctrico.

![Carga vs Consumo](carga_vs_consumo.png)
