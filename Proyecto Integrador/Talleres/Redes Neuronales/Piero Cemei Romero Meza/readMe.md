--**Interpretación**--

**CNN:**
La utilización de redes neuronales convolucionales (CNN) resulta pertinente para el desarrollo del proyecto debido a que una de las principales fuentes de información serán imágenes de grietas presentes en paredes y otras estructuras. Una CNN está diseñada para analizar imágenes a partir de sus píxeles y aprender características visuales relevantes, como bordes, texturas, formas y patrones. Por esta razón, su utilización permite plantear un sistema capaz de analizar las fotografías proporcionadas por el usuario y reconocer características asociadas a los diferentes tipos o niveles de grietas.

Esta aplicación resulta especialmente importante para el proyecto, ya que se plantea trabajar con un conjunto de imágenes que represente grietas de diferentes niveles de severidad, desde aquellas que presentan un menor nivel de riesgo hasta aquellas que pueden representar una condición más crítica. El modelo puede utilizar las imágenes del dataset durante el entrenamiento para aprender patrones visuales y posteriormente utilizarlos para realizar una clasificación sobre nuevas imágenes.

En el notebook analizado se implementa una CNN utilizando PyTorch. El modelo está compuesto por bloques de convolución, funciones de activación ReLU, operaciones de pooling y una etapa final de clasificación. Además, el dataset utilizado por el código auxiliar se organiza en clases y se divide en conjuntos de entrenamiento, validación y prueba, siguiendo una distribución de 70 %, 15 % y 15 %, respectivamente.

Para el proyecto de detección de grietas, este mismo enfoque puede ser adaptado posteriormente al dataset específico de imágenes de grietas. De esta manera, la CNN podría aprender las características visuales presentes en las diferentes categorías establecidas para el proyecto y utilizar dicho aprendizaje para analizar nuevas fotografías.

Por otro lado, el notebook también presenta Keras como una herramienta para facilitar la construcción y entrenamiento de redes neuronales. Sin embargo, en el código analizado Keras se utiliza como un ejemplo independiente mediante el dataset IMDB y modelos de capas densas, mientras que la CNN encargada del procesamiento de imágenes se implementa mediante PyTorch. Por ello, Keras puede considerarse dentro del trabajo como una herramienta complementaria para comprender y experimentar con la construcción de modelos de aprendizaje profundo, pero no como el framework utilizado actualmente para la CNN de imágenes.

Finalmente, el análisis de imágenes mediante CNN podría complementarse con información geológica y territorial relacionada con zonas del Perú que presentan condiciones de riesgo, como problemas de inestabilidad del suelo o posibles zonas susceptibles a hundimientos. La combinación de la información visual obtenida de las fotografías con información geológica permitiría plantear posteriormente un análisis más completo del riesgo. No obstante, esta integración corresponde a una etapa posterior del proyecto y no se encuentra implementada directamente en el notebook analizado.

**Keras:**

Keras es una herramienta de alto nivel que facilita la construcción, configuración y entrenamiento de modelos de redes neuronales. Su principal ventaja es que permite definir la estructura de una red mediante capas y configurar elementos como el optimizador, la función de pérdida y las métricas sin tener que implementar manualmente todos los procesos internos del entrenamiento.

En el notebook se utiliza Keras mediante una arquitectura Sequential, en la cual se agregan capas densas (Dense) con funciones de activación ReLU y una capa final con función sigmoide para realizar una clasificación binaria. Posteriormente, el modelo se configura mediante compile() y se entrena mediante fit().

Además, el notebook permite observar diferentes técnicas relacionadas con el entrenamiento de redes neuronales, como la validación, la regularización y el Dropout, utilizados principalmente para analizar y reducir problemas de sobreajuste.

En el contexto del proyecto, el estudio de Keras permite comprender una alternativa para desarrollar modelos de aprendizaje profundo de forma más sencilla. Sin embargo, es importante diferenciarlo de la implementación principal de la CNN mostrada en el notebook, ya que esta última utiliza PyTorch.
