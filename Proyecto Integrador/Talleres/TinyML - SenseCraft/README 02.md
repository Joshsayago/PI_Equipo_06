# 🟢  Entrenar y Desplegar un Modelo de Clasificación Personalizado

**Proyecto Integrador · Taller de TinyML & Edge AI**

En esta segunda fase se desarrolló, entrenó y desplegó un modelo personalizado de clasificación de imágenes en el microcontrolador **XIAO ESP32S3 Sense**. A diferencia de la primera parte, el conjunto de datos fue recopilado directamente en el entorno de trabajo para reconocer objetos de uso frecuente (`BOX ESP32xiao` y `Mouse`) frente al fondo de la estación (`Entorno`), conmutando una salida física GPIO tras la validación de las clases.

---

##  1. Objetivos del Proyecto

* **Construcción de Dataset Local:** Capturar y categorizar muestras de imágenes desde el lente óptico para entrenar un modelo a medida.
* **Entrenamiento e Inferencia On-Device:** Entrenar la red de clasificación en SenseCraft AI y transferir el modelo generado al SOC del XIAO ESP32S3 Sense.
* **Prueba de Confianza en Tiempo Real:** Evaluar el porcentaje de certeza (*Preview*) del modelo ante los distintos objetos objetivos.
* **Control de Periferia por Hardware:** Configurar una salida GPIO para activar un indicador LED cuando se valide la detección de las clases entrenadas.
* **Gestión de Repositorio:** Comprimir las imágenes de entrenamiento en un archivo `.zip` y alojar los binarios del modelo dentro del repositorio del grupo.

---

##  2. Componentes y Recursos Utilizados

| Recurso | Tipo | Descripción de Uso |
| :--- | :--- | :--- |
| **XIAO ESP32S3 Sense** | Hardware / Board | Tarjeta de desarrollo encargada de la captura y la inferencia. |
| **SenseCraft AI** | Plataforma / Cloud | Módulo de recolección de datos, motor de entrenamiento y despliegue. |
| **Clase 1: BOX ESP32xiao** | Objeto Objetivo | Estructura/carcasa de protección azul en impresión 3D. |
| **Clase 2: Mouse** | Objeto Objetivo | Periférico de cómputo sobre la mesa de trabajo. |
| **Clase 3: Entorno** | Muestra de Control | Toma del fondo de la mesa de trabajo sin presencia de objetos. |
| **Salida GPIO & LED** | Actuador Físico | Respuesta luminosa accionada tras la clasificación afirmativa. |

---

## 3. Recolección de Datos y Estructura del Dataset

Para el entrenamiento del modelo se habilitó la captura continua de imágenes en vivo a través de la cámara del dispositivo:

* **Estrategia de captura:** Se variaron los ángulos, la distancia y las condiciones de iluminación sobre la mesa de laboratorio para evitar el sobreajuste (*overfitting*).
* **Consolidado de datos:**
  * **Clases de Objetos (Mouse y BOX):** 78 muestras de alta variabilidad.
  * **Clase de Control (Entorno):** 82 muestras de la mesa de trabajo vacía.
  * **Total recopilado:** 160 imágenes de entrenamiento descargadas y empaquetadas en un archivo `.zip` para el repositorio del grupo.

---

##  4. Validación del Modelo en Tiempo Real (Preview)

Tras completar el proceso de entrenamiento (`Step 2: Training`), se realizaron las pruebas de inferencia previa directamente sobre la plataforma para analizar los puntajes de confianza del algoritmo.

### 4.1. Evaluación de la Clase: BOX ESP32xiao

<img width="1600" height="882" alt="image" src="https://github.com/user-attachments/assets/4fa94db0-3521-47f0-b37e-860c63d797b3" />


* **Etiqueta predicha:** `BOX ESP32xiao`
* **Porcentaje de confianza obtenido:** **97%**
* **Comportamiento secundario:** `Entorno` (2%), `Mouse` (0%).
* **Análisis de la toma:** Al ubicar la carcasa azul en la zona de enfoque del sensor, el algoritmo aisló correctamente sus geometría y color, asignando un 97% de certeza frente a las demás clases.

---

### 4.2. Evaluación de la Clase: Mouse
<img width="1600" height="869" alt="image" src="https://github.com/user-attachments/assets/cb0e2905-2f82-42f1-a2d3-32e615d51644" />


* **Etiqueta predicha:** `Mouse`
* **Porcentaje de confianza obtenido:** **99%**
* **Comportamiento secundario:** `BOX ESP32xiao` (0%), `Entorno` (0%).
* **Análisis de la toma:** Con el mouse situado sobre la superficie de madera, el sistema alcanzó un nivel de reconocimiento casi perfecto (99%), demostrando una clara diferenciación estética entre las clases entrenadas.

---

## 🔌 5. Pruebas de Funcionamiento de Salida GPIO y Actuación Física

Posteriormente al despliegue del modelo en la placa, se habilitó la línea GPIO para enlazar el resultado de la inferencia con el encendido del LED indicador.

### 5.1. Prueba de Hardware 1: Detección de la Carcasa 3D (BOX)

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/37e9260e-d371-4c7d-97c2-7398362fbe57" />


* **Integrante a cargo de la prueba:**
 Dominik Beleván Amaro
* **Resultados observados:**
  * **Objeto presentado:** Carcasa de impresión 3D azul (`BOX ESP32xiao`).
  * **Inferencia del modelo:** Reconocimiento positivo con nivel de confianza superior al umbral.
  * **Respuesta del hardware:** Conmutación de la línea GPIO a nivel ALTO -> **LED encendido (🟡)**.
* **Explicación:** La cámara procesa el objeto sostenido cerca del sensor. Al validar la etiqueta objetivo, el firmware ejecuta el cambio de estado lógico enviando la señal al LED integrado.

---

### 5.2. Prueba de Hardware 2: Detección del Periférico (Mouse)

<img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/1dce9411-4136-4339-98e7-a959f416d284" />


* **Integrantes participando en la prueba:**
Mónica Huamán Bernal
* **Resultados observados:**
  * **Objeto presentado:** Periférico `Mouse` en el área de trabajo.
  * **Inferencia del modelo:** Clasificación certera del periférico sobre la mesa.
  * **Respuesta del hardware:** Conmutación de la línea GPIO a nivel ALTO -> **LED encendido (🟡)**.
* **Explicación:** Con la placa enfocando el mouse en el escritorio, el modelo ejecuta la inferencia localmente y dispara la señal de salida GPIO, manteniendo el indicador LED iluminado durante la detección.

---

##   6. Tabla Resumen de Resultados

| Objeto Evaluado | Clase Asignada | Confianza (Preview) | Estado del LED | Diagnóstico del Sistema |
| :--- | :---: | :---: | :---: | :--- |
| **Carcasa 3D Azul** | `BOX ESP32xiao` | 97% | 🟡 Encendido | Clasificación correcta y activación GPIO confirmada. |
| **Mouse de Escritorio** | `Mouse` | 99% | 🟡 Encendido | Inferencia de alta precisión e integración física estable. |
| **Mesa de Trabajo** | `Entorno` | 0% - 2% | ⚫ Apagado | Sin falsos disparos en ausencia de objetos clave. |

---

##   7. Conclusiones y Entregables del Repositorio

* Se completó exitosamente el ciclo TinyML completo: desde la recolección local de datos hasta el entrenamiento y despliegue del modelo en el hardware **XIAO ESP32S3 Sense**.
* El modelo entrenado demostró altos índices de confianza en la etapa de *Preview* (97% para la estructura 3D y 99% para el mouse).

## 8. Referencias

- [SenseCraft AI](https://sensecraft.seeed.cc/)
- [Documentación oficial de Seeed Studio](https://wiki.seeedstudio.com/)
---

* Se logró validar la interacción del software con el entorno físico, comprobando que las inferencias locales generan una respuesta digital inmediata a través del pin GPIO y el encendido del LED.
* **Archivos adjuntos en el repositorio del grupo:**
  1. Archivo comprimido `.zip` con el dataset de imágenes recopiladas.
  2. Archivo del modelo entrenado desplegable en el dispositivo (*.uf2 / binarios*).
