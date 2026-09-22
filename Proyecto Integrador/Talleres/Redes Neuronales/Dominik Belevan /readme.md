# Taller 4: CNN, Keras y Perceptrón

## Introducción

En este taller estudié tres temas relacionados con las redes neuronales: las **redes neuronales convolucionales (CNN)**, **Keras** y el **perceptrón**. Cada uno me ayudó a comprender una parte diferente del aprendizaje automático. Las CNN permiten analizar imágenes, Keras facilita la construcción de modelos y el perceptrón explica los fundamentos de una neurona artificial.

Durante el taller clasifiqué imágenes de residuos, trabajé con reseñas de películas y probé compuertas lógicas. Finalmente, relacioné estos conocimientos con **CrackScan**, el proyecto de nuestro equipo para apoyar la inspección preliminar de estructuras de concreto mediante imágenes y el registro de grietas.

---

## 1. Redes neuronales convolucionales (CNN)

Una **CNN** es una red neuronal especialmente útil para analizar imágenes. Utiliza filtros que recorren distintas zonas de la imagen para identificar características como bordes, formas y texturas. Luego combina esas características para realizar una clasificación [1].

Sus componentes principales son:

- **Convolución:** aplica filtros para extraer características de la imagen.
- **ReLU:** permite que la red aprenda relaciones más complejas.
- **Pooling:** reduce el tamaño de los mapas de características y conserva información relevante.
- **Capas densas:** utilizan las características extraídas para generar la clasificación final.

![Arquitectura de una CNN](https://github.com/user-attachments/assets/3ff90676-2c9d-4c97-a3d5-5a8da7d8b585)

*Figura 1. Representación del procesamiento de una imagen mediante una CNN. Las primeras capas extraen características visuales y las últimas las utilizan para obtener una predicción.*

### 1.1 Clasificación de imágenes con TrashNet

En el taller utilicé **PyTorch** y el conjunto de imágenes **TrashNet** para clasificar residuos de **vidrio y plástico** [2, 3]. Primero construí una CNN desde cero y evalué sus resultados mediante métricas como exactitud (*accuracy*) y ROC-AUC.

El modelo alcanzó aproximadamente **63,27 % de exactitud** y un **ROC-AUC cercano a 0,68**. Esto muestra que logró reconocer algunas diferencias entre las imágenes, aunque todavía tenía margen de mejora.

![Resultados del entrenamiento de la CNN](https://github.com/user-attachments/assets/64293380-5e23-43b0-98d8-80287ad1396a)

*Figura 2. Resultados utilizados para observar cómo evolucionó el entrenamiento de la CNN y evaluar su capacidad de clasificación.*

### 1.2 Técnicas para mejorar y comprender el modelo

Después se aplicó **data augmentation**, que consiste en hacer pequeñas transformaciones a las imágenes de entrenamiento para aumentar su variedad.

También se probó **transfer learning** con **ResNet18**. Esta técnica aprovecha características que un modelo ya aprendió con otras imágenes. Posteriormente se realizó *fine-tuning* para adaptar parte del modelo al problema de clasificación entre vidrio y plástico [4].

Finalmente se trabajó con **Grad-CAM**, una técnica que permite visualizar qué zonas de una imagen influyeron en la predicción de una CNN [5].

![Visualización del análisis de una imagen](https://github.com/user-attachments/assets/7b2b3cbf-b4df-41b8-901a-8e7e5263ca22)

*Figura 3. La visualización ayuda a revisar el análisis de una imagen y a comprender mejor en qué información puede apoyarse la predicción.*

**Lo que aprendí:** entrenar una CNN no consiste solamente en obtener un porcentaje de aciertos. También es necesario evaluar el modelo con imágenes distintas de las utilizadas para entrenarlo y revisar si toma decisiones basadas en características relevantes.

---

## 2. Keras

**Keras** facilita la construcción y el entrenamiento de redes neuronales [6]. En esta parte del taller trabajé con el conjunto **IMDB**, que contiene reseñas de películas clasificadas como positivas o negativas [7]. Por lo tanto, este ejercicio fue de **clasificación de texto**, no de imágenes.

Primero se transformaron las reseñas en una representación numérica que el modelo pudiera procesar. Después se construyó una red con **dos capas ocultas de 16 neuronas** y una capa de salida para la clasificación binaria.

### 2.1 Resultados y sobreajuste

El modelo obtuvo aproximadamente **86,1 % de exactitud**. Sin embargo, las gráficas mostraron **sobreajuste** (*overfitting*): el modelo seguía mejorando con los datos de entrenamiento, pero dejaba de mejorar con los datos de validación.

![Comparación del entrenamiento y la validación](https://github.com/user-attachments/assets/52e4e47a-0600-4174-b420-bf86ceb09768)

*Figura 4. La comparación de las curvas de entrenamiento y validación permite identificar si el modelo está aprendiendo a trabajar con datos nuevos o si comienza a presentar sobreajuste.*

### 2.2 Comparación de modelos

Para estudiar el sobreajuste se probaron distintas configuraciones, entre ellas un modelo más pequeño, **regularización** y **dropout**.

![Primera gráfica de evaluación con Keras](https://github.com/user-attachments/assets/f22d4608-6f8a-4e30-b097-409ce12e7973)

*Figura 5. Esta gráfica permite evaluar el comportamiento de una de las configuraciones entrenadas con Keras.*

![Segunda gráfica de evaluación con Keras](https://github.com/user-attachments/assets/a65cd8a2-60fd-4d16-9b02-a8aefc45f53b)

*Figura 6. Comparar esta gráfica con la anterior ayuda a observar cómo los cambios en el modelo afectan su aprendizaje.*

La **regularización** busca reducir la dependencia del modelo respecto de ciertos pesos. **Dropout**, en cambio, desactiva aleatoriamente una parte de las neuronas mientras se entrena. En el taller se utilizó un dropout de **50 %**.

![Tercera gráfica de evaluación con Keras](https://github.com/user-attachments/assets/815d1b6d-4977-4e4b-92e3-5a62cca4f002)

*Figura 7. Esta gráfica forma parte de la comparación de los resultados obtenidos al probar estrategias contra el sobreajuste.*

![Cuarta gráfica de evaluación con Keras](https://github.com/user-attachments/assets/6898097c-d787-4b58-8dec-af18bab9f884)

*Figura 8. La revisión de las curvas permite valorar si una configuración mejora el comportamiento del modelo con datos de validación.*

Finalmente se realizó una predicción de ejemplo. Para una reseña, el modelo obtuvo aproximadamente **99,4 % de probabilidad** de pertenecer a la clase positiva. **Este valor corresponde a esa reseña específica** y no significa que la exactitud general del modelo sea 99,4 %.

**Lo que aprendí:** una buena exactitud no es suficiente para evaluar una red neuronal. También hay que observar el comportamiento de la validación y comprobar si el modelo puede trabajar con datos nuevos.

---

## 3. Perceptrón

El **perceptrón** es uno de los modelos más sencillos de una red neuronal. Recibe entradas, las combina con pesos, añade un sesgo y aplica una función de activación para producir una salida [8]:

$$
y=f\left(\sum_{i=1}^{n}w_i x_i+b\right)
$$

Donde $x_i$ representa las entradas, $w_i$ los pesos, $b$ el sesgo y $f$ la función de activación.

En el taller se probaron funciones de activación como **escalón** y **tanh**, además de las compuertas lógicas **AND**, **OR** y **XOR**:

| Compuerta | ¿Cuándo produce una salida de 1? |
|---|---|
| AND | Cuando ambas entradas son 1. |
| OR | Cuando al menos una entrada es 1. |
| XOR | Cuando las entradas son diferentes. |

Un solo perceptrón puede representar **AND** y **OR** porque sus resultados se pueden separar mediante una recta. **XOR no puede resolverse con un solo perceptrón**, ya que sus resultados no son linealmente separables. Para representar relaciones más complejas se necesitan varias neuronas organizadas en capas.

![Representación de las compuertas lógicas](https://github.com/user-attachments/assets/aa09b6d1-687a-495c-ac4c-8b3758c1a591)

*Figura 9. La representación permite estudiar la separación de los resultados de las compuertas lógicas y comprender la limitación de un perceptrón frente a XOR.*

**Lo que aprendí:** el perceptrón me ayudó a comprender conceptos básicos como entradas, pesos, sesgo y activación. El caso XOR muestra por qué las redes con varias capas pueden resolver problemas que una sola neurona no puede.

---

## 4. Aplicación de lo aprendido a CrackScan

**CrackScan** es una propuesta tecnológica de nuestro equipo para apoyar la **inspección preliminar de estructuras de concreto**. El sistema busca capturar imágenes, detectar posibles grietas, registrar sus características aproximadas y asociar cada inspección con una ubicación geográfica.

De los temas estudiados, las **CNN** son las más relacionadas con el análisis visual de CrackScan. Una CNN podría aprender a distinguir imágenes de concreto **con grietas** y **sin grietas**. Más adelante, el análisis de imágenes también podría ayudar a ubicar la zona afectada dentro de la fotografía.

### 4.1 Posible proceso de análisis

1. **Captura:** la cámara obtiene una fotografía de la superficie de concreto.
2. **Preparación:** la imagen se ajusta al tamaño y formato necesarios para el modelo.
3. **Detección:** el modelo estima si en la imagen hay una posible grieta.
4. **Localización:** se identifica la zona de la imagen donde aparece.
5. **Registro:** se guardan la imagen, el resultado y las coordenadas de la inspección.

Para desarrollar esta propuesta sería necesario reunir fotografías de concreto en distintas condiciones: superficies con y sin grietas, diferentes iluminaciones, texturas y distancias de captura. Los datos deberían etiquetarse y dividirse para entrenar y evaluar el modelo.

El **transfer learning** podría ser útil si inicialmente no se dispone de muchas imágenes etiquetadas. **Grad-CAM** serviría como apoyo para revisar si una CNN se fija en la grieta y no en sombras, juntas, manchas u otros elementos que podrían confundirse con ella.

La **detección de una grieta** y la **estimación de su ancho o longitud** son tareas diferentes. Para estimar dimensiones reales a partir de una fotografía harían falta una referencia de escala o una calibración adecuada de la cámara. Por eso, no sería correcto afirmar que una CNN por sí sola puede medir esas dimensiones con precisión.

**Keras** podría utilizarse para construir y entrenar un modelo de imágenes, mientras que el ejercicio del **perceptrón** aporta los conceptos básicos para comprender cómo aprende una red neuronal.

### 4.2 Alcance de la propuesta

CrackScan busca **apoyar la inspección preliminar y organizar los registros de campo**. Una predicción automática puede señalar una zona que requiere atención, pero el estado de seguridad de una estructura debe ser evaluado por un especialista. Asimismo, los resultados obtenidos con TrashNet o IMDB **no demuestran todavía el desempeño de CrackScan**, porque corresponden a problemas y conjuntos de datos diferentes.

---

## 5. Conclusiones

El taller me permitió comprender que los modelos y herramientas de redes neuronales se utilizan de acuerdo con el problema que se quiere resolver:

- Las **CNN** permiten aprender características visuales y son las más relacionadas con el análisis de fotografías propuesto para CrackScan.
- **Keras** facilita la construcción de modelos y el ejercicio con IMDB permitió reconocer el sobreajuste.
- El **perceptrón** explica cómo intervienen las entradas, los pesos, el sesgo y las funciones de activación en una red neuronal.

La relación con **CrackScan** es una **aplicación propuesta**, no un resultado ya validado. El siguiente paso sería reunir fotografías propias de estructuras de concreto, definir cómo se etiquetarán las grietas y evaluar el desempeño del sistema con imágenes tomadas en condiciones reales. Así, el análisis automático podría convertirse en una herramienta útil para apoyar el registro de inspecciones preliminares.

## Referencias

[1] I. Goodfellow, Y. Bengio y A. Courville, *Deep Learning*. MIT Press, 2016.

[2] G. Thung y M. Yang, *TrashNet: Dataset of Images of Trash*, 2016.

[3] PyTorch, *PyTorch Documentation*. https://pytorch.org/docs/stable/

[4] K. He et al., “Deep Residual Learning for Image Recognition”, *CVPR*, 2016.

[5] R. R. Selvaraju et al., “Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization”, *ICCV*, 2017.

[6] Keras, *Keras Documentation*. https://keras.io/

[7] Keras, *IMDB Movie Reviews Sentiment Classification Dataset*. https://keras.io/api/datasets/imdb/

[8] F. Rosenblatt, “The Perceptron: A Probabilistic Model for Information Storage and Organization in the Brain”, *Psychological Review*, vol. 65, n.º 6, pp. 386–408, 1958.
