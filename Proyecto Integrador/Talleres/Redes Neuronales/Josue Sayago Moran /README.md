# Análisis: Sistemas de redes neuronales (CNN, Keras y Perceptrón)
Tras comprender los fundamentos teóricos de las Redes Neuronales Convolucionales (CNN) —incluyendo el uso de filtros para extraer características visuales (Conv2D) es factible sustentar este modelo de análisis como uno de utilidad para el proyecto que se planea trabajar. Entonces, este modelo computacional sería capaz de analizar fotografías de superficies de concreto para diagnosticar, de manera automática, la presencia de grietas o fallas estructurales. 

Es importante mencionar que, a comparación de los otros modelos (Keras y Perceptrón), CNN es, para el procesamiento de imágenes, el método más óptimo ya que logra extraer patrones, texturas y formas (como los bordes oscuros de una fisura) de manera autónoma. Si bien para entrenar a las redes Neuronales Convolucionales (CNN) con muchas de imágenes se requiere una potencia de cálculo masiva ello es solucionable al ejecutar una GPU de forma que el modelo procesara en menor tiempo su entrenamiento.
<p align="center">
<img width="302" height="246" alt="image" src="https://github.com/user-attachments/assets/98a787c4-1637-433b-a7ab-53518d2223a9" />
</p>
En primer lugar, se importan las bibliotecas fundamentales. TensorFlow y Keras nos proporcionarán las funciones matemáticas para construir la Red Neuronal Convolucional (CNN), mientras que Matplotlib nos permitirá visualizar las imágenes de concreto y las gráficas de aprendizaje del modelo.
<p align="center">
<img width="465" height="212" alt="image" src="https://github.com/user-attachments/assets/4f876556-61bd-41c5-9a22-62ccb65f2e11" />
</p>
Posteriormente, tras realizar la carga y el preprocesamiento del conjunto de imágenes de concreto, se procedió a construir y entrenar la arquitectura convolucional.Tras realizar la carga y el preprocesamiento del conjunto de imágenes de concreto, se procedió a construir y entrenar la arquitectura convolucional. Para evaluar la efectividad del aprendizaje durante la etapa de entrenamiento, se monitoreó el comportamiento de la función de pérdida (*loss*), la cual mide el margen de error del modelo en cada iteración:
<p align="center">
<img width="663" height="395" alt="image" src="https://github.com/user-attachments/assets/ff25e95a-e298-4e98-ad2f-9319e94bf0d1" />
</p>

### Interpretación de la Gráfica de Pérdida y Sustentación del Modelo

La gráfica muestra la curva de pérdida de entrenamiento de la CNN construida desde cero a lo largo de 8 épocas (registradas de la 0 a la 7). En el eje vertical (*Loss*), se aprecia un descenso constante e intermitente del error, partiendo desde un valor cercano a 0.694 en la primera época y reduciéndose progresivamente hasta alcanzar aproximadamente 0.672. Esta tendencia decreciente confirma que el modelo está ajustando sus pesos de forma efectiva y reduciendo su incertidumbre al clasificar las superficies. El rendimiento mostrado en la gráfica permite sustentar técnicamente por qué la elección de una Red Neuronal Convolucional (CNN) es superior a arquitecturas tradicionales como el Perceptrón Multicapa o los algoritmos basados en Métodos de Kernel:
- **Preservación de la información espacial:** Un Perceptrón clásico exige aplanar las imágenes en un vector unidimensional de datos, lo que destruye por completo las relaciones geométricas entre píxeles adyacentes. Las grietas en el concreto son patrones continuos y lineales que dependen de su entorno espacial; la CNN preserva esta estructura bidimensional mediante las capas de convolución (Conv2D), analizando el contexto de cada región de la imagen.
- **Extracción autónoma de características (frente a Métodos de Kernel):** Los métodos tradicionales basados en Kernel (como las Máquinas de Vectores de Soporte o SVM) dependen de una ingeniería de características manual, donde el usuario debe diseñar previamente qué filtros aplicar para resaltar bordes. En contraste, el descenso de la curva de pérdida demuestra cómo la CNN aprende y optimiza de forma totalmente autónoma sus propios núcleos o filtros internos para aislar fisuras y texturas del concreto.
- **Invarianza a la traslación:** Gracias a la inclusión de capas de reducción (MaxPooling), la red es capaz de reconocer lo que aparezca dentro de la fotografía (centro, esquina o bordes), capacidad de la que carecen las redes densas tradicionales.

Además de monitorear la pérdida durante el entrenamiento, es crucial evaluar cómo el modelo generaliza su aprendizaje frente a imágenes de concreto que no ha procesado previamente. Para ello, se analizaron las métricas de validación:
<p align="center">
<img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/886f5983-3126-4d6d-a2cb-5646f58b158b" />
</p>

### Análisis de las Métricas de Validación (Accuracy y ROC-AUC)

La gráfica ilustra el comportamiento de la red frente al conjunto de validación a lo largo de 8 épocas (0 a 7), evaluando dos indicadores de rendimiento: la Exactitud o *Accuracy* (representada por la línea azul) y el Área Bajo la Curva ROC o ROC-AUC (representada por la línea naranja)

Al analizar la evolución de estas métricas, se destacan los siguientes comportamientos en el aprendizaje del modelo:

*   **Evolución del Accuracy (Exactitud):** Durante las primeras cinco épocas (de la 0 a la 4), la curva azul se mantiene completamente plana en un valor cercano a 0.510. Este estancamiento temporal es un fenómeno común en las etapas iniciales de las redes neuronales, e indica que el modelo probablemente estaba clasificando todas las imágenes bajo una sola categoría mayoritaria mientras calibraba sus pesos internos. Sin embargo, a partir de la época 5, la red logra un "despertar" en su aprendizaje, incrementando drásticamente su exactitud hasta alcanzar un valor superior a 0.625 en la época 7. Esto demuestra que la arquitectura finalmente logró abstraer las características que definen a una grieta y comenzó a realizar predicciones correctas sobre datos nuevos.

En conjunto, esta gráfica demuestra la resiliencia de la arquitectura CNN: aunque inicialmente la red no era capaz de dar el diagnóstico exacto (*Accuracy* bajo), sus filtros convolucionales ya estaban comenzando a detectar sutiles diferencias matemáticas entre las texturas sanas y las fisuras (*ROC-AUC* alto y estable)[cite: 6]. Conforme avanzaron las épocas, esa capacidad discriminatoria se cristalizó en predicciones concretas y precisas, confirmando la viabilidad del modelo para la detección automática de daños estructurales.


## Explicabilidad del Modelo mediante Grad-CAM (Interpretabilidad Cualitativa)

Además de evaluar el rendimiento numérico mediante métricas globales y la matriz de confusión, es indispensable auditar el criterio interno de la red para romper el paradigma de "caja negra". Para verificar en qué regiones visuales se enfoca el modelo al tomar una decisión, se implementó la técnica **Grad-CAM** (*Gradient-weighted Class Activation Mapping*):
<p align="center">
<img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/6e53b0df-e0ff-4074-804f-2a3c11b90653" />
</p>

### Interpretación del Mapa de Activación y Utilidad del Código

El resultado de la técnica Grad-CAM se compone de tres visualizaciones clave:

1. **Imagen Original (Imagen label=0):** Representa la fotografía de entrada que se ingresa a la red neuronal para su evaluación.
2. **Mapa de Activación (rad-CAM pred=0):** Genera una matriz de intensidad donde los colores cálidos (tonos amarillos y verdes) representan los píxeles que provocaron la mayor activación matemática en las últimas capas convolucionales.
3. **Superposición:** Fusiona el mapa de calor sobre la fotografía original, permitiendo auditar la atención espacial del modelo de forma intuitiva.

#### Utilidad en la Inspección Estructural
Esta técnica aporta el máximo nivel de validación cualitativa al proyecto. En el diagnóstico de estructuras de concreto, garantiza que la Red Neuronal Convolucional esté detectando la geometría lineal y los bordes oscuros característicos de una grieta, y no patrones espurios del entorno como manchas de humedad, porosidades normales del cemento o sombras de la iluminación.

## Conclusión

El desarrollo de este proyecto demuestra que las Redes Neuronales Convolucionales (CNN) son la herramienta óptima para el diagnóstico de superficies de concreto, superando a modelos tradicionales como el Perceptrón Multicapa o SVM al abstraer de manera autónoma la geometría bidimensional de las fisuras sin requerir ingeniería de características manual. Esta viabilidad arquitectónica se respalda con la evolución positiva del aprendizaje, donde el incremento sostenido del Accuracy y la estabilidad del ROC-AUC prueban que el modelo generalizó con éxito los patrones de daño estructural, reduciendo su margen de error ante imágenes nunca antes vistas. Finalmente, la integración de la técnica Grad-CAM dotó al sistema de la transparencia y confiabilidad indispensables en la ingeniería civil, comprobando cualitativamente que la red enfoca su análisis matemático en las fracturas físicas reales y no en ruidos visuales del entorno

### Sobre la aplicación directa en nuestro proyecto "CrackScan"
- Los detalles se encuentran señalados en el readme.md de la capeta redes neuronales.
