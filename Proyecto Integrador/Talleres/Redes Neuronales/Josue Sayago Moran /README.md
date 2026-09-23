# Análisis Práctico: Detección de Grietas en Estructuras de Concreto mediante CNNs

Tras comprender los fundamentos teóricos de las Redes Neuronales Convolucionales (CNN) —incluyendo el uso de filtros para extraer características visuales (Conv2D), la introducción de no linealidad (ReLU) y la retención de información clave (Pooling)— es momento de llevar estos conceptos a la práctica. 

El objetivo de la siguiente sección es demostrar cómo se estructuró un modelo computacional capaz de analizar fotografías de superficies de concreto para diagnosticar, de manera automática, la presencia de grietas o fallas estructurales. 

¿Qué código lleva? Las herramientas que vas a usar. Generalmente TensorFlow o Keras (para la red neuronal), Matplotlib (para gráficos) y OpenCV o PIL (para leer las fotos).
<img width="1765" height="412" alt="image" src="https://github.com/user-attachments/assets/4f876556-61bd-41c5-9a22-62ccb65f2e11" />

<img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/a35269d4-1978-43ac-b3ad-6005d3712978" />

En esta primera etapa, se importan las bibliotecas fundamentales. TensorFlow y Keras nos proporcionarán las funciones matemáticas para construir la Red Neuronal Convolucional (CNN), mientras que Matplotlib nos permitirá visualizar las imágenes de concreto y las gráficas de aprendizaje del modelo.

<img width="1748" height="603" alt="image" src="https://github.com/user-attachments/assets/397a4cd8-03fa-4b0d-9985-2dc56a104b01" />
Las redes neuronales no entienden imágenes en bruto. En esta celda, estandarizamos todas las fotografías de las estructuras de concreto a una resolución fija (ej. 150x150 píxeles) y normalizamos sus valores para facilitar que la red detecte las sombras y bordes característicos de las grietas.

<img width="1002" height="651" alt="image" src="https://github.com/user-attachments/assets/02e26e60-a555-4f26-899d-7e4ef409cd24" />
