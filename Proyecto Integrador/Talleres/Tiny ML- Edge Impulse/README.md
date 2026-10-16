#Clasificación de Imágenes con TinyML (Edge Impulse, Arduino y SenseCraft)

Se presenta el desarrollo e implementación de un sistema de TinyML (Machine Learning en dispositivos de borde) enfocado en la clasificación de imágenes en tiempo real. El proyecto utiliza un microcontrolador con cámara (XIAO ESP32S3) para reconocer y diferenciar entre dos clases específicas: el integrante **Josue** y una **botella**. Todo el flujo comprende desde la recolección y etiquetado del dataset, el diseño del impulso y entrenamiento en Edge Impulse, hasta la validación estadística y el despliegue visual en SenseCraft.

---

## Dataset de Imágenes y Etiquetas del proyecto
Para el entrenamiento del modelo de red neuronal se recolectó un conjunto de datos (dataset) compuesto por dos clases principales:
* **Clase 1:** `Josue` (fotografías del integrante bajo diferentes ángulos y poses).
* **Clase 2:** `botella` (fotografías de una botella de agua como prueba).

El proceso de carga y estructuración de los datos se realizó mediante las siguientes etapas:
* **Carga de archivos:** Las imágenes de cada clase se subieron de forma independiente a la plataforma Edge Impulse utilizando la opción de carga directa de archivos individuales o carpetas[cite: 1, 2].
* **Etiquetado:** Se asignó una etiqueta personalizada a cada conjunto (`Josue` y `botella`), indicando que no se trataba de un proyecto de detección de objetos con delimitadores (*bounding boxes*), sino de una tarea de clasificación de imágenes general[cite: 3].
* **División del Dataset (Split):** El conjunto de datos se dividió automáticamente para separar los datos de entrenamiento y las pruebas de validación[cite: 3, 4].

---

## 3. Configuración en Edge Impulse (Paso a Paso - Incluyendo Paso 6)
El pipeline de procesamiento y entrenamiento del modelo se configuró en la plataforma de Edge Impulse siguiendo una estructura modular:
<img width="1600" height="877" alt="image" src="https://github.com/user-attachments/assets/f14f8ee7-c949-49be-9f4f-3073d5f1d499" />
imagen del proyecto:

1. **Creación del Proyecto:** Se configuró un nuevo proyecto enfocado en la clasificación de imágenes[cite: 1, 2].
2. **Diseño del Impulso (*Impulse Design*):** 
   * Se estableció un bloque de entrada de imagen (*Image data*), redimensionando las entradas a una resolución estándar de **96x96 píxeles**[cite: 5].
   * Como **Processing Block**, se seleccionó *Image*, encargado de preprocesar, normalizar y ajustar la profundidad de color (RGB) de las imágenes[cite: 6, 7].
   * Como **Learning Block**, se seleccionó **Transfer Learning (Images)**[cite: 6, 7]. Esta opción aprovecha un modelo preentrenado para extraer características visuales complejas, permitiendo obtener un rendimiento óptimo incluso con datasets pequeños[cite: 6].
3. **Configuración de Entrenamiento:**
   * **Ciclos de entrenamiento (*Epochs*):** Se configuraron 30 ciclos[cite: 7].
   * **Tasa de aprendizaje (*Learning rate*):** 0.0005[cite: 7].
   * **Procesador:** CPU[cite: 7].
4. **Generación de Características y Entrenamiento:** Se ejecutó la extracción de características (*Generate features*) y posteriormente el entrenamiento de la red neuronal (*Save & train*)[cite: 7, 8].

---

## 4. Pruebas Estadísticas y Métricas de Validación
Una vez completado el entrenamiento, se evaluó el desempeño del modelo utilizando el conjunto de validación (*validation set*), obteniendo métricas estadísticas sobresalientes:
* **Precisión (*Accuracy*):** 100.0% de acierto en el conjunto de validación[cite: 8].
* **Pérdida (*Loss*):** 0.04[cite: 8].
* **Matriz de Confusión:** Mostró una separación perfecta entre ambas clases (`Josue` y `botella`), sin falsos positivos ni falsos negativos registrados en la validación[cite: 8].
* **Métricas adicionales:**
  * Área bajo la curva ROC (AUC): `1.00`[cite: 8].
  * Precisión promedio ponderada: `1.00`[cite: 8].
  * Sensibilidad (*Recall*): `1.00`[cite: 8].
  * Puntaje F1 (*F1-Score*): `1.00`[cite: 8].
* **Rendimiento en Dispositivo (*On-device performance*):** Se seleccionó la optimización **Quantized (int8)** para reducir la latencia, el consumo de memoria RAM y el tamaño en la memoria Flash, manteniendo la misma precisión que el modelo flotante (*float32*)[cite: 10].

---

## 5. Despliegue y Pruebas en SenseCraft / Arduino IDE
El modelo optimizado en formato TensorFlow Lite (`int8 quantized`) se exportó para su implementación práctica[cite: 10, 16]:
* **Implementación en Arduino IDE:** Se descargó la librería de Arduino del proyecto[cite: 10], se configuraron los pines específicos para la placa **XIAO ESP32S3** (ajustando parámetros de la cámara y el búfer de memoria `arena_size` en caso de requerir espacio adicional)[cite: 11, 12, 13, 14], logrando visualizar las predicciones en tiempo real a través del Monitor de Serie[cite: 15].
* **Pruebas de Visualización en SenseCraft:** 
  * Se subió el archivo del modelo cuantizado (`.lite`) a la plataforma de espacio de trabajo de **SenseCraft**[cite: 16, 17].
  * Durante las pruebas en tiempo real frente a la cámara, el sistema logró identificar de forma correcta y fluida tanto al integrante **Josue** como a la **botella**, mostrando barras de probabilidad con altos porcentajes de confianza en la interfaz gráfica[cite: 17].
