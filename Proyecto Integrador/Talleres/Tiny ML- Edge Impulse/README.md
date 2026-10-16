# Clasificación de Imágenes con TinyML (Edge Impulse, Arduino y SenseCraft)

Se presenta el desarrollo e implementación de un sistema de TinyML (Machine Learning en dispositivos de borde) enfocado en la clasificación de imágenes en tiempo real. El proyecto utiliza un microcontrolador con cámara (XIAO ESP32S3) para reconocer y diferenciar entre dos clases específicas: el integrante **Josue** y una **botella**. Todo el flujo comprende desde la recolección y etiquetado del dataset, el diseño del impulso y entrenamiento en Edge Impulse, hasta la validación estadística y el despliegue visual en SenseCraft.

---

## Dataset de Imágenes y Etiquetas del proyecto
Para el entrenamiento del modelo de red neuronal se recolectó un conjunto de datos (dataset) compuesto por dos clases principales:
* **Clase 1:** `Josue` (fotografías del integrante bajo diferentes ángulos y poses).
* **Clase 2:** `botella` (fotografías de una botella de agua como prueba).

El proceso de carga y estructuración de los datos se realizó mediante las siguientes etapas:
* **Carga de archivos:** Las imágenes de cada clase se subieron de forma independiente a la plataforma Edge Impulse utilizando la opción de carga directa de archivos individuales o carpetas.
* **Etiquetado:** Se asignó una etiqueta personalizada a cada conjunto (`Josue` y `botella`), indicando que no se trataba de un proyecto de detección de objetos con delimitadores (*bounding boxes*), sino de una tarea de clasificación de imágenes general.
* **División del Dataset (Split):** El conjunto de datos se dividió automáticamente para separar los datos de entrenamiento y las pruebas de validación.

---

Configuración en Edge Impulse (Paso a Paso - Incluyendo Paso 6)
El pipeline de procesamiento y entrenamiento del modelo se configuró en la plataforma de Edge Impulse siguiendo una estructura modular.

1. **Creación del Proyecto:** Se configuró un nuevo proyecto enfocado en la clasificación de imágenes
<img width="1600" height="877" alt="image" src="https://github.com/user-attachments/assets/f14f8ee7-c949-49be-9f4f-3073d5f1d499" />
imagen del proyecto:

2. **Diseño del Impulso (*Impulse Design*):** 
   * Se estableció un bloque de entrada de imagen (*Image data*), redimensionando las entradas a una resolución estándar de **96x96 píxeles**.
   * Como **Processing Block**, se seleccionó *Image*, encargado de preprocesar, normalizar y ajustar la profundidad de color (RGB) de las imágenes.
   * Como **Learning Block**, se seleccionó **Transfer Learning (Images)**. Esta opción aprovecha un modelo preentrenado para extraer características visuales complejas, permitiendo obtener un rendimiento óptimo incluso con datasets pequeños.
     
---

## 4. Pruebas Estadísticas y Métricas de Validación
Una vez completado el entrenamiento, se evaluó el desempeño del modelo utilizando el conjunto de validación (*validation set*), obteniendo métricas estadísticas sobresalientes.

Matriz de Confusión y Precisión General: El modelo alcanza una precisión del 100.0% y una pérdida de 0.00 en el conjunto de validación. La matriz de confusión refleja un 100% de aciertos para ambas clases (BOTELLA_AGUA y JOSUE), sin ningún error de clasificación cruzada (0%) y una puntuación de F1 de 1.00. Esto se mantiene tanto en su versión cuantizada (int8) como no optimizada (float32).  

<p align="center">
<img width="644" height="352" alt="image" src="https://github.com/user-attachments/assets/c3f29ecd-a357-4e66-885b-8ace91ebbdad" />
</p>

Métricas de Evaluación Global: Las pruebas estadísticas del conjunto de validación arrojan un Área bajo la curva ROC de 1.00, una precisión media ponderada de 1.00, un promedio ponderado de llamada (Recall) de 1.00 y una puntuación media ponderada en F1 de 1.00, lo que demuestra una discriminación perfecta y una alta fiabilidad del modelo. 

<p align="center">
<img width="735" height="744" alt="image" src="https://github.com/user-attachments/assets/5efa356b-6082-4f3f-b579-94f3adf73383" />
</p>

Explorador de Características: El gráfico de distribución espacial muestra dos cúmulos (clusters) totalmente independientes y distantes entre las características de Botella_agua y Josue, lo que indica que el sistema ha extraído patrones visuales únicos y distinguibles para cada clase sin zonas de ambigüedad.

<p align="center">
<img width="729" height="636" alt="image" src="https://github.com/user-attachments/assets/f075f8b0-ae62-4eb8-bf9d-8495b56aafbb" />
</p>

Explorador de Datos y Pruebas Individuales: El explorador de datos clasificados valida que la totalidad de las muestras de prueba fueron categorizadas correctamente (indicadas en color verde). Al evaluar una muestra específica (como botella_agua_042), el sistema emite un resultado detallado con una probabilidad de 1.00 (100%) para la clase correcta y 0 para la alternativa, confirmando la estabilidad del sistema en la inferencia individual.   

<p align="center">
<img width="1024" height="642" alt="image" src="https://github.com/user-attachments/assets/548c7e02-9ff1-4259-b62e-cb80cb4b40a9" />
</p>

### Interpretación de Resultados Estadísticos y de Validación

#### 1. Análisis de la Matriz de Confusión y Explorador de Características
* **Matriz de Confusión:** Los resultados muestran un rendimiento de clasificación perfecto en el conjunto de validación. Ambas clases (`BOTELLA_AGUA` y `JOSUE`) obtuvieron un **100% de aciertos**, sin registrarse confusiones (0%) ni muestras clasificadas como `INCIERTO` (0%). Asimismo, la **Puntuación de F1** alcanza el valor máximo de **1.00** para ambas categorías, lo que evidencia un equilibrio óptimo entre la precisión y la sensibilidad del modelo.
* **Explorador de Características:** El gráfico de dispersión espacial demuestra una separación clara y definida entre los grupos de datos. Las muestras correspondientes a `Botella_agua` y `Josue` se agrupan en regiones totalmente independientes, confirmando que el algoritmo extrajo características visuales robustas y distinguibles para cada clase sin solapamientos.
<img width="735" height="681" alt="image" src="https://github.com/user-attachments/assets/3d102f60-6cfd-489f-9824-1b109d2bac21" />

#### 2. Métricas Globales del Modelo (Versión No Optimizada - float32)
* **Precisión Global (*Accuracy*):** El modelo registra un **100.00%** de precisión total, validando la efectividad del aprendizaje por transferencia implementado.
* **Área bajo la curva ROC (AUC):** Con un valor de **1.00**, indica una capacidad predictiva y de discriminación ideal entre las clases evaluadas.
* **Precisión y Sensibilidad (*Recall*) Media Ponderada:** Ambas métricas se sitúan en **1.00**, lo que ratifica la ausencia absoluta de errores de tipo I (falsos positivos) y tipo II (falsos negativos).
* **Puntuación F1 Media Ponderada:** El valor de **1.00** consolida la alta fiabilidad y consistencia estadística del modelo antes de aplicar procesos de cuantización u optimización en el dispositivo de borde.
<img width="726" height="687" alt="image" src="https://github.com/user-attachments/assets/c18d6745-f8e7-4dc7-a6ac-0baf2e26c80d" />



* **Precisión (*Accuracy*):** 100.0% de acierto en el conjunto de validación[cite: 8].
* **Pérdida (*Loss*):** 0.04[cite: 8].
* **Matriz de Confusión:** Mostró una separación perfecta entre ambas clases (`Josue` y `botella`), sin falsos positivos ni falsos negativos registrados en la validación[cite: 8].
* **Métricas adicionales:**
  * Área bajo la curva ROC (AUC): `1.00`.
  * Precisión promedio ponderada: `1.00`.
  * Sensibilidad (*Recall*): `1.00`.
  * Puntaje F1 (*F1-Score*): `1.00`.
* **Rendimiento en Dispositivo (*On-device performance*):** Se seleccionó la optimización **Quantized (int8)** para reducir la latencia, el consumo de memoria RAM y el tamaño en la memoria Flash, manteniendo la misma precisión que el modelo flotante (*float32*)[cite: 10].

---

## 5. Despliegue y Pruebas en SenseCraft / Arduino IDE
El modelo optimizado en formato TensorFlow Lite (`int8 quantized`) se exportó para su implementación práctica[cite: 10, 16]:
* **Implementación en Arduino IDE:** Se descargó la librería de Arduino del proyecto[cite: 10], se configuraron los pines específicos para la placa **XIAO ESP32S3** (ajustando parámetros de la cámara y el búfer de memoria `arena_size` en caso de requerir espacio adicional)[cite: 11, 12, 13, 14], logrando visualizar las predicciones en tiempo real a través del Monitor de Serie[cite: 15].
* **Pruebas de Visualización en SenseCraft:** 
  * Se subió el archivo del modelo cuantizado (`.lite`) a la plataforma de espacio de trabajo de **SenseCraft**[cite: 16, 17].
  * Durante las pruebas en tiempo real frente a la cámara, el sistema logró identificar de forma correcta y fluida tanto al integrante **Josue** como a la **botella**, mostrando barras de probabilidad con altos porcentajes de confianza en la interfaz gráfica[cite: 17].
