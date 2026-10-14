# README 2: Entrenar y Desplegar un Modelo de IA Propio en SenseCraft AI

## 1. Descripción de la Tarea
En esta segunda parte del proyecto, el grupo desarrolló, entrenó y desplegó un modelo de clasificación de imágenes personalizado utilizando el módulo **XIAO ESP32S3 Sense**[cite: 1]. El objetivo fue clasificar objetos en tiempo real (por ejemplo, detectar un *Mouse* u objetos como *BOX ESP32xiao* frente a la clase *Entorno*) y vincular la inferencia a una salida física mediante GPIO para activar un indicador LED[cite: 1].
Este análisis fue realizado por los integrantes 4 y 5 Dominik Beleván Amaro y Piero Cimei Romero 

---

## 2. Recolección de Datos (Dataset) y Entrenamiento del Modelo

Para garantizar un entrenamiento preciso y representativo, se capturaron muestras de imágenes directamente desde la cámara del dispositivo en tiempo real[cite: 1]:

* **Clases creadas:**
  * **Mouse:** Muestras enfocando el mouse sobre la mesa de trabajo[cite: 10].
  * **BOX ESP32xiao:** Muestras de la caja o estructura de protección e impresión 3D[cite: 10, 11].
  * **Entorno:** Muestras de control de la mesa y espacio de trabajo sin el objeto objetivo[cite: 10].
* **Dataset generado:**
  * Se recopilaron 78 muestras para las clases de objetos principales y 82 muestras para la clase *Entorno*[cite: 10].
  * Todo el conjunto de datos recopilados fue exportado y comprimido en un archivo `.zip` para ser subido al repositorio del grupo[cite: 1].

### Evidencia 1: Panel de recolección de datos y vista previa (Preview)
* **Integrantes del equipo:**
  <!-- [AQUÍ PONER EL NOMBRE DE LOS INTEGRANTES DEL GRUPO QUE PARTICIPARON EN LA CAPTURA Y ENTRENAMIENTO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 1: Archivo image_231c78.jpg - Captura de la interfaz de SenseCraft con las clases 'Mouse', 'Entorno', el video en vivo y la vista previa del 99% de confianza] -->

* **Explicación:** En la interfaz de SenseCraft AI se observa la etapa de recolección (`Step 1: Collect Classification Data`)[cite: 10]. En la parte inferior derecha, en la sección **Preview**, se valida el modelo entrenado mostrando un **99% de probabilidad/confianza** para la clase *Mouse* cuando el objeto se encuentra posicionado frente al lente de la cámara[cite: 10].

---

## 3. Pruebas de Inferencia y Activación de Salida GPIO

Tras desplegar el modelo en la placa **XIAO ESP32S3 Sense**, se configuró una regla de salida GPIO para enviar un estado lógico alto cada vez que el modelo clasifique exitosamente el objeto objetivo[cite: 1].

### Evidencia 2: Prueba de salida GPIO con el objeto objetivo y carcasa 3D
* **Integrantes en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DEL INTEGRANTE QUE MANTIENE LA PLACA Y REALIZA LA PRUEBA] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 2: Archivo image_231c9b.jpg - Foto en primer plano de la placa XIAO con el LED encendido en naranja, sosteniendo la caja 3D azul en la mano] -->

* **Explicación:** Se sostiene la caja/impresión 3D azul frente al módulo de visión[cite: 11]. Al ser reconocida la clase correspondiente, el pin GPIO cambia su estado y se enciende el LED indicador luminoso integrado en la placa, demostrando la respuesta física e inmediata del hardware ante la inferencia[cite: 1, 11].

---

### Evidencia 3: Validación del modelo enfocando el Mouse de prueba
* **Integrantes en la foto:**
  <!-- [AQUÍ PONER EL NOMBRE DE LOS INTEGRANTES RESTANTES DEL EQUIPO QUE VALIDAN LA PRUEBA EN EL ESCRITORIO] -->

* **Evidencia:**
  <!-- [AQUÍ VA LA IMAGEN 3: Archivo image_231cbb.jpg - Foto enfocando el mouse en la mesa y la placa XIAO con el LED encendido frente a la laptop] -->

* **Explicación:** Se posicionó el *Mouse* sobre la mesa de trabajo en el rango visual de la cámara[cite: 12]. El modelo procesó la imagen en el borde (*Edge AI*) identificando el objeto con éxito, lo que activó nuevamente la salida GPIO y encendió el LED indicador de la tarjeta[cite: 1, 12].

---

## 4. Archivos del Modelo en el Repositorio
Para dar cumplimiento a los requerimientos de la tarea[cite: 1]:
1. El archivo comprimido `.zip` con todo el dataset de imágenes de entrenamiento fue subido a la carpeta raíz/datos del repositorio del grupo[cite: 1].
2. El archivo ejecutable del modelo de IA generado (*.uf2* / binario de despliegue) se encuentra almacenado dentro del repositorio del grupo para su posterior reutilización e inspección[cite: 1].
