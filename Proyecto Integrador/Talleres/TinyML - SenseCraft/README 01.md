# 🟢  Implementación de Modelo Preentrenado y Control GPIO

**Proyecto Integrador · Taller de TinyML & Edge AI**

En este primer apartado se realiza el despliegue de un modelo preentrenado para visión computacional en la plataforma **SenseCraft AI**, ejecutándolo directamente sobre la tarjeta **XIAO ESP32S3 Sense**. Se evaluó el modelo con pruebas de reconocimiento visual en tiempo real junto a los miembros del equipo y se configuró una línea de salida digital GPIO para conmutar un LED indicador cuando se satisface el reconocimiento.

---

##  1. Objetivos

* **Despliegue On-Device:** Implementar y ejecutar un modelo de detección y clasificación en tiempo real sobre el hardware de procesamiento en el borde (*XIAO ESP32S3 Sense*).
* **Validación Experimental:** Validar la capacidad de detección del algoritmo tanto en tomas individuales como en pruebas grupales con integrantes del equipo.
* **Calibración de Parámetros:** Evaluar el impacto práctico del umbral de confianza (*Confidence Threshold*) y del umbral de superposición (*IoU Threshold*) en el rendimiento del modelo.
* **Integración Hardware-Software:** Configurar los pines de salida GPIO para accionar una respuesta física (encendido de un indicador LED) vinculada a los eventos de detección.

---

##  2. Recursos y Componentes de Hardware

| Recurso | Tipo | Función Principal |
| :--- | :--- | :--- |
| **XIAO ESP32S3 Sense** | Hardware / SoC | Microcontrolador de alto rendimiento para ejecución de redes neuronales en el borde. |
| **Cámara OV2640** | Hardware / Sensor | Captura continua de fotogramas e ingreso de video al modelo de visión. |
| **SenseCraft AI** | Software / Web | Entorno de gestión, configuración de umbrales y monitoreo de inferencias en vivo. |
| **Modelo Preentrenado** | Red Neuronal | Algoritmo de clasificación facial para la detección de características y género. |
| **Salida Digital GPIO** | Periférico / Hardware | Control del estado lógico del indicador LED según el resultado del procesamiento. |

---

##  3. Fundamentación e Implementación

Para esta fase se utilizó un modelo preentrenado de visión artificial optimizado para dispositivos de bajo consumo. El sistema analiza el flujo de imágenes capturado por el lente de la cámara del **XIAO ESP32S3 Sense**, identifica rostros y genera un recuadro delimitador (*bounding box*) junto con la probabilidad calculada (`male` o `female`).

---

##  4. Pruebas de Reconocimiento y Evaluación con Integrantes

Se llevaron a cabo pruebas en la estación de trabajo para evaluar la estabilidad del modelo frente a diferentes integrantes y combinaciones.

### 👥 Prueba 1: Detección Simultánea Múltiple
* **Integrantes en la foto:** Mónica Huamán Bernal y Josue Sayago Morán

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
* **Integrante en la foto:** Piero Simei Romero

- **Evidencia:**
<p align="center">
 <img width="1284" height="994" alt="image" src="https://github.com/user-attachments/assets/3fde6091-db3f-4ca5-8632-0108aa01099b" />

</p>

* **Resultado obtenido:** Etiqueta `male` con confianza de **88%**.
* **Análisis técnico:** Se validó la inferencia de manera individual. En la consola lateral (*Device Logger*) se verificaron los tiempos de ciclo, confirmando una tasa de procesamiento estable con un tiempo de inferencia cercano a los **960 ms**.

---

### Prueba 3: Detección individual 2
* **Integrante en la foto:** Diego Alessandre Murga Saavedra

- **Evidencia:**
<p align="center">
  <img width="1100" height="850" alt="image" src="https://github.com/user-attachments/assets/30220c44-4fff-419d-a3a4-6135de15b7f2" />
</p>

* **Resultado obtenido:** Etiqueta `male` con confianza de **86%**.
* **Análisis técnico:** Se confirmó la repetibilidad del modelo ante cambios de posición y condiciones de iluminación del ambiente de trabajo, superando sin inconvenientes el valor crítico del umbral establecido.

---

## 5. Configuración de las Reglas de Salida GPIO

Para vincular las inferencias del modelo con la respuesta física en la tarjeta, se accedió a la sección **Salida > GPIO** en SenseCraft AI[cite: 13]. Se configuró la conmutación de la salida digital para activar el LED cuando cualquier reconocimiento válido supere el umbral de confianza establecido[cite: 13].

### Parámetros Configurables de la Regla

| Parámetro | Valor Asignado | Función / Descripción |
| :--- | :--- | :--- |
| **Objetos configurados** | `male` / `female` | Clases que disparan el evento de activación de salida[cite: 13]. |
| **Salida GPIO** | `LED` | Pin de salida digital conectado al indicador luminoso integrado[cite: 13]. |
| **Condición lógica** | `Mayor que` | Operador de comparación evaluado sobre el nivel de confianza[cite: 13]. |
| **Umbral de confianza** | `53` | Porcentaje mínimo requerido para conmutar la salida a estado ALTO[cite: 13]. |
| **Estado predeterminado** | `LED apagado` | Estado inicial del pin cuando no hay detección válida[cite: 13]. |
| **Estado activo** | `LED encendido` | Estado del pin al cumplirse la condición en cualquiera de las clases[cite: 13]. |

---

## 6. Evidencias Fotográficas e Interpretación de los Integrantes

Se realizaron las verificaciones en vivo con los integrantes del equipo para comprobar la activación del LED ante detecciones afirmativas.

### 👤 Prueba 1: Integrante Masculino (Detección Positiva)
 <img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/bc3e73f1-57eb-40c8-a290-7fd253dd3780" />
 

* **Nombre del integrante:**  Josué Sayago 
* **Resultados de la inferencia:**
  * **Etiqueta detectada:** `male`
  * **Confianza obtenida:** 86%
  * **Umbral GPIO:** Mayor que 53%
  * **Estado del LED:** 🟡 **Encendido**
    <img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/df709202-4717-4a8d-b77b-385b06ff9429" />

* **Interpretación técnica:** El modelo identificó a la persona con la etiqueta `male` y un 86% de certeza. Al superar holgadamente el umbral ($86\% > 53\%$), el sistema envió el pulso digital a la salida GPIO y el **LED se encendió exitosamente**.

---

### 👤 Prueba 2: Integrante Femenina (Detección Positiva)

 <img width="1600" height="1200" alt="image" src="https://github.com/user-attachments/assets/1fb8bd7b-c0b2-45bb-a608-3b80314535b0" />


* **Nombre de la integrante:**  Mónica Huamán 
* **Resultados de la inferencia:**
  * **Etiqueta detectada:** `female`
  * **Confianza obtenida:** 80%
  * **Umbral GPIO:** Mayor que 53%
  * **Estado del LED:** 🟡 **Encendido**
    <img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/331d841b-3c31-414b-9e73-3dc9429bf6e4" />

* **Interpretación técnica:** Al posicionarte frente a la cámara, el modelo te identificó con la etiqueta `female` y un 80% de confianza. Como el valor superó el umbral configurado ($80\% > 53\%$), la condición de activación se cumplió nuevamente de forma correcta y el **LED también se encendió**, confirmando que el hardware responde ante la presencia de ambos integrantes.

---

### 📊 Resumen de Respuestas del Hardware

| Integrante Evaluado | Clase Detectada | Confianza | ¿Supera el Umbral (>53%)? | Estado del LED |
| :--- | :--- | :---: | :---: | :---: |
| Josué| `male` | 86% | **Sí** | 🟡 Encendido |
| Mónica | `female` | 80% | **Sí** | 🟡 Encendido |

---

## 7. Explicación del Funcionamiento del LED

El comportamiento observado responde a la integración directa entre el algoritmo de clasificación y el pin de salida física:

1. **Captura e Inferencia:** La cámara del dispositivo XIAO ESP32S3 Sense procesa el rostro presente en el entorno y determina su etiqueta y porcentaje de confianza[cite: 1].
2. **Evaluación de Umbral:** SenseCraft AI verifica si el porcentaje de confianza obtenido por el modelo es mayor a 53[cite: 13].
3. **Respuesta Física:** Al ser la confianza de 86% para `male` y de 80% para `female`, en ambos casos se superó el valor de 53 %, por lo que la señal GPIO conmuta a nivel alto y el **LED permanece encendido durante el reconocimiento activo de cualquiera de los dos integrantes**.

---

## 8. Conclusiones

* Se comprobó la integración entre el software SenseCraft AI y la tarjeta **XIAO ESP32S3 Sense** para el control de periferia física mediante visión artificial[cite: 1, 13].
* Se validó que el indicador LED responde de manera inmediata y estable ante porcentajes de confianza superiores al 53 % tanto para la clase `male` como para `female`.
* Los resultados demostraron una tasa de certeza consistente (80%–88%) en la estación de trabajo durante las pruebas realizadas con el equipo.
