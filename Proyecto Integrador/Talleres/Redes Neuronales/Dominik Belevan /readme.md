# Taller 4: CNN, Keras y Perceptrón

## Introducción

En este taller estudié las **redes neuronales convolucionales (CNN)**, **Keras** y el **perceptrón**. Primero clasifiqué imágenes de residuos; después, reseñas de películas; y finalmente trabajé con compuertas lógicas. Estas actividades me permitieron conocer distintas aplicaciones de las redes neuronales y relacionarlas con **CrackScan**, el proyecto de nuestro equipo.

CrackScan busca apoyar la inspección preliminar de estructuras de concreto mediante la captura de imágenes, la detección de posibles grietas y el registro de cada inspección.

---

## 1. Redes neuronales convolucionales (CNN)

Una **CNN** es una red neuronal adecuada para analizar imágenes. Sus filtros identifican características visuales, como bordes, formas y texturas, que luego se utilizan para realizar una clasificación [1].

En el taller trabajé con **PyTorch** y el conjunto de imágenes **TrashNet** para diferenciar residuos de **vidrio** y **plástico** [2, 3].

![Ejemplos de imágenes de vidrio y plástico](https://github.com/user-attachments/assets/3ff90676-2c9d-4c97-a3d5-5a8da7d8b585)

*Figura 1. Ejemplos de imágenes del conjunto utilizado. Se observan objetos etiquetados como vidrio (`glass`) y plástico (`plastic`), las dos clases que debe distinguir la CNN.*

**Interpretación:**  
La figura muestra ejemplos de las dos clases utilizadas en el experimento: vidrio (`glass`) y plástico (`plastic`). En las imágenes se pueden observar diferentes formas, tamaños, bordes y texturas. Estas características visuales son las que la CNN debe aprender para poder distinguir una clase de la otra.

**¿Por qué es importante?**  
Esta figura es importante porque permite observar los datos de entrada que utiliza el modelo antes del entrenamiento. La CNN aprende directamente de las características visuales presentes en estas imágenes para posteriormente realizar la clasificación. También permite comprender que la calidad y variedad de los datos utilizados pueden influir en el comportamiento del modelo.

### 1.1 CNN entrenada desde cero

Primero se construyó una CNN con capas de convolución, activación ReLU, *pooling* y clasificación. Durante el entrenamiento, la pérdida fue disminuyendo, lo que indica que el modelo estaba ajustando sus parámetros.

![Pérdida de entrenamiento de la CNN](https://github.com/user-attachments/assets/64293380-5e23-43b0-98d8-80287ad1396a)

*Figura 2. La pérdida de entrenamiento de la CNN disminuye a lo largo de ocho épocas. Esto muestra que el modelo está aprendiendo con los datos de entrenamiento, aunque por sí solo no demuestra que clasifique bien imágenes nuevas.*

**Interpretación:**  
La gráfica muestra que la pérdida de entrenamiento disminuye progresivamente durante las ocho épocas. Esto significa que el error del modelo sobre los datos utilizados durante el entrenamiento se va reduciendo a medida que la red ajusta sus pesos y parámetros.

**¿Por qué es importante?**  
Esta figura es importante porque permite observar el proceso de aprendizaje de la CNN. Sin embargo, una disminución de la pérdida de entrenamiento no garantiza que el modelo funcione correctamente con imágenes nuevas. Por eso es necesario complementar este análisis con datos de validación y prueba para comprobar su capacidad de generalización.

Al final del entrenamiento se obtuvo **63,27 % de exactitud en validación**. Sin embargo, al evaluar la CNN desde cero con el **conjunto de prueba**, su exactitud fue de **55,03 %** y su ROC-AUC fue de **0,6191**. Es importante distinguir estos resultados porque corresponden a conjuntos de datos diferentes.

![Matriz de confusión de la CNN](https://github.com/user-attachments/assets/7b2b3cbf-b4df-41b8-901a-8e7e5263ca22)

*Figura 3. Matriz de confusión de la CNN desde cero en la prueba final. La diagonal muestra las clasificaciones correctas y las otras casillas muestran los errores. El modelo acertó 82 de 149 imágenes.*

**Interpretación:**  
La matriz de confusión compara las clases reales de las imágenes con las clases predichas por el modelo. Los valores ubicados en la diagonal representan las clasificaciones correctas, mientras que los valores fuera de la diagonal representan los errores de clasificación entre vidrio y plástico.

En total, el modelo clasificó correctamente **82 de 149 imágenes** del conjunto de prueba.

**¿Por qué es importante?**  
Esta figura es importante porque permite conocer cómo se producen los errores del modelo y no solamente observar una única medida de exactitud. La matriz permite identificar si el modelo confunde imágenes de vidrio con plástico o imágenes de plástico con vidrio. De esta manera, se puede analizar con mayor detalle el comportamiento de la CNN.

### 1.2 Data augmentation y transfer learning

Después se aplicó **data augmentation**, realizando pequeñas transformaciones a las imágenes para variar los ejemplos de entrenamiento. En la prueba final, esta versión alcanzó **56,38 % de exactitud**.

También se utilizó **transfer learning** con **ResNet18**. Esta técnica aprovecha características que una red ya aprendió con otras imágenes y las adapta a un problema nuevo [4]. En la prueba final, el modelo con transfer learning obtuvo **86,58 % de exactitud** y **0,9562 de ROC-AUC**. En este ejercicio, su desempeño fue superior al de la CNN entrenada desde cero.

**Interpretación:**  
El data augmentation genera variaciones de las imágenes originales mediante pequeñas transformaciones, como rotaciones o desplazamientos. Esto permite que el modelo tenga ejemplos ligeramente diferentes durante el entrenamiento.

Por otro lado, el transfer learning utiliza un modelo previamente entrenado, en este caso ResNet18, y aprovecha las características visuales que ya aprendió para adaptarlas al problema de clasificación de vidrio y plástico.

**¿Por qué es importante?**  
Esta comparación es importante porque permite analizar diferentes estrategias para entrenar una CNN. El resultado obtenido con ResNet18 muestra que aprovechar características aprendidas previamente puede ser útil cuando se busca mejorar el desempeño del modelo. Esta estrategia también puede ser relevante para CrackScan si inicialmente se dispone de una cantidad limitada de imágenes de grietas.

### 1.3 Grad-CAM

Por último, se utilizó **Grad-CAM** para visualizar las regiones de la imagen que influyeron en una predicción [5].

![Imagen, mapa Grad-CAM y superposición](https://github.com/user-attachments/assets/52e4e47a-0600-4174-b420-bf86ceb09768)

*Figura 4. A la izquierda aparece la imagen analizada; en el centro, el mapa Grad-CAM; y a la derecha, ambos superpuestos. Las zonas más destacadas indican regiones que influyeron más en la predicción.*

**Interpretación:**  
La figura presenta tres elementos: la imagen original, el mapa de activación generado mediante Grad-CAM y la superposición del mapa sobre la imagen. Las regiones más resaltadas corresponden a las zonas que tuvieron mayor influencia en la predicción realizada por la CNN.

**¿Por qué es importante?**  
Grad-CAM es importante porque permite interpretar visualmente la decisión del modelo. No solamente se obtiene la clase predicha, sino que también se puede observar qué partes de la imagen tuvieron mayor influencia en esa decisión.

Esto es especialmente importante para **CrackScan**, ya que permitiría comprobar si el modelo está concentrando su atención en una posible grieta y no en elementos que podrían generar errores, como sombras, manchas, juntas o irregularidades del concreto.

**Lo que aprendí:** para valorar una CNN hay que revisar sus resultados con imágenes que no utilizó para entrenarse. También es útil examinar dónde concentra su atención.

---

## 2. Keras

**Keras** facilita la construcción y el entrenamiento de redes neuronales [6]. En esta parte del taller trabajé con **IMDB**, un conjunto de reseñas de películas clasificadas como positivas o negativas [7]. A diferencia del ejercicio anterior, aquí se clasificó **texto**, no imágenes.

Las reseñas se transformaron en datos numéricos y se entrenó una red con **dos capas ocultas de 16 neuronas** y una salida para clasificación binaria. El modelo obtuvo aproximadamente **86,1 % de exactitud en el conjunto de prueba**.

### 2.1 Sobreajuste

Las curvas mostraron **sobreajuste**: la pérdida de entrenamiento continuó disminuyendo, mientras que la pérdida de validación comenzó a aumentar. Esto indica que seguir entrenando no siempre mejora el resultado con datos nuevos.

![Pérdidas del modelo original en Keras](https://github.com/user-attachments/assets/f22d4608-6f8a-4e30-b097-409ce12e7973)

*Figura 5. La pérdida de entrenamiento baja continuamente, pero la de validación empieza a subir después de las primeras épocas. Esa separación es una señal de sobreajuste.*

**Interpretación:**  
En la gráfica se observa que la pérdida de entrenamiento continúa disminuyendo, mientras que después de determinadas épocas la pérdida de validación comienza a aumentar. Esto significa que el modelo sigue mejorando sobre los datos que utilizó para aprender, pero comienza a comportarse peor con datos que no utilizó directamente durante el entrenamiento.

Este comportamiento corresponde a un problema de **sobreajuste (overfitting)**.

**¿Por qué es importante?**  
Esta figura es importante porque demuestra que una menor pérdida de entrenamiento no significa necesariamente que el modelo esté mejorando su capacidad de generalización. Si el modelo aprende demasiado los datos de entrenamiento, puede perder capacidad para clasificar correctamente datos nuevos.

Por ello, es necesario analizar simultáneamente las curvas de entrenamiento y validación.

### 2.2 Pruebas para reducir el sobreajuste

Primero se comparó el modelo original con **uno más pequeño**, que tiene menos neuronas. La idea fue observar si reducir su capacidad cambiaba el comportamiento de la pérdida de validación.

![Comparación del modelo pequeño con el original](https://github.com/user-attachments/assets/a65cd8a2-60fd-4d16-9b02-a8aefc45f53b)

*Figura 6. Comparación de la pérdida de validación del modelo pequeño y el original. Permite observar cómo el tamaño de la red influye en su comportamiento con datos que no utilizó para entrenarse.*

**Interpretación:**  
La figura compara el comportamiento de la pérdida de validación del modelo original con el modelo de menor tamaño. Al reducir la cantidad de neuronas también se reduce la capacidad de la red para memorizar los datos de entrenamiento.

El modelo más pequeño presenta un comportamiento diferente en la pérdida de validación y el aumento del error aparece de manera menos pronunciada.

**¿Por qué es importante?**  
Esta comparación es importante porque muestra que aumentar el tamaño de una red no siempre significa obtener un mejor modelo. Reducir la capacidad puede ayudar a disminuir el sobreajuste y favorecer que la red aprenda características más generales.

Luego se probó la **regularización**, una técnica que penaliza ciertos valores de los pesos para reducir el sobreajuste.

![Resultados con regularización](https://github.com/user-attachments/assets/815d1b6d-4977-4e4b-92e3-5a62cca4f002)

*Figura 7. Se comparan las pérdidas de entrenamiento y validación del modelo con regularización, junto con la pérdida de validación del modelo original.*

**Interpretación:**  
La figura muestra el comportamiento de las pérdidas del modelo después de aplicar regularización y permite compararlo con el modelo original. La regularización modifica el proceso de aprendizaje al penalizar determinados valores de los pesos de la red.

**¿Por qué es importante?**  
Esta figura es importante porque permite observar otra estrategia para disminuir el sobreajuste. La regularización busca evitar que el modelo dependa excesivamente de determinados pesos y favorecer un aprendizaje que pueda generalizar mejor a datos nuevos.

Por último, se probó **dropout de 50 %**, que desactiva aleatoriamente parte de las neuronas durante el entrenamiento.

![Resultados con dropout](https://github.com/user-attachments/assets/6898097c-d787-4b58-8dec-af18bab9f884)

*Figura 8. Comparación de la pérdida de validación del modelo con dropout y el original. Esta gráfica permite estudiar si dropout retrasa o reduce el sobreajuste.*

**Interpretación:**  
La gráfica compara la pérdida de validación del modelo original con la del modelo que utiliza un dropout del 50 %. Durante el entrenamiento, dropout desactiva aleatoriamente una parte de las neuronas, haciendo que la red no dependa demasiado de un grupo específico de neuronas.

**¿Por qué es importante?**  
Esta figura es importante porque permite estudiar otra técnica utilizada para reducir el sobreajuste. Al desactivar aleatoriamente parte de las neuronas durante el entrenamiento, el modelo busca aprender diferentes combinaciones de características y mejorar su capacidad de generalización.

También se realizó una predicción de ejemplo: para una reseña, el modelo asignó aproximadamente **99,4 % de probabilidad** a la clase positiva. Ese porcentaje corresponde **solo a esa reseña**; no es la exactitud general del modelo.

**Lo que aprendí:** una red puede obtener buenos resultados y aun así presentar sobreajuste. Por eso, es necesario comparar entrenamiento y validación antes de elegir cómo utilizarla.

---

### 3. Perceptrón

El **perceptrón** es un modelo sencillo que permite comprender la base de una red neuronal. Combina entradas y pesos, añade un sesgo y aplica una función de activación [8]:

$$
y=f\left(\sum_{i=1}^{n}w_i x_i+b\right)
$$

Donde $x_i$ representa las entradas, $w_i$ los pesos, $b$ el sesgo y $f$ la función de activación.

En el taller se probaron las funciones de activación **escalón** y **tanh**, además de las compuertas **AND**, **OR** y **XOR**.

| Compuerta | ¿Cuándo produce una salida de 1? |
|---|---|
| AND | Cuando ambas entradas son 1. |
| OR | Cuando al menos una entrada es 1. |
| XOR | Cuando las entradas son diferentes. |

![Fronteras de decisión de AND y OR](https://github.com/user-attachments/assets/27a772e8-e140-4faa-a8f0-2f20434f0a25)

*Figura 9. Las rectas muestran que las salidas de AND y OR pueden separarse en dos grupos. Por eso, un perceptrón puede representar estas compuertas.*

**Interpretación:**  
La figura representa las fronteras de decisión de las compuertas AND y OR. En ambos casos, las diferentes clases pueden separarse mediante una línea recta.

En AND, solamente la combinación `(1,1)` produce una salida de 1. En OR, las combinaciones `(0,1)`, `(1,0)` y `(1,1)` producen una salida de 1.

**¿Por qué es importante?**  
Esta figura es importante porque permite visualizar el concepto de **separabilidad lineal**. AND y OR pueden resolverse utilizando un único perceptrón porque existe una frontera lineal que permite separar correctamente las diferentes clases.

![Representación de XOR](https://github.com/user-attachments/assets/6481d994-48f2-42a4-8b84-72664c1e7713)

*Figura 10. En XOR, los puntos correspondientes a la salida 0 son (0,0) y (1,1), mientras que los puntos con salida 1 son (0,1) y (1,0). Los puntos de una misma clase quedan ubicados en esquinas opuestas del plano, por lo que una sola recta no puede separarlos correctamente. Debido a ello, un único perceptrón no puede resolver este problema.*

**Interpretación:**  
En XOR, las entradas `(0,0)` y `(1,1)` producen una salida de 0, mientras que `(0,1)` y `(1,0)` producen una salida de 1. Los puntos pertenecientes a una misma clase se encuentran en esquinas opuestas del plano.

Por esta distribución, no existe una única línea recta capaz de separar correctamente las dos clases.

**¿Por qué es importante?**  
Esta figura es importante porque muestra una limitación fundamental del perceptrón individual. XOR no es un problema linealmente separable, por lo que un único perceptrón no puede resolverlo correctamente.

Este ejemplo permite comprender por qué las redes neuronales utilizan múltiples neuronas y capas para resolver problemas más complejos.

**Lo que aprendí:** AND y OR son problemas linealmente separables. XOR muestra una limitación del perceptrón individual y ayuda a entender por qué algunas redes necesitan varias capas.

---

## 4. Aplicación de lo aprendido a CrackScan

**CrackScan** es una propuesta para apoyar la **inspección preliminar de estructuras de concreto**. Su objetivo es capturar imágenes, detectar posibles grietas, registrar información sobre ellas y asociar cada inspección con una ubicación geográfica.

De los temas estudiados, la **CNN** es la más relacionada con el análisis visual de CrackScan. Un posible primer objetivo sería clasificar fotografías de concreto en dos grupos: **con posibles grietas** y **sin grietas**. Para desarrollar esa función se necesitarían fotografías propias, etiquetas confiables y una evaluación con imágenes que el modelo no haya visto durante el entrenamiento.

El **transfer learning** podría ser útil si al inicio se dispone de pocas imágenes etiquetadas. **Grad-CAM** podría ayudar a revisar si la red se fija en la grieta y no en sombras, manchas o juntas del concreto.

Detectar una grieta y **medir su ancho o longitud real** son tareas distintas. Para estimar dimensiones a partir de fotografías haría falta una referencia de escala o una calibración adecuada de la cámara. Asimismo, las coordenadas GPS servirían para registrar dónde se realizó la inspección.

Keras o PyTorch podrían utilizarse para construir el modelo de imágenes. El perceptrón aporta los conceptos básicos para comprender cómo aprende una red, aunque por sí solo no es suficiente para realizar todo el análisis visual planteado para CrackScan.

**Los resultados de TrashNet e IMDB pertenecen a los ejercicios del taller:** todavía no indican qué exactitud obtendría CrackScan al analizar grietas reales. La propuesta busca apoyar el registro y la inspección preliminar; la evaluación técnica de una estructura corresponde a un especialista.

---

## Conclusiones

El taller me permitió comprender que cada método cumple una función diferente. Las **CNN** aprenden características de imágenes; **Keras** facilita construir modelos y comparar sus resultados; y el **perceptrón** explica conceptos como pesos, sesgo, activación y separabilidad lineal.

La comparación entre la CNN desde cero y el modelo con **transfer learning** mostró la importancia de probar distintas estrategias y evaluar los resultados con datos de prueba. Las gráficas de **Keras** mostraron por qué también se debe vigilar el sobreajuste.

En **CrackScan**, lo aprendido podría servir como base para detectar posibles grietas en fotografías. Antes de afirmar que el sistema funciona, será necesario reunir imágenes de concreto, entrenar el modelo y comprobar su desempeño en condiciones reales.

## Referencias

[1] I. Goodfellow, Y. Bengio y A. Courville, *Deep Learning*. MIT Press, 2016.

[2] G. Thung y M. Yang, *TrashNet: Dataset of Images of Trash*, 2016.

[3] PyTorch, *PyTorch Documentation*. https://pytorch.org/docs/stable/

[4] K. He et al., “Deep Residual Learning for Image Recognition”, *CVPR*, 2016.

[5] R. R. Selvaraju et al., “Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization”, *ICCV*, 2017.

[6] Keras, *Keras Documentation*. https://keras.io/

[7] Keras, *IMDB Movie Reviews Sentiment Classification Dataset*. https://keras.io/api/datasets/imdb/

[8] F. Rosenblatt, “The Perceptron: A Probabilistic Model for Information Storage and Organization in the Brain”, *Psychological Review*, vol. 65, n.º 6, pp. 386–408, 1958.
