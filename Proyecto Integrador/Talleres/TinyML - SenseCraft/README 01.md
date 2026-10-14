# README: Implementación de Modelo Preentrenado en SenseCraft AI

## 1. Introducción y Marco Teórico

### Clasificación e Identificación de Género con Inteligencia Artificial
La clasificación de género mediante visión por computadora utiliza modelos de redes neuronales convolucionales (CNN) entrenados para identificar características faciales clave (facciones, proporciones y estructuras de la cara). En este proyecto se utiliza un modelo preentrenado desplegado en la plataforma **SenseCraft AI**, el cual analiza en tiempo real el flujo de video capturado por la cámara, dibujando un recuadro delimitador (*bounding box*) sobre cada rostro detectado y asignando la etiqueta correspondiente (`male` o `female`) junto con un porcentaje de confianza (*confidence score*).

### Módulo XIAO ESP32S3 Sense / Grove Vision AI
Para la ejecución de esta prueba se utiliza el dispositivo **XIAO ESP32S3 Sense** (o **Grove - Vision AI Module**), una plataforma hardware orientada a **Edge AI** (inteligencia artificial en el borde). Sus principales características incluyen:
- **Procesamiento On-Device:** Capacidad de ejecutar la inferencia de redes neuronales de forma local sin depender continuamente de un servidor en la nube.
- **Módulo de Cámara Integrado:** Permite la captura continua de fotogramas a bajo consumo energético.
- **General Purpose Input/Output (GPIO):** Pines programables que permiten interactuar con el entorno físico, enviando señales digitales (como encender un LED o activar un actuador) en respuesta a los resultados de la inferencia.

---

## 2. Pruebas del Modelo con Integrantes del Equipo

### Prueba 1: Detección múltiple
* **Integrantes en la foto:** Mónica y Josue

<p align="center">
  <img width="1100" height="850" alt="image" src="https://github.com/user-attachments/assets/8d4cba8d-fc15-447f-9f19-b04889131d07" />
</p>

- **Evidencia:**
<p align="center">
  <img width="900" height="850" alt="image" src="https://github.com/user-attachments/assets/3cae9abd-638c-49e5-b27b-2472c330df49" />
</p>

- **Explicación de la prueba:** En esta primera prueba se evaluó la capacidad del modelo para detectar y clasificar simultáneamente a dos personas frente a la cámara. El sistema logra etiquetar correctamente a cada rostro por separado gracias al ajuste dinámico de los umbrales de superposición (*IoU Threshold*), evitando que una sola caja delimitadora encierre a ambos rostros.

---

### Prueba 2: Detección individual 1
* **Integrante en la foto:** Josue

- **Evidencia:**
<p align="center">
  <img width="1100" height="850" alt="image" src="https://github.com/user-attachments/assets/0ed17ebf-8926-43cd-acff-6704c2dd9e11" />
</p>

- **Explicación de la prueba:** Se probó el sistema de manera individual. El panel de la derecha (*Device Logger*) muestra en tiempo real las coordenadas de la caja detectada (`boxes`) y las métricas de rendimiento interno (`preprocess`, `inference` y `postprocess`).

---

### Prueba 3: Detección individual 2
* **Integrante en la foto:** Diego

- **Evidencia:**
<p align="center">
  <img width="1100" height="850" alt="image" src="https://github.com/user-attachments/assets/30220c44-4fff-419d-a3a4-6135de15b7f2" />
</p>

- **Explicación de la prueba:** Se repitió la prueba con otro integrante para validar la robustez del modelo ante diferentes fisonomías, manteniendo estable el porcentaje de confianza por encima del umbral establecido.

---

## 3. Análisis de Parámetros de Configuración

- **Confidence Threshold (Umbral de confianza: 83):**
  * **Qué significa:** Define el porcentaje mínimo de certeza que exige el modelo para validar una detección.
  * **Por qué se configuró en 83:** Se estableció en este valor para evitar falsos positivos (por ejemplo, que elementos del fondo sean confundidos con personas). Cualquier rostro detectado con una probabilidad menor a este porcentaje es descartado automáticamente.

- **IoU Threshold (Intersection over Union: 44):**
  * **Qué significa:** Es el umbral de superposición utilizado para el filtrado de cajas duplicadas (*Non-Maximum Suppression*).
  * **Por qué se configuró en 44:** Permite que el sistema diferencie con precisión a dos personas cuando se encuentran cerca (como en la primera prueba), evitando que aparezcan múltiples recuadros encimados sobre un mismo rostro.

---

## 4. Métricas de Rendimiento del Dispositivo (Device Logger)

A través del panel de logs se registraron los tiempos de procesamiento por cada fotograma:
- **Preprocess (~73 ms - 80 ms):** Tiempo que tarda la placa XIAO en capturar, redimensionar y normalizar la imagen de la cámara.
- **Inference (~950 ms - 970 ms):** Tiempo que le toma a la red neuronal en el chip ejecutar el procesamiento matemático para reconocer y clasificar los rostros.
- **Postprocess (~1 ms - 3 ms):** Tiempo empleado en aplicar los filtros de umbral y renderizar la interfaz gráfica final.

---

## 5. Prueba de Salida GPIO y Activación del LED

En esta sección se completó la configuración del hardware para vincular la detección del modelo a una salida física (GPIO) que activa un indicador LED al cumplirse el reconocimiento.

### Evidencia 1: Montaje y prueba de hardware con el equipo
* **Integrantes en la foto:** Mónica y Josue

- **Evidencia:**
<p align="center">
  <img width="1100" height="858" alt="image" src="https://github.com/user-attachments/assets/5b869d28-2d79-48f6-a796-22184efa10b7" />
</p>

- **Explicación:** Se preparó el entorno físico sobre la mesa de trabajo, conectando la placa con la cámara y el sistema de pines GPIO listo para interactuar con los integrantes del equipo.

<p align="center">
  <img width="900" height="800" alt="image" src="https://github.com/user-attachments/assets/b38f0095-0c96-4167-bd03-5a24d80cc5ef" />
</p>

---

### Evidencia 2: Detalle del módulo XIAO ESP32S3 Sense
* **Integrante en la foto:** Mónica

<p align="center">
  <img width="900" height="800" alt="image" src="https://github.com/user-attachments/assets/8b0a3fff-123b-4ad8-8a4d-d59c366884d7" />
</p>

- **Evidencia:**
<p align="center">
  <img width="900" height="800" alt="image" src="https://github.com/user-attachments/assets/ad9952b5-3be3-494e-8fbd-e41d7b729617" />
</p>

- **Explicación:** Vista en detalle del dispositivo hardware XIAO. Aquí se observa el módulo ensamblado que procesa la inferencia en el borde (*Edge AI*) y gestiona la línea de salida digital para el LED.

- **Resultado de Activación:** Al cumplirse la condición de reconocimiento positivo en la plataforma SenseCraft, el pin GPIO configurado cambió de estado lógico (nivel bajo a nivel alto), lo que provocó el **encendido exitoso del LED** integrado en la placa XIAO, confirmando la correcta comunicación entre la inteligencia artificial y el hardware externo.
