# 🔎 CrackScan

## Sistema portátil para la evaluación preliminar de grietas en concreto

**CrackScan** es una propuesta de sistema portátil orientado a la detección, registro y evaluación preliminar de grietas en estructuras de concreto. El sistema integra captura de imágenes, geolocalización, procesamiento de información y generación de resultados para apoyar la priorización de inspecciones técnicas.

---

# 📦 Caja Negra

La **caja negra** representa de manera general las entradas y salidas del sistema CrackScan, considerando los flujos de energía e información necesarios para el funcionamiento del dispositivo.

<p align="center">
  <img width="970" height="542" alt="image" src="https://github.com/user-attachments/assets/e63ed7e8-55d7-4205-8a1f-adaf37d32043" />
</p>

### Entradas

- ⚡ Energía eléctrica.
- 🔘 Señal de encendido/apagado.
- 📷 Fotografía de la grieta.
- 📍 Ubicación GPS.

### Salidas

- 📏 Características de la grieta.
- 🗺️ Información territorial obtenida.
- ⚠️ Evaluación preliminar.
- 📋 Recomendación/priorización de inspección.

---

# ⚙️ Esquema de funciones

El **esquema de funciones** representa la interacción entre los diferentes subsistemas del dispositivo y el flujo de información desde la adquisición de datos hasta la generación de resultados.

<p align="center">
 <img width="966" height="531" alt="Captura de pantalla 2026-09-08 190254" src="https://github.com/user-attachments/assets/1fc8f993-1883-4d1a-ae79-31926fb63a5b" />

El funcionamiento del sistema se organiza principalmente en cuatro bloques.

### 🔋 Energía

- Controlar la carga de la batería mediante BMS.
- Almacenar energía en la batería.
- Regular la energía.
- Energizar los sensores.
- Energizar el sistema de control.
- Energizar el sistema de comunicación.

### 📷 Sensor

- Capturar la imagen de la grieta.
- Capturar las coordenadas geográficas.
- Recibir información de geolocalización.

### 🧠 Control

- Recibir datos de la fisura y ubicación.
- Reconocer dimensiones y tipo de fisura.
- Obtener características y ubicación geográfica de la grieta.
- Enviar el modelo de fisura para análisis.
- Comparar los resultados con indicadores de peligro.
- Establecer alertas.

### 📡 Comunicación

- Enviar datos de la fisura y su localización geográfica.
- Indicar el estado de la batería.
- Generar alertas.
- Mostrar información mediante LED.
- Enviar información al Dashboard.
- Comunicar la recomendación o priorización de inspección.

---

# 🧩 Matriz Morfológica

La **matriz morfológica** permite plantear diferentes alternativas de solución para las funciones parciales del sistema y establecer distintos conceptos para el desarrollo del prototipo.

### 🎨 Leyenda

- 🟨 **Concepto A — Primera opción**
- 🟩 **Concepto B — Segunda opción**
- 🟪 **Concepto C — Tercera opción**

---

## 🔌 1. Dominio electrónico

<p align="center">
  <img width="695" height="710" alt="Matriz morfológica - Dominio electrónico" src="https://github.com/user-attachments/assets/f3ea47bd-406d-4914-8b9c-c8a208962ce8" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Capturar imagen de la grieta | XIAO ESP32S3 Sense | Maix Bit / Sipeed Maix | Raspberry Pi Pico 2 W |
| Obtener geolocalización | GPS NEO-6M | GPS NEO-M8N | GPS del celular |
| Conectividad | Bluetooth | Wi-Fi | USB |

---

## 🛠️ 2. Dominio mecánico

<p align="center">
  <img width="701" height="518" alt="Matriz morfológica - Dominio mecánico" src="https://github.com/user-attachments/assets/a96f839b-ad8b-4eaf-bdfd-ffd8904f462a" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Proteger componentes | Carcasa impresa en 3D | Carcasa de acrílico | Caja plástica |
| Facilitar acceso interno | Tapa desmontable | Tapa con bisagra | Carcasa modular |

---

## 🔋 3. Dominio de energía

<p align="center">
  <img width="690" height="512" alt="Matriz morfológica - Dominio de energía" src="https://github.com/user-attachments/assets/bf04f2dc-c7e0-4b36-9210-bf67bdad8745" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Alimentar el sistema | Batería recargable Li-ion 18650 | Batería recargable Li-Po | Power bank |
| Recargar dispositivo | Cable | Panel solar | Cargador externo |

---

## 🎛️ 4. Dominio de control

<p align="center">
  <img width="697" height="957" alt="Matriz morfológica - Dominio de control" src="https://github.com/user-attachments/assets/e6965d53-7b8c-46da-ae1c-a46ae9ff7f83" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Controlar el sistema | XIAO ESP32S3 Sense | Maix Bit / Sipeed Maix | Raspberry Pi Pico 2 W |
| Iniciar captura | Botón físico | Aplicación móvil | Captura automática |
| Controlar iluminación | Interruptor | Control por software | Activación automática |
| Gestionar ubicación | Activación manual | Lectura automática del GPS | Ubicación desde celular |

---

## 🚨 5. Dominio de actuación

<p align="center">
  <img width="782" height="752" alt="image" src="https://github.com/user-attachments/assets/520b086e-7fca-4d0c-9b1d-4b308d1b21a8" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Confirmar captura | LED indicador | Buzzer | Vibración |
| Alertar al usuario | LED tipo semáforo | Buzzer | Notificación digital |
| Mostrar estado del equipo | LCD | Indicadores LED | LED RGB |

---

## 💻 6. Dominio de software

<p align="center">
  <img width="696" height="968" alt="Matriz morfológica - Dominio de software" src="https://github.com/user-attachments/assets/8a8fadc9-cfb2-49c7-b8b2-c36bba7d7894" />
</p>

| Función parcial | Concepto A | Concepto B | Concepto C |
|---|---|---|---|
| Detectar grietas | Machine Learning | Procesamiento de imágenes | Detección de bordes |
| Obtener información territorial | Base de datos pública | API geográfica | Mapa de riesgo |
| Relacionar grieta y zona | Sistema de puntuación | Clasificación automática | Umbrales |
| Clasificar prioridad | Sistema de puntuación | Baja / media / alta | Porcentaje |
| Almacenar resultados | Base de datos | MicroSD | Memoria interna |
| Visualizar resultados | Dashboard web | Aplicación móvil | Pantalla integrada |

---

# 📊 Evaluación de la Matriz Morfológica

## 1. Criterios de evaluación y pesos

Para evaluar los conceptos generados se utilizaron criterios relacionados con el funcionamiento, desempeño y viabilidad del sistema.

| Criterio | Peso |
|---|---:|
| Precisión en detección de grietas | 0.2353 |
| Portabilidad | 0.1176 |
| Facilidad de integración | 0.1176 |
| Consumo energético | 0.1176 |
| Autonomía | 0.1176 |
| Facilidad de uso | 0.1176 |
| Registro y almacenamiento de datos | 0.0588 |
| Costo de implementación | 0.0588 |
| Disponibilidad de componentes | 0.0588 |
| **TOTAL** | **1.00** |

---

## 2. Evaluación de los conceptos

Se utilizó la siguiente escala de valoración:

| Puntaje | Evaluación |
|---:|---|
| 0 | No satisface |
| 1 | Aceptable |
| 2 | Suficiente |
| 3 | Bien |
| 4 | Excelente |

### Resultados

| Criterio | C.S1 – Concepto A | C.S2 – Concepto B | C.S3 – Concepto C |
|---|---:|---:|---:|
| Precisión en detección de grietas | 4 | 3 | 3 |
| Portabilidad | 4 | 3 | 3 |
| Facilidad de integración | 4 | 3 | 3 |
| Consumo energético | 3 | 3 | 2 |
| Autonomía | 3 | 3 | 4 |
| Facilidad de uso | 4 | 3 | 3 |
| Registro y almacenamiento de datos | 4 | 3 | 2 |
| Costo de implementación | 3 | 2 | 3 |
| Disponibilidad de componentes | 3 | 3 | 3 |
| **SUMA TOTAL** | **32** | **26** | **26** |

### Resultado de la evaluación

- **Concepto A = 32 puntos**
- **Concepto B = 26 puntos**
- **Concepto C = 26 puntos**

El Concepto A obtiene la mayor puntuación inicial.

---

## 3. Comparación respecto al Concepto A

El Concepto A se tomó como alternativa base para comparar el desempeño relativo de los conceptos B y C.

| Criterio | Base A | B vs A | C vs A |
|---|---:|---:|---:|
| Precisión en detección de grietas | 0 | -1 | -1 |
| Portabilidad | 0 | -1 | -1 |
| Facilidad de integración | 0 | -1 | -1 |
| Consumo energético | 0 | 0 | -1 |
| Autonomía | 0 | 0 | +1 |
| Facilidad de uso | 0 | -1 | -1 |
| Registro y almacenamiento de datos | 0 | -1 | -2 |
| Costo de implementación | 0 | -1 | 0 |
| Disponibilidad de componentes | 0 | 0 | 0 |
| **SUMA** | **0** | **-6** | **-6** |

### Diferencias respecto al concepto base

**B − A = 26 − 32 = −6**

**C − A = 26 − 32 = −6**

Esto indica que tanto el Concepto B como el Concepto C presentan una diferencia total de **−6 puntos** respecto al Concepto A.

---

## 4. Evaluación ponderada

La evaluación ponderada permite considerar la importancia relativa de cada criterio mediante la asignación de pesos.

| Criterio | Peso | Puntaje A | Puntaje B | Puntaje C |
|---|---:|---:|---:|---:|
| Precisión en detección | 0.2353 | 4 | 3 | 3 |
| Portabilidad | 0.1176 | 4 | 3 | 3 |
| Facilidad de integración | 0.1176 | 4 | 3 | 3 |
| Consumo energético | 0.1176 | 3 | 3 | 2 |
| Autonomía | 0.1176 | 3 | 3 | 4 |
| Facilidad de uso | 0.1176 | 4 | 3 | 3 |
| Registro y almacenamiento | 0.0588 | 4 | 3 | 2 |
| Costo de implementación | 0.0588 | 3 | 2 | 3 |
| Disponibilidad de componentes | 0.0588 | 3 | 3 | 3 |
| **TOTAL** | **1.00** | **32** | **26** | **26** |

---

## 5. Resultados de la evaluación ponderada

El resultado ponderado se obtiene multiplicando el peso de cada criterio por el puntaje correspondiente a cada concepto.

| Criterio | Peso × Concepto A | Peso × Concepto B | Peso × Concepto C |
|---|---:|---:|---:|
| Precisión en detección | 0.9412 | 0.7059 | 0.7059 |
| Portabilidad | 0.4706 | 0.3529 | 0.3529 |
| Facilidad de integración | 0.4706 | 0.3529 | 0.3529 |
| Consumo energético | 0.3529 | 0.3529 | 0.2353 |
| Autonomía | 0.3529 | 0.3529 | 0.4706 |
| Facilidad de uso | 0.4706 | 0.3529 | 0.3529 |
| Registro y almacenamiento | 0.2353 | 0.1765 | 0.1176 |
| Costo de implementación | 0.1765 | 0.1176 | 0.1765 |
| Disponibilidad de componentes | 0.1765 | 0.1765 | 0.1765 |
| **TOTAL PONDERADO** | **3.6471** | **2.9412** | **2.9412** |

Redondeando los resultados:

- **Concepto A = 3.65**
- **Concepto B = 2.94**
- **Concepto C = 2.94**

---

# 🏆 6. Selección del concepto

| Posición | Concepto | Puntuación ponderada | Resultado |
|---:|---|---:|---|
| **1** | **Concepto A (Base)** | **3.65** | ✅ **Seleccionado** |
| **2** | Concepto B | 2.94 | Alternativa secundaria |
| **2** | Concepto C | 2.94 | Alternativa secundaria |

El **Concepto A** se selecciona como alternativa base para el desarrollo del prototipo al obtener la mayor puntuación, con **32 puntos en la evaluación general y 3.65 en la evaluación ponderada**.

Este concepto presenta el mejor equilibrio entre:

- Precisión en la detección de grietas.
- Portabilidad.
- Facilidad de integración.
- Consumo energético.
- Autonomía.
- Facilidad de uso.
- Registro y almacenamiento de datos.
- Costo de implementación.
- Disponibilidad de componentes.

Los conceptos **B y C** obtuvieron **26 puntos** y una puntuación ponderada de **2.94**, por lo que ambos se consideran alternativas secundarias.

---

# ✅ Concepto seleccionado

A partir de la matriz morfológica y de la evaluación realizada, el concepto seleccionado incorpora principalmente las siguientes alternativas:

| Área | Alternativa seleccionada |
|---|---|
| Captura de imagen | XIAO ESP32S3 Sense |
| Geolocalización | GPS NEO-6M |
| Conectividad | Bluetooth |
| Protección | Carcasa impresa en 3D |
| Acceso interno | Tapa desmontable |
| Alimentación | Batería recargable Li-ion 18650 |
| Recarga | Cable |
| Control del sistema | XIAO ESP32S3 Sense |
| Inicio de captura | Botón físico |
| Iluminación | Interruptor |
| Gestión de ubicación | Activación manual |
| Confirmación de captura | LED indicador |
| Alerta | LED tipo semáforo |
| Estado del equipo | LED |
| Detección de grietas | Machine Learning |
| Información territorial | Base de datos pública |
| Relación grieta-zona | Sistema de puntuación |
| Clasificación de prioridad | Sistema de puntuación |
| Almacenamiento | Base de datos |
| Visualización | Dashboard web |

---
