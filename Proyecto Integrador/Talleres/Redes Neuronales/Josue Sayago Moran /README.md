# Análisis Práctico: Detección de Grietas en Estructuras de Concreto mediante CNNs

Tras comprender los fundamentos teóricos de las Redes Neuronales Convolucionales (CNN) —incluyendo el uso de filtros para extraer características visuales (Conv2D) es factible sustentar este modelo de análisis como uno de utilidad para el proyecto que se planea trabajar. Entonces, este modelo computacional sería capaz de analizar fotografías de superficies de concreto para diagnosticar, de manera automática, la presencia de grietas o fallas estructurales. 

Es importante mencionar que, a comparación de los otros modelos (Keras y Perceptrón), CNN es, para el procesamiento de imágenes, el método más óptimo ya que logra extraer patrones, texturas y formas (como los bordes oscuros de una fisura) de manera autónoma. Si bien para entrenar a las redes Neuronales Convolucionales (CNN) con muchas de imágenes se requiere una potencia de cálculo masiva ello es solucionable al ejecutar una GPU de forma que el modelo procesara en menor tiempo su entrenamiento.

<img width="302" height="246" alt="image" src="https://github.com/user-attachments/assets/98a787c4-1637-433b-a7ab-53518d2223a9" />

En primer lugar, se importan las bibliotecas fundamentales. TensorFlow y Keras nos proporcionarán las funciones matemáticas para construir la Red Neuronal Convolucional (CNN), mientras que Matplotlib nos permitirá visualizar las imágenes de concreto y las gráficas de aprendizaje del modelo.

<img width="765" height="212" alt="image" src="https://github.com/user-attachments/assets/4f876556-61bd-41c5-9a22-62ccb65f2e11" />

Posteriormente, tras realizar la carga y el preprocesamiento del conjunto de imágenes de concreto, se procedió a construir y entrenar la arquitectura convolucional.Tras realizar la carga y el preprocesamiento del conjunto de imágenes de concreto, se procedió a construir y entrenar la arquitectura convolucional. Para evaluar la efectividad del aprendizaje durante la etapa de entrenamiento, se monitoreó el comportamiento de la función de pérdida (*loss*), la cual mide el margen de error del modelo en cada iteración:



<img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/ff25e95a-e298-4e98-ad2f-9319e94bf0d1" />


### Interpretación de la Gráfica de Pérdida y Sustentación del Modelo

La gráfica muestra la curva de pérdida de entrenamiento de la CNN construida desde cero a lo largo de 8 épocas (registradas de la 0 a la 7). En el eje vertical (*Loss*), se aprecia un descenso constante e intermitente del error, partiendo desde un valor cercano a 0.694 en la primera época y reduciéndose progresivamente hasta alcanzar aproximadamente 0.672[cite: 4]. Esta tendencia decreciente confirma que el modelo está ajustando sus pesos de forma efectiva y reduciendo su incertidumbre al clasificar las superficies.

El rendimiento mostrado en esta gráfica permite sustentar técnicamente por qué la elección de una Red Neuronal Convolucional (CNN) es superior a arquitecturas tradicionales como el Perceptrón Multicapa o los algoritmos basados en Métodos de Kernel:

1. **Preservación de la información espacial (frente al Perceptrón):** Un Perceptrón clásico exige aplanar las imágenes en un vector unidimensional de datos, lo que destruye por completo las relaciones geométricas entre píxeles adyacentes. Las grietas en el concreto son patrones continuos y lineales que dependen de su entorno espacial; la CNN preserva esta estructura bidimensional mediante las capas de convolución (`Conv2D`), analizando el contexto de cada región de la imagen.
2. **Extracción autónoma de características (frente a Métodos de Kernel):** Los métodos tradicionales basados en Kernel (como las Máquinas de Vectores de Soporte o SVM) dependen de una ingeniería de características manual, donde el usuario debe diseñar previamente qué filtros aplicar para resaltar bordes. En contraste, el descenso de la curva de pérdida demuestra cómo la CNN aprende y optimiza de forma totalmente autónoma sus propios núcleos o filtros internos para aislar fisuras y texturas del concreto.
3. **Invarianza a la traslación:** Gracias a la inclusión de capas de reducción (`MaxPooling`), la red es capaz de reconocer una falla en el concreto sin importar la posición exacta en la que aparezca dentro de la fotografía (centro, esquina o bordes), capacidad de la que carecen las redes densas tradicionales.

4. 

### Interpretación de la Gráfica de Pérdida y Sustentación del Modelo

La gráfica muestra la curva de pérdida de entrenamiento de la CNN construida desde cero a lo largo de 8 épocas (registradas de la 0 a la 7). En el eje vertical (*Loss*), se aprecia un descenso constante e intermitente del error, partiendo desde un valor cercano a 0.694 en la primera época y reduciéndose progresivamente hasta alcanzar aproximadamente 0.672[cite: 4]. Esta tendencia decreciente confirma que el modelo está ajustando sus pesos de forma efectiva y reduciendo su incertidumbre al clasificar las superficies.

El rendimiento mostrado en esta gráfica permite sustentar técnicamente por qué la elección de una Red Neuronal Convolucional (CNN) es superior a arquitecturas tradicionales como el Perceptrón Multicapa o los algoritmos basados en Métodos de Kernel:

1. **Preservación de la información espacial (frente al Perceptrón):** Un Perceptrón clásico exige aplanar las imágenes en un vector unidimensional de datos, lo que destruye por completo las relaciones geométricas entre píxeles adyacentes. Las grietas en el concreto son patrones continuos y lineales que dependen de su entorno espacial; la CNN preserva esta estructura bidimensional mediante las capas de convolución (`Conv2D`), analizando el contexto de cada región de la imagen.
2. **Extracción autónoma de características (frente a Métodos de Kernel):** Los métodos tradicionales basados en Kernel (como las Máquinas de Vectores de Soporte o SVM) dependen de una ingeniería de características manual, donde el usuario debe diseñar previamente qué filtros aplicar para resaltar bordes. En contraste, el descenso de la curva de pérdida demuestra cómo la CNN aprende y optimiza de forma totalmente autónoma sus propios núcleos o filtros internos para aislar fisuras y texturas del concreto.
3. **Invarianza a la traslación:** Gracias a la inclusión de capas de reducción (`MaxPooling`), la red es capaz de reconocer una falla en el concreto sin importar la posición exacta en la que aparezca dentro de la fotografía (centro, esquina o bordes), capacidad de la que carecen las redes densas tradicionales.

<img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/a35269d4-1978-43ac-b3ad-6005d3712978" />

En esta primera etapa, se importan las bibliotecas fundamentales. TensorFlow y Keras nos proporcionarán las funciones matemáticas para construir la Red Neuronal Convolucional (CNN), mientras que Matplotlib nos permitirá visualizar las imágenes de concreto y las gráficas de aprendizaje del modelo.

<img width="1748" height="603" alt="image" src="https://github.com/user-attachments/assets/397a4cd8-03fa-4b0d-9985-2dc56a104b01" />
Las redes neuronales no entienden imágenes en bruto. En esta celda, estandarizamos todas las fotografías de las estructuras de concreto a una resolución fija (ej. 150x150 píxeles) y normalizamos sus valores para facilitar que la red detecte las sombras y bordes característicos de las grietas.

<img width="1002" height="651" alt="image" src="https://github.com/user-attachments/assets/02e26e60-a555-4f26-899d-7e4ef409cd24" />
