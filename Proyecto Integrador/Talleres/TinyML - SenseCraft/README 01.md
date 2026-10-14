# README 1: Implementación de Modelo Preentrenado en SenseCraft AI

## 1. Introducción y Marco Teórico

### Clasificación e Identificación de Género con Inteligencia Artificial
La clasificación de género mediante visión por computadora utiliza modelos de redes neuronales convolucionales (CNN) entrenados para identificar características faciales clave (facciones, proporciones y estructuras de la cara). En este proyecto se utiliza un modelo preentrenado desplegado en la plataforma **SenseCraft AI**, el cual analiza en tiempo real el flujo de video capturado por la cámara, dibujando un recuadro delimitador (*bounding box*) sobre cada rostro detectado y asignando la etiqueta correspondiente (`male` o `female`) junto con un porcentaje de confianza (*confidence score*).

### Módulo XIAO ESP32S3 Sense / Grove Vision AI
Para la ejecución de esta prueba se utiliza el dispositivo **XIAO ESP32S3 Sense** (o **Grove - Vision AI Module**), una plataforma hardware orientada a **Edge AI** (inteligencia artificial en el borde). Sus principales características incluyen:
* **Procesamiento On-Device:** Capacidad de ejecutar la inferencia de redes neuronales de forma local sin depender continuamente de un servidor en la nube.
* **Módulo de Cámara Integrado:** Permite la captura continua de fotogramas a bajo consumo energético.
* **General Purpose Input/Output (GPIO):** Pines programables que permiten interactuar con el entorno físico, enviando señales digitales (como encender un LED o activar un actuador) en respuesta a los resultados de la inferencia.

---

## 2. Pruebas del Modelo con Integrantes del Equipo

### Prueba 1: Detección múltiple
* **Integrantes en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE 1 Y DEL INTEGRANTE 2 QUE SALEN EN ESTA FOTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 1: Captura donde aparecen los 2 compañeros con las cajas de detección 'male' y 'female'] -->

* **Explicación de la prueba:** En esta primera prueba se evaluó la capacidad del modelo para detectar y clasificar simultáneamente a dos personas frente a la cámara. El sistema logra etiquetar correctamente a cada rostro por separado gracias al ajuste dinámico de los umbrales de superposición (*IoU Threshold*), evitando que una sola caja delimitadora encierre a ambos rostros.

---

### Prueba 2: Detección individual 1
* **Integrante en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE QUE SALE EN ESTA FOTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 2: Captura del dispositivo mostrando a un integrante individual con el log de consola a la derecha] -->

* **Explicación de la prueba:** Se probó el sistema de manera individual. El panel de la derecha (*Device Logger*) muestra en tiempo real las coordenadas de la caja detectada (`boxes`) y las métricas de rendimiento interno (`preprocess`, `inference` y `postprocess`).

---

### Prueba 3: Detección individual 2
* **Integrante en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE QUE SALE EN ESTA FOTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 3: Captura del dispositivo mostrando al segundo integrante individual] -->

* **Explicación de la prueba:** Se repitió la prueba con otro integrante para validar la robustez del modelo ante diferentes fisonomías, manteniendo estable el porcentaje de confianza por encima del umbral establecido.

---

## 3. Análisis de Parámetros de Configuración

* **Confidence Threshold (Umbral de confianza: 83):**
  * **Qué significa:** Define el porcentaje mínimo de certeza que exige el modelo para validar una detección.
  * **Por qué se configuró en 83:** Se estableció en este valor para evitar falsos positivos (por ejemplo, que elementos del fondo sean confundidos con personas). Cualquier rostro detectado con una probabilidad menor a este porcentaje es descartado automáticamente.

* **IoU Threshold (Intersection over Union: 44):**
  * **Qué significa:** Es el umbral de superposición utilizado para el filtrado de cajas duplicadas (*Non-Maximum Suppression*).
  * **Por qué se configuró en 44:** Permite que el sistema diferencie con precisión a dos personas cuando se encuentran cerca (como en la primera prueba), evitando que aparezcan múltiples recuadros encimados sobre un mismo rostro.

---

## 4. Métricas de Rendimiento del Dispositivo (Device Logger)

A través del panel de logs se registraron los tiempos de procesamiento por cada fotograma:
* **Preprocess (~73 ms - 80 ms):** Tiempo que tarda la placa XIAO en capturar, redimensionar y normalizar la imagen de la cámara.
* **Inference (~950 ms - 970 ms):** Tiempo que le toma a la red neuronal en el chip ejecutar el procesamiento matemático para reconocer y clasificar los rostros.
* **Postprocess (~1 ms - 3 ms):** Tiempo empleado en aplicar los filtros de umbral y renderizar la interfaz gráfica final.

---

## 5. Prueba de Salida GPIO y Activación del LED

En esta sección se completó la configuración del hardware para vincular la detección del modelo a una salida física (GPIO) que activa un indicador LED al cumplirse el reconocimiento.

### Evidencia 1: Montaje y prueba de hardware con el equipo
* **Integrantes en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DE LOS INTEGRANTES QUE SALEN EN ESTA FOTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 4: Archivo image_2295d0.jpg - Foto general del equipo con la placa conectada y los integrantes listos para la prueba] -->

* **Explicación:** Se preparó el entorno físico sobre la mesa de trabajo, conectando la placa con la cámara y el sistema de pines GPIO listo para interactuar con los integrantes del equipo.

---

### Evidencia 2: Detalle del módulo XIAO ESP32S3 Sense
* **Integrantes en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE QUE SOSTIENE EL DISPOSITIVO SI APLICA] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 5: Archivo image_2295f4.jpg - Primer plano de la placa XIAO y la cámara sostenida mostrando los componentes y el LED integrado] -->

* **Explicación:** Vista en detalle del dispositivo hardware XIAO. Aquí se observa el módulo ensamblado que procesa la inferencia en el borde (*Edge AI*) y gestiona la línea de salida digital para el LED.

---

### Evidencia 3: Validación del modelo con integrante en estación de trabajo
* **Integrante en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DE LA INTEGRANTE QUE SALE EN ESTA FOTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 6: Archivo image_229d30.jpg - Foto de la integrante frente al portátil mientras se ejecuta la prueba de reconocimiento] -->

* **Explicación:** Se ejecutó la prueba de validación enfocando a la integrante del equipo. Al posicionarse frente a la cámara, el sistema procesó la imagen y reconoció el rostro con el nivel de confianza configurado.

---

### Evidencia 4: Detalle de la activación de salida GPIO y LED encendido
* **Integrante en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE QUE SOSTIENE LA PLACA SI APLICA] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 7: Archivo image_229d50.jpg - Primer plano de la placa XIAO con el LED indicador encendido] -->

* **Explicación:** Al cumplirse la condición de reconocimiento positivo en la plataforma SenseCraft, el pin GPIO configurado cambió de estado lógico (nivel bajo a nivel alto), lo que provocó el **encendido exitoso del LED** integrado en la placa XIAO, confirmando la correcta comunicación entre la inteligencia artificial y el hardware externo.
