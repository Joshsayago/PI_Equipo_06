
# README 1: Implementación de Modelo Preentrenado en SenseCraft AI

## 1. Descripción de la Tarea
En esta primera parte se implementó un modelo preentrenado de SenseCraft AI para el reconocimiento y clasificación de rostros y género en tiempo real. Se realizaron pruebas con 3 integrantes del equipo, documentando el funcionamiento de los umbrales de configuración y el rendimiento del dispositivo.

---

## 2. Pruebas del Modelo con Integrantes del Equipo

### Prueba 1: Detección múltiple (2 integrantes)
* **Evidencia:**
  <<img width="1280" height="850" alt="image" src="https://github.com/user-attachments/assets/f9608c34-d2ef-4e8c-b53b-78589d9bb8b6" />
<img width="1200" height="856" alt="image" src="https://github.com/user-attachments/assets/4fddcd27-558c-40ca-bf7e-2e6ab137f541" />


* **Explicación de la prueba:** En esta primera prueba se evaluó la capacidad del modelo para detectar y clasificar simultáneamente a dos personas frente a la cámara. El sistema logra etiquetar correctamente a cada rostro por separado gracias al ajuste dinámico de los umbrales de superposición (*IoU Threshold*), evitando que una sola caja delimitadora encierre a ambos rostros.

---

### Prueba 2: Detección individual - Integrante 1
* **Evidencia:**
  <img width="1293" height="960" alt="image" src="https://github.com/user-attachments/assets/359ae155-57fb-4ad5-a05e-fb360536cb2b" />

* **Explicación de la prueba:** Se probó el sistema de manera individual. El panel de la derecha (*Device Logger*) muestra en tiempo real las coordenadas de la caja detectada (`boxes`) y las métricas de rendimiento interno (`preprocess`, `inference` y `postprocess`).

---

### Prueba 3: Detección individual - Integrante 2
* **Evidencia:**
<img width="1295" height="972" alt="image" src="https://github.com/user-attachments/assets/cad9065b-6898-4d54-9d0a-48068a65a8b0" />

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
* **Preprocess (~73 ms - 80 ms):** Tiempo que tarda la placa en capturar, redimensionar y normalizar la imagen de la cámara.
* **Inference (~950 ms - 970 ms):** Tiempo que le toma a la red neuronal ejecutar el procesamiento matemático para reconocer y clasificar los rostros.
* **Postprocess (~1 ms - 3 ms):** Tiempo empleado en aplicar los filtros de umbral y renderizar la interfaz gráfica final.

---
 
## 5. Prueba de Salida GPIO y Activación del LED

En esta sección se completó la configuración del hardware para vincular la detección del modelo a una salida física (GPIO) que activa un indicador LED al cumplirse el reconocimiento.

### Evidencia 1: Montaje y prueba de hardware con el equipo
* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 1: Archivo image_2295d0.jpg - Foto general del equipo con la placa conectada y los integrantes listos para la prueba] -->

* **Explicación:** Se preparó el entorno físico sobre la mesa de trabajo, conectando la placa con la cámara y el sistema de pines GPIO listo para interactuar con los integrantes del equipo.

---

### Evidencia 2: Detalle del módulo de hardware (SenseCraft / XIAO)
* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 2: Archivo image_2295f4.jpg - Primer plano de la placa y la cámara sostenida mostrando los componentes y el LED integrado] -->

* **Explicación:** Vista en detalle del dispositivo hardware. Aquí se observa el módulo ensamblado que procesa la inferencia en el borde (*Edge AI*) y gestiona la línea de salida digital para el LED.

---

### Evidencia 3: Validación del modelo con integrante en estación de trabajo
* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 3: Archivo image_229d30.jpg - Foto de la integrante frente al portátil mientras se ejecuta la prueba de reconocimiento] -->

* **Explicación:** Se ejecutó la prueba de validación enfocando a la integrante del equipo. Al posicionarse frente a la cámara, el sistema procesó la imagen y reconoció el rostro con el nivel de confianza configurado.

---

### Evidencia 4: Detalle de la activación de salida y LED encendido
* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 4: Archivo image_229d50.jpg - Primer plano de la placa con el LED indicador encendido en naranja/amarillo] -->

* **Explicación:** Al cumplirse la condición de reconocimiento positivo en la plataforma SenseCraft, el pin GPIO configurado cambió de estado lógico (nivel bajo a nivel alto), lo que provocó el **encendido exitoso del LED** integrado en la placa, confirmando la correcta comunicación entre la inteligencia artificial y el hardware externo.
