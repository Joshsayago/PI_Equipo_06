# Taller de Redes Neuronales

## Clasificación de imágenes, análisis de sobreajuste y fundamentos del perceptrón

<div align="center">

**Estudiante:** Mónica Huamán Bernal
**Equipo:** Equipo 06
**Curso:** Proyecto Integrador

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge\&logo=googlecolab\&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge\&logo=pytorch\&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=for-the-badge\&logo=keras\&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge\&logo=scikit-learn\&logoColor=white)

</div>

---

# 1. Introducción

Las **redes neuronales artificiales** son modelos computacionales capaces de aprender relaciones a partir de datos mediante unidades conectadas denominadas neuronas. Durante el entrenamiento, los pesos de estas conexiones se ajustan para reducir el error entre las predicciones del modelo y los valores reales.

En el presente taller se estudiaron diferentes arquitecturas y estrategias de aprendizaje automático aplicadas a problemas de clasificación. Se trabajó inicialmente con una **red neuronal convolucional (CNN)** para clasificar imágenes de las categorías *glass* y *plastic*. Posteriormente, se evaluó el efecto del **data augmentation** y se implementó **transfer learning** utilizando una arquitectura **ResNet18** preentrenada.

También se estudió una red neuronal densa mediante **Keras**, utilizando el conjunto de datos IMDb para clasificar reseñas de películas como positivas o negativas. En este caso se analizaron conceptos como **sobreajuste, capacidad del modelo, regularización L2 y dropout**.

Finalmente, se implementó un **perceptrón** desde cero para comprender el funcionamiento básico de una neurona artificial, las funciones de activación y las fronteras de decisión. Se analizaron las compuertas lógicas **AND, OR y XOR**, mostrando la limitación de un único perceptrón para resolver problemas que no son linealmente separables.

El objetivo del taller fue comprender tanto el funcionamiento de las redes neuronales como las estrategias utilizadas para mejorar su capacidad de generalización e interpretar sus predicciones.

---

# 2. Metodología

## 2.1. Red neuronal convolucional entrenada desde cero

Se construyó una CNN sencilla utilizando **PyTorch**. La arquitectura estuvo compuesta por bloques de convolución, función de activación ReLU y reducción espacial mediante *max pooling*.

La arquitectura implementada fue:

* `Conv2d(1, 16)` + ReLU + MaxPool
* `Conv2d(16, 32)` + ReLU + MaxPool
* `Conv2d(32, 64)` + ReLU
* `AdaptiveAvgPool2d`
* Capa `Linear` para la clasificación final

La arquitectura puede representarse conceptualmente como:

**Imagen → Convolución → ReLU → Pooling → Convolución → ReLU → Pooling → Convolución → ReLU → Clasificador**

El modelo fue entrenado utilizando:

* **Función de pérdida:** `CrossEntropyLoss`
* **Optimizador:** Adam
* **Tasa de aprendizaje:** `0.001`
* **Número de épocas:** 8

La evaluación se realizó mediante **accuracy**, **ROC-AUC**, matriz de confusión, precision, recall y F1-score.

La función `accuracy` representa el porcentaje de predicciones correctas, mientras que **ROC-AUC** permite evaluar la capacidad del modelo para distinguir entre las dos clases.

---

## 2.2. Curvas de entrenamiento

Durante el entrenamiento se registraron la pérdida (`loss`), la exactitud de validación (`accuracy`) y el área bajo la curva ROC (`ROC-AUC`) para cada época.

<div align="center">

<<img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/7d072232-9857-40a4-b794-3801ec6050bd" />
>

</div>

**Figura 1. Curvas de entrenamiento y métricas de validación de la CNN entrenada desde cero.**

### Interpretación

La pérdida de entrenamiento disminuyó progresivamente, indicando que la red estaba aprendiendo patrones presentes en las imágenes.

A partir de aproximadamente la cuarta época se observó una mejora en la exactitud de clasificación, alcanzando un valor de validación de **63.27 %**. El ROC-AUC se mantuvo aproximadamente entre **0.67 y 0.69**, mostrando una capacidad moderada para distinguir entre las clases *glass* y *plastic*.

Sin embargo, el desempeño final sobre el conjunto de prueba fue inferior al observado durante la validación, lo que indica que la capacidad de generalización del modelo entrenado desde cero fue limitada.

---

## 2.3. Evaluación de la CNN

Una vez terminado el entrenamiento, el modelo fue evaluado utilizando el conjunto de prueba.

Los resultados obtenidos fueron:

| Métrica  |  Resultado |
| -------- | ---------: |
| Accuracy | **0.5503** |
| ROC-AUC  | **0.6191** |

La matriz de confusión obtenida fue:

|            | Predicción 0 | Predicción 1 |
| ---------- | -----------: | -----------: |
| **Real 0** |           38 |           38 |
| **Real 1** |           29 |           44 |

<div align="center">

<<img width="364" height="346" alt="image" src="https://github.com/user-attachments/assets/ae2ff6ee-0426-4e0e-a751-422225bc722f" />
/>

</div>

**Figura 2. Matriz de confusión de la CNN entrenada desde cero.**

### Interpretación

El modelo alcanzó una exactitud de **55.03 %** sobre el conjunto de prueba y un ROC-AUC de **0.6191**.

De las 76 observaciones pertenecientes a la clase 0, el modelo clasificó correctamente 38 y confundió 38 con la clase 1. Para la clase 1, clasificó correctamente 44 de 73 observaciones y confundió 29 con la clase 0.

Los valores obtenidos mediante el reporte de clasificación fueron:

| Clase | Precision | Recall | F1-score |
| ----- | --------: | -----: | -------: |
| 0     |    0.5672 | 0.5000 |   0.5315 |
| 1     |    0.5366 | 0.6027 |   0.5677 |

Estos resultados muestran que la CNN entrenada desde cero presentó una capacidad de clasificación limitada para este conjunto de imágenes.

---

# 3. Data augmentation

## 3.1. Aumento de datos

Para intentar mejorar la capacidad de generalización de la CNN se aplicó **data augmentation**.

Se utilizaron:

* Rotaciones aleatorias de hasta ±10°.
* Traslaciones horizontales y verticales de hasta 5 %.

El objetivo del aumento de datos fue generar variaciones de las imágenes originales sin modificar su categoría, permitiendo que el modelo aprendiera características menos dependientes de una posición o orientación específica.

<div align="center">

<<img width="931" height="153" alt="image" src="https://github.com/user-attachments/assets/09a2bfca-12c0-4c75-a4c7-92ab11e3c213" />
 />

</div>

**Figura 3. Entrenamiento de la CNN utilizando data augmentation.**

### Interpretación

Con el aumento de datos, la exactitud de validación continuó aumentando durante las seis épocas de entrenamiento y alcanzó **65.31 %** en la última época. El ROC-AUC se mantuvo alrededor de **0.67**.

Al evaluar el modelo en el conjunto de prueba se obtuvo:

| Modelo               | Accuracy | ROC-AUC |
| -------------------- | -------: | ------: |
| CNN sin augmentation |   0.5503 |  0.6191 |
| CNN con augmentation |   0.5638 |  0.6411 |

El uso de augmentation produjo una mejora en ambas métricas de prueba. La exactitud aumentó de **55.03 % a 56.38 %**, mientras que el ROC-AUC aumentó de **0.6191 a 0.6411**.

Esto indica que las transformaciones utilizadas aportaron cierta mejora en la generalización del modelo, aunque el incremento fue moderado.

---

# 4. Transfer Learning con ResNet18

## 4.1. Modelo preentrenado

Posteriormente se utilizó **transfer learning**, reutilizando una arquitectura ResNet18 previamente entrenada.

Para adaptar las imágenes al modelo preentrenado se realizaron las siguientes transformaciones:

* Redimensionamiento a `224 × 224`.
* Rotaciones pequeñas.
* Traslaciones.
* Conversión a tensor.
* Conversión de imágenes de un canal a tres canales mediante repetición del canal.

La última capa de ResNet18 fue reemplazada por una capa lineal con el número de clases correspondiente al problema.

Inicialmente se congelaron los parámetros del modelo y solamente se entrenó la capa final.

---

## 4.2. Entrenamiento de la capa final

Durante esta primera etapa se obtuvieron los siguientes resultados:

| Época | Accuracy validación | ROC-AUC validación |
| ----: | ------------------: | -----------------: |
|     1 |              0.6395 |             0.7152 |
|     2 |              0.6122 |             0.7739 |
|     3 |              0.7279 |             0.8169 |
|     4 |              0.5782 |             0.8207 |

El ROC-AUC aumentó progresivamente hasta **0.8207**, mostrando una mejora en la capacidad del modelo para distinguir las dos clases.

---

## 4.3. Fine-tuning

Después de entrenar la capa final se realizó **fine-tuning**, descongelando `layer4` y la capa `fc` de ResNet18.

En esta etapa se utilizó una tasa de aprendizaje menor:

**Learning rate = 0.0001**

Los resultados fueron:

| Época | Accuracy validación | ROC-AUC validación |
| ----: | ------------------: | -----------------: |
|     1 |              0.7891 |             0.9165 |
|     2 |              0.8231 |             0.9531 |
|     3 |              0.8639 |             0.9602 |
|     4 |              0.8844 |             0.9676 |

 

**Figura 4. Evolución de las métricas durante el fine-tuning de ResNet18.**

### Interpretación

Durante el fine-tuning se observó una mejora progresiva tanto en la exactitud como en el ROC-AUC. La última época alcanzó una exactitud de validación de **88.44 %** y un ROC-AUC de **0.9676**.

Esto muestra que permitir que algunas de las capas finales de la red ajustaran sus parámetros al problema específico permitió mejorar considerablemente el desempeño respecto a la CNN entrenada desde cero.

---

## 4.4. Evaluación final de ResNet18

En el conjunto de prueba, el modelo obtuvo:

| Métrica  |  Resultado |
| -------- | ---------: |
| Accuracy | **0.8658** |
| ROC-AUC  | **0.9562** |

La matriz de confusión fue:

|            | Predicción 0 | Predicción 1 |
| ---------- | -----------: | -----------: |
| **Real 0** |           72 |            4 |
| **Real 1** |           16 |           57 |

 

**Figura 5. Matriz de confusión del modelo ResNet18 después del transfer learning y fine-tuning.**

Los resultados de clasificación fueron:

| Clase | Precision | Recall | F1-score |
| ----- | --------: | -----: | -------: |
| 0     |    0.8182 | 0.9474 |   0.8780 |
| 1     |    0.9344 | 0.7808 |   0.8507 |

### Interpretación

El modelo clasificó correctamente **72 de las 76 observaciones de la clase 0** y **57 de las 73 observaciones de la clase 1**.

El accuracy de **86.58 %** indica que el modelo realizó correctamente la mayor parte de las clasificaciones del conjunto de prueba. Además, el ROC-AUC de **0.9562** muestra una elevada capacidad de separación entre las dos clases.

El desempeño también fue más equilibrado que el obtenido por la CNN entrenada desde cero.

---

# 5. Comparación de los modelos CNN

Los resultados finales obtenidos fueron:

| Modelo                       |   Accuracy |    ROC-AUC |
| ---------------------------- | ---------: | ---------: |
| CNN desde cero               | **0.5503** | **0.6191** |
| CNN + data augmentation      | **0.5638** | **0.6411** |
| ResNet18 + transfer learning | **0.8658** | **0.9562** |

 

**Figura 6. Comparación del desempeño de los tres modelos CNN evaluados.**

### Interpretación

La CNN entrenada desde cero obtuvo un accuracy de **55.03 %**. Al incorporar data augmentation, el desempeño aumentó moderadamente hasta **56.38 %**.

El modelo basado en ResNet18 alcanzó un accuracy de **86.58 %** y un ROC-AUC de **0.9562**.

La diferencia observada muestra que reutilizar características aprendidas previamente mediante transfer learning permitió obtener un desempeño considerablemente mayor en este conjunto de datos que entrenar una CNN pequeña completamente desde cero.

---

# 6. Interpretabilidad mediante Grad-CAM

Para analizar qué regiones de una imagen influyeron en la predicción del modelo se implementó una versión simplificada de **Grad-CAM** sobre la capa `layer4` de ResNet18.

Grad-CAM genera un mapa de calor asociado a la contribución de diferentes regiones de la imagen en la predicción.

<div align="center">

<<img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/03072ded-5d43-475c-bc79-717be70d5c29" />
 />

</div>

**Figura 7. Interpretación de una predicción mediante Grad-CAM: imagen original, mapa de calor y superposición.**

### Interpretación

Las regiones con mayor intensidad en el mapa de Grad-CAM representan aquellas zonas que tuvieron una mayor contribución a la predicción de la red.

Por el contrario, las regiones con menor intensidad representan zonas con una contribución menor.

Esta herramienta permite complementar las métricas de desempeño, ya que no solamente muestra si el modelo clasifica correctamente, sino también **qué regiones de la imagen influyeron en su decisión**.

---

# 7. Clasificación binaria con Keras

## 7.1. Conjunto de datos IMDb

Se utilizó el conjunto de datos **IMDb** para clasificar reseñas de películas en dos categorías:

* **0:** reseña negativa.
* **1:** reseña positiva.

Las reseñas fueron transformadas en representaciones numéricas utilizando un vocabulario de **10 000 palabras**.

Posteriormente se aplicó **one-hot encoding**, transformando cada reseña en un vector binario donde:

* `0` representa una palabra ausente.
* `1` representa una palabra presente.

---

## 7.2. Construcción de la red

Se construyó una red neuronal secuencial mediante Keras con la siguiente arquitectura:

**Entrada → Dense(16) → Dense(16) → Dense(1)**

Las dos capas ocultas utilizaron la función de activación **ReLU**, mientras que la capa de salida utilizó **sigmoid**.

La función de pérdida utilizada fue `binary_crossentropy`, adecuada para una clasificación binaria.

El modelo se entrenó durante **20 épocas**, utilizando un tamaño de lote de **512**.

---

## 7.3. Análisis del sobreajuste

Durante el entrenamiento se compararon las pérdidas de entrenamiento y validación.

<div align="center">

<<img width="826" height="813" alt="image" src="https://github.com/user-attachments/assets/3eb6aba3-7dcd-4355-bc89-7eb3f5eef29c" />
/>

</div>

**Figura 8. Pérdida de entrenamiento y validación de la red neuronal con Keras.**

### Interpretación

La pérdida de entrenamiento disminuyó progresivamente hasta valores muy bajos, mientras que la pérdida de validación dejó de disminuir y posteriormente comenzó a aumentar.

Esto evidencia la presencia de **sobreajuste**.

El modelo continuó aprendiendo cada vez mejor los datos utilizados para el entrenamiento, pero su capacidad de generalización comenzó a disminuir.

En la evaluación sobre el conjunto de prueba se obtuvo:

* **Loss:** 0.6056
* **Accuracy:** 86.11 %

---

# 8. Red neuronal más pequeña

Para analizar el efecto de la capacidad del modelo se construyó una segunda red con menor número de neuronas:

**Entrada → Dense(4) → Dense(1)**

En comparación con la red original, esta arquitectura posee una capacidad mucho menor.

<div align="center">

<<img width="835" height="813" alt="image" src="https://github.com/user-attachments/assets/cc1bd973-bc3e-4ef2-801c-34c0e2bb289d" />
>

</div>

**Figura 9. Comparación de la pérdida de validación entre la red original y la red de menor tamaño.**

### Interpretación

La red original presentó un sobreajuste más pronunciado. En cambio, el modelo más pequeño mantuvo el mínimo de pérdida durante un mayor número de épocas y el incremento posterior fue menor.

Esto muestra que reducir la capacidad de la red puede disminuir el sobreajuste, aunque un modelo demasiado pequeño también puede tener dificultades para aprender patrones complejos.

---

# 9. Regularización L2

Se implementó regularización **L2** en las capas ocultas de la red original.

La regularización agrega una penalización asociada al tamaño de los pesos del modelo, con el objetivo de evitar que la red dependa excesivamente de determinadas conexiones.

<div align="center">

<<img width="826" height="813" alt="image" src="https://github.com/user-attachments/assets/6deba140-fccb-486e-bd2f-0a3290d817a9" />
/>

</div>

**Figura 10. Comparación de la pérdida de validación con y sin regularización L2.**

### Interpretación

La regularización modifica el proceso de aprendizaje al penalizar pesos elevados. Por esta razón, la curva de pérdida puede presentar valores mayores en determinadas épocas respecto al modelo original.

El objetivo no es necesariamente reducir inmediatamente la pérdida de entrenamiento, sino favorecer una representación que generalice mejor hacia datos no utilizados durante el entrenamiento.

---

# 10. Dropout

Otra estrategia utilizada para reducir el sobreajuste fue **Dropout**.

Se incorporó:

`Dropout(0.5)`

después de cada una de las dos capas ocultas.

Durante el entrenamiento, aproximadamente el **50 % de las neuronas** de estas capas se desactiva aleatoriamente en cada iteración.

<div align="center">

<<img width="835" height="813" alt="image" src="https://github.com/user-attachments/assets/c1a4f39c-5579-48fe-aceb-c4366baf66ce" />
>

</div>

**Figura 11. Comparación de la pérdida de validación con Dropout y sin Dropout.**

### Interpretación

El Dropout obliga a la red a aprender utilizando diferentes combinaciones de neuronas durante el entrenamiento.

De esta manera se busca reducir la dependencia excesiva de determinadas neuronas y mejorar la capacidad de generalización del modelo.

---

# 11. Predicción con la red neuronal

Finalmente, se utilizó el modelo para realizar predicciones sobre el conjunto de prueba.

Para una de las reseñas analizadas se obtuvo una probabilidad de:

**99.38 %**

para la clase positiva.

Esto significa que el modelo asignó una probabilidad elevada a que dicha reseña perteneciera a la categoría de reseñas positivas.

---

# 12. Perceptrón

## 12.1. Funcionamiento básico

El perceptrón constituye una representación sencilla de una neurona artificial.

El proceso puede expresarse como:

**Entradas → suma ponderada + bias → función de activación → salida**

La suma ponderada utilizada fue:

**z = w₁x₁ + w₂x₂ + b**

Posteriormente, el resultado se transforma mediante una función de activación.

En el taller se implementaron dos funciones:

* Función escalón.
* Función `tanh`.

---

## 12.2. Función escalón y función tanh

La función escalón transforma el resultado en una salida binaria:

* `0`
* `1`

Por otro lado, `tanh` transforma el resultado a un valor entre **−1 y 1**.

Para el ejemplo de sobrecalentamiento del equipo se obtuvo:

| Función |  Salida |
| ------- | ------: |
| Escalón |       0 |
| tanh    | -0.9999 |

En ambos casos la salida indicó que el equipo **no presentaba una alerta de sobrecalentamiento**.

### Interpretación

La función de activación es la encargada de transformar la suma ponderada de las entradas en una salida que puede utilizarse para tomar una decisión.

---

# 13. Perceptrón y compuertas lógicas

## 13.1. Compuerta AND

Para la primera configuración se utilizaron:

* Pesos: `[0.4, 0.4]`
* Bias: `-0.5`

El resultado fue:

|  P |  Q | Predicción |
| -: | -: | ---------: |
|  0 |  0 |          0 |
|  0 |  1 |          0 |
|  1 |  0 |          0 |
|  1 |  1 |          1 |

El perceptrón produce `1` únicamente cuando ambas entradas son `1`, por lo que reproduce el comportamiento de una compuerta **AND**.

---

## 13.2. Segunda configuración

Con:

* Pesos: `[0.8, 0.5]`
* Bias: `-0.7`

se obtuvo:

|  P |  Q | Predicción |
| -: | -: | ---------: |
|  0 |  0 |          0 |
|  0 |  1 |          0 |
|  1 |  0 |          1 |
|  1 |  1 |          1 |

En esta configuración la salida depende principalmente de la primera entrada, debido al mayor peso asignado a `P`.

---

## 13.3. Compuerta OR

Para representar OR se utilizaron:

* Pesos: `[2, 1]`
* Bias: `-0.5`

El perceptrón produce `1` cuando al menos una de las entradas es `1`.

Por lo tanto:

|  P |  Q | OR |
| -: | -: | -: |
|  0 |  0 |  0 |
|  0 |  1 |  1 |
|  1 |  0 |  1 |
|  1 |  1 |  1 |

---

# 14. El problema XOR

La compuerta XOR produce `1` cuando las entradas son diferentes:

|  P |  Q | XOR |
| -: | -: | --: |
|  0 |  0 |   0 |
|  0 |  1 |   1 |
|  1 |  0 |   1 |
|  1 |  1 |   0 |

<div align="center">

<<img width="503" height="505" alt="image" src="https://github.com/user-attachments/assets/b57fecaf-2711-43fa-95ff-39a13e3f88e6" />
 />

</div>

**Figura 12. Fronteras de decisión utilizadas para representar AND y OR.**

<div align="center">

<<img width="503" height="505" alt="image" src="https://github.com/user-attachments/assets/09f33833-ade2-41ff-a72d-a5e4f7b31a9b" />
/>

</div>

**Figura 13. Representación del problema XOR y sus fronteras de decisión.**

### Interpretación

El perceptrón simple genera una **frontera de decisión lineal**. Por esta razón puede separar problemas como AND y OR, pero no puede separar correctamente los casos correspondientes a XOR utilizando una sola neurona.

En el gráfico, los casos de XOR no pueden separarse mediante una única línea recta.

La solución consiste en utilizar más de un perceptrón organizado en capas:

**Un perceptrón → no puede resolver XOR**

**Múltiples perceptrones + capa de salida → pueden representar XOR**

Este concepto constituye una de las bases para comprender por qué las redes neuronales utilizan **múltiples capas y neuronas**.

---

# 15. Conclusiones

1. Se estudiaron diferentes modelos de redes neuronales aplicados a problemas de clasificación, incluyendo una CNN, redes densas implementadas con Keras y un perceptrón.

2. La CNN entrenada desde cero obtuvo un **accuracy de 55.03 %** y un **ROC-AUC de 0.6191** en el conjunto de prueba. La aplicación de data augmentation produjo una mejora moderada, alcanzando **56.38 % de accuracy** y **0.6411 de ROC-AUC**.

3. El modelo basado en **ResNet18 mediante transfer learning y fine-tuning** obtuvo un accuracy de **86.58 %** y un ROC-AUC de **0.9562**, mostrando una mejora considerable respecto a las CNN entrenadas desde cero en este conjunto de datos.

4. El análisis mediante **Grad-CAM** permitió visualizar las regiones de las imágenes que tuvieron mayor influencia en las predicciones realizadas por ResNet18, proporcionando una herramienta básica de interpretabilidad.

5. En el problema de clasificación de reseñas IMDb, la red neuronal densa alcanzó una exactitud de **86.11 %** sobre el conjunto de prueba. Sin embargo, las curvas de entrenamiento y validación mostraron evidencia de sobreajuste.

6. La reducción del tamaño de la red, la regularización L2 y el Dropout fueron estudiados como estrategias para disminuir el sobreajuste y mejorar la generalización.

7. El perceptrón permitió comprender el funcionamiento básico de una neurona artificial mediante entradas, pesos, bias y funciones de activación.

8. El análisis de las compuertas AND, OR y XOR permitió observar que un único perceptrón puede representar fronteras de decisión lineales, pero presenta limitaciones frente a problemas que no son linealmente separables, como XOR.

9. En conjunto, el taller permitió relacionar los conceptos fundamentales de las redes neuronales con estrategias prácticas de entrenamiento, evaluación, regularización, transferencia de aprendizaje e interpretabilidad.

---

# 16. Código

El código completo utilizado para el desarrollo del taller se encuentra disponible en Google Colab.

<div align="center">

### 💻 Proyecto en Google Colab

<a href="TU_LINK_DE_COLAB">
  <img src="https://img.shields.io/badge/Abrir%20en-Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Abrir en Google Colab">
</a>

<br><br>

**Proyecto Integrador — Equipo 06**

</div>

---

<div align="center">

**Proyecto Integrador — Equipo 06**
**Mónica Huamán Bernal**

</div>

