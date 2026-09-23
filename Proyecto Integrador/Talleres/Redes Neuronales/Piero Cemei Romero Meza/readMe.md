--**Interpretación**--

**CNN:**

La utilización de redes neuronales convolucionales (CNN) resulta especialmente importante para el proyecto debido a que una de las principales fuentes de información serán las fotografías de grietas presentes en paredes y otras estructuras. A diferencia de otros modelos que trabajan principalmente con datos numéricos o tabulares, una CNN está diseñada para trabajar directamente con imágenes, aprendiendo características visuales a partir de los píxeles. Esto permite que el modelo pueda reconocer patrones relacionados con bordes, texturas, formas y estructuras presentes en una grieta.

Esto resulta útil para el proyecto porque se plantea trabajar con un dataset compuesto por fotografías de grietas clasificadas según diferentes niveles y condiciones. Mediante el entrenamiento, la red puede aprender las características que diferencian una clase de otra y posteriormente utilizar ese aprendizaje para analizar una nueva fotografía. Por lo tanto, la CNN representa una posible base para automatizar el análisis visual de las grietas en lugar de depender únicamente de una evaluación manual.

Dentro del notebook, esta metodología se implementa mediante PyTorch. Uno de los elementos importantes del código es la función de entrenamiento, donde se calcula la pérdida mediante `CrossEntropyLoss()` y se utiliza el optimizador `Adam` para modificar los parámetros del modelo durante el aprendizaje. Además, el entrenamiento se realiza durante 8 épocas y en cada una se registran la pérdida de entrenamiento, la precisión de validación (`val_acc`) y el ROC-AUC (`val_auc`). Esto permite observar no solamente si el modelo está aprendiendo, sino también cómo se comporta con datos que no utiliza directamente para entrenarse.

El código utilizado para este proceso es especialmente importante porque permite almacenar el historial de entrenamiento:

```python
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.Adam(model_scratch.parameters(), lr=1e-3)

epochs = 8
history_scratch = {"train_loss": [], "val_acc": [], "val_auc": []}
```

Posteriormente, estos valores son guardados en cada época:

```python
history_scratch["train_loss"].append(train_loss)
history_scratch["val_acc"].append(val_acc)
history_scratch["val_auc"].append(val_auc)
```

Gracias a esto es posible generar las curvas de entrenamiento y analizar visualmente la evolución del modelo. El notebook indica específicamente que estas curvas sirven para visualizar la pérdida y las métricas con el objetivo de detectar posibles problemas de sobreajuste.
**Figura 1. Pérdida de entrenamiento y métricas de validación de la CNN.**

<img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/3d73253c-ad33-46c2-a76f-b81f5df4624a" />


La primera imagen es importante porque permite interpretar cómo aprende la CNN a lo largo de las épocas. La gráfica de pérdida permite observar si el error del modelo disminuye durante el entrenamiento, mientras que las métricas de validación permiten comprobar si este aprendizaje también se refleja cuando el modelo trabaja con datos que no utilizó directamente para entrenarse.

En los resultados obtenidos se observa que la pérdida de entrenamiento disminuye progresivamente, pasando de `0.6943` en la primera época a `0.6718` en la octava. Al mismo tiempo, la precisión de validación aumenta desde `0.5102` hasta `0.6327`. Esto indica que durante estas épocas el modelo está aprendiendo progresivamente a distinguir las clases. Sin embargo, el ROC-AUC se mantiene en valores cercanos, por lo que todavía existe margen para mejorar la capacidad de discriminación del modelo.

Esta gráfica resulta particularmente útil para el proyecto porque, cuando se utilice un dataset específico de grietas, permitirá comprobar si la CNN realmente está aprendiendo características útiles de las imágenes o si solamente está memorizando los datos utilizados durante el entrenamiento. Por ello, observar simultáneamente la pérdida y las métricas de validación será importante para determinar si el modelo puede generalizar correctamente hacia fotografías nuevas.

Otro elemento importante del código corresponde a la evaluación del modelo. La función `evaluate()` obtiene las probabilidades y las predicciones realizadas por la CNN y posteriormente calcula métricas como `accuracy` y `ROC-AUC`. Además, las predicciones son comparadas con las etiquetas reales para generar la matriz de confusión.

**Figura 2. Matriz de confusión de la CNN.**

<img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/f507eb71-7fcc-438c-90ff-536e34aefb32" />


La segunda imagen permite observar con mayor detalle cómo se comportó el modelo al clasificar las muestras de prueba. A diferencia de la primera gráfica, que muestra la evolución del entrenamiento, la matriz de confusión permite identificar directamente cuántas muestras fueron clasificadas correctamente y cuántas fueron confundidas entre las dos clases.

En la matriz obtenida se registran `38` muestras de la clase 0 correctamente clasificadas y `44` muestras de la clase 1 correctamente clasificadas. También se observan `38` muestras de la clase 0 clasificadas como clase 1 y `29` muestras de la clase 1 clasificadas como clase 0. Estos resultados corresponden a una precisión global de prueba (`accuracy`) de `0.5503` y un ROC-AUC de `0.6191`.
La importancia de esta matriz para el proyecto está en que permite identificar los errores específicos del modelo. Esto será especialmente relevante cuando las clases representen diferentes niveles de severidad de las grietas, ya que no solamente será necesario conocer el porcentaje total de aciertos, sino también saber qué categorías son confundidas entre sí. De esta manera, la matriz puede ayudar a determinar qué clases necesitan más datos, una mejor preparación de las imágenes o modificaciones en la arquitectura y entrenamiento de la CNN.

Por otra parte, el archivo `.py` permite preparar el dataset para este tipo de procesamiento. Los datos son organizados por clases y divididos en conjuntos de entrenamiento, validación y prueba, utilizando una distribución de 70 %, 15 % y 15 %. También se realiza el procesamiento de las imágenes antes de introducirlas al modelo. Esta preparación es importante porque la calidad y organización del dataset influyen directamente en la capacidad de aprendizaje de la CNN.

En conjunto, el análisis de la CNN resulta relevante para el proyecto porque permite establecer un procedimiento completo: preparar las imágenes, entrenar el modelo, observar su evolución mediante las métricas, evaluar su comportamiento y analizar los errores mediante la matriz de confusión. Este mismo procedimiento podrá aplicarse posteriormente al dataset específico de fotografías de grietas para determinar si el modelo puede reconocer las diferentes categorías planteadas.

Además, este análisis podría complementarse posteriormente con información geológica y territorial de zonas del Perú que presenten condiciones de inestabilidad del suelo o riesgo de hundimiento. La CNN permitiría analizar la condición observable en la estructura mediante la fotografía, mientras que la información geológica podría aportar datos adicionales relacionados con el lugar donde se encuentra. Sin embargo, esta integración corresponde a una etapa posterior, ya que no se encuentra implementada directamente en el notebook analizado.

**Keras:**

Keras se presenta en el notebook como otra herramienta para la construcción y entrenamiento de redes neuronales. En este caso, se utiliza mediante el dataset IMDB para realizar una clasificación binaria de reseñas de películas, por lo que esta parte funciona como una demostración de cómo construir y entrenar un modelo de aprendizaje profundo.

Una de las partes importantes del código es la construcción y configuración del modelo mediante `Sequential`, `Dense`, `compile()` y `fit()`. El modelo utilizado cuenta con dos capas ocultas de 16 neuronas y una capa de salida de una neurona, utilizando `binary_crossentropy` como función de pérdida y `accuracy` como métrica.

Posteriormente, el modelo se entrena utilizando datos de entrenamiento y validación:

```python
modelb = model.fit(partial_x_train,
                   partial_y_train,
                   epochs=20,
                   batch_size=512,
                   validation_data=(x_val,y_val))
```

Este código resulta importante porque muestra cómo Keras permite realizar el entrenamiento y obtener simultáneamente métricas de entrenamiento y validación. En el ejemplo del notebook, la precisión de validación alcanza valores cercanos a `0.89` durante algunas épocas, mientras que la pérdida de validación también permite observar la evolución del modelo.

Para el proyecto, el principal aporte de esta sección de Keras es mostrar una forma simplificada de construir, configurar, entrenar y evaluar redes neuronales. Aunque actualmente la CNN utilizada para el análisis de imágenes se encuentra implementada mediante PyTorch, el conocimiento adquirido con Keras puede servir como referencia para comprender la estructura y el funcionamiento de otros modelos de aprendizaje profundo.

Por lo tanto, la parte de CNN es la que tiene una relación más directa con el análisis de las fotografías de grietas, mientras que Keras complementa el trabajo al mostrar otra metodología para desarrollar modelos de redes neuronales. Ambas partes permiten comprender diferentes componentes necesarios para posteriormente desarrollar un modelo adaptado al problema específico del proyecto.
