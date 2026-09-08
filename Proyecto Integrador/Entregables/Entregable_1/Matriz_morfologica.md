# 🧩 Matriz Morfológica

La **matriz morfológica** permite generar y comparar diferentes alternativas de solución para las funciones parciales del sistema portátil de detección de grietas en concreto.

Para la generación de conceptos se consideraron tres alternativas:

- 🟨 **Concepto A — Primera opción**
- 🟩 **Concepto B — Segunda opción**
- 🟪 **Concepto C — Tercera opción**

---

## 🔌 Dominio electrónico

<p align="center">
  <img width="695" height="710" alt="Matriz morfológica - Dominio electrónico" src="https://github.com/user-attachments/assets/f3ea47bd-406d-4914-8b9c-c8a208962ce8" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
|---|---|---|---|
| Capturar imagen de la grieta | XIAO ESP32S3 Sense | Maix Bit / Sipeed Maix | Raspberry Pi Pico 2 W |
| Obtener geolocalización | GPS NEO-6M | GPS NEO-M8N | GPS del celular |
| Conectividad | Bluetooth | Wi-Fi | USB |

---

## 🛠️ Dominio mecánico

<p align="center">
  <img width="701" height="518" alt="Matriz morfológica - Dominio mecánico" src="https://github.com/user-attachments/assets/a96f839b-ad8b-4eaf-bdfd-ffd8904f462a" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
|---|---|---|---|
| Proteger componentes | Carcasa impresa en 3D | Carcasa de acrílico | Caja plástica |
| Facilitar acceso interno | Tapa desmontable | Tapa con bisagra | Carcasa modular |

---

## 🔋 Dominio de energía

<p align="center">
  <img width="690" height="512" alt="Matriz morfológica - Dominio de energía" src="https://github.com/user-attachments/assets/bf04f2dc-c7e0-4b36-9210-bf67bdad8745" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
|---|---|---|---|
| Alimentar el sistema | Batería recargable Li-ion 18650 | Batería recargable Li-Po | Power bank |
| Recargar dispositivo | Cable | Panel solar | Cargador externo |

---

## 🎛️ Dominio de control

<p align="center">
  <img width="697" height="957" alt="Matriz morfológica - Dominio de control" src="https://github.com/user-attachments/assets/e6965d53-7b8c-46da-ae1c-a46ae9ff7f83" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
|---|---|---|---|
| Controlar el sistema | XIAO ESP32S3 Sense | Maix Bit / Sipeed Maix | Raspberry Pi Pico 2 W |
| Iniciar captura | Botón físico | Aplicación móvil | Captura automática |
| Controlar iluminación | Interruptor | Control por software | Activación automática |
| Gestionar ubicación | Activación manual | Lectura automática del GPS | Ubicación desde celular |

---

## 🚨 Dominio de actuación

<p align="center">
  <img width="676" height="682" alt="Matriz morfológica - Dominio de actuación" src="https://github.com/user-attachments/assets/cedae156-b678-4ceb-8c10-e45bd7b78d97" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
|---|---|---|---|
| Confirmar captura | LED indicador | Buzzer | Vibración |
| Alertar al usuario | LED tipo semáforo | Buzzer | Notificación digital |
| Mostrar estado del equipo | LED | Indicadores LED | LED RGB |

---

## 💻 Dominio de software

<p align="center">
  <img width="696" height="968" alt="Matriz morfológica - Dominio de software" src="https://github.com/user-attachments/assets/8a8fadc9-cfb2-49c7-b8b2-c36bba7d7894" />
</p>

| Función parcial | Concepto A 🟨 | Concepto B 🟩 | Concepto C 🟪 |
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

Para evaluar las alternativas generadas se establecieron criterios relacionados con el desempeño, funcionamiento y viabilidad del sistema.

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

### Evaluación

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

### Resultado

- 🥇 **Concepto A = 32 puntos**
- **Concepto B = 26 puntos**
- **Concepto C = 26 puntos**

---

## 3. Comparación respecto al Concepto A

Se tomó el **Concepto A** como alternativa base para realizar la comparación con los conceptos B y C.

| Criterio | Base (A) | B vs A | C vs A |
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

### Diferencia respecto al concepto base

**B − A = 26 − 32 = −6**

**C − A = 26 − 32 = −6**

---

## 4. Evaluación ponderada

La evaluación ponderada permite considerar la importancia relativa de cada criterio mediante los pesos establecidos.

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

Para obtener la puntuación ponderada se multiplicó el peso asignado a cada criterio por el puntaje obtenido por cada concepto.

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

### Resultados finales

- **Concepto A = 3.65**
- **Concepto B = 2.94**
- **Concepto C = 2.94**

---

## 🏆 6. Selección del concepto

| Posición | Concepto | Puntuación ponderada | Resultado |
|---:|---|---:|---|
| **1** | **Concepto A (Base)** | **3.65** | ✅ **Seleccionado** |
| **2** | Concepto B | 2.94 | Alternativa secundaria |
| **2** | Concepto C | 2.94 | Alternativa secundaria |

El **Concepto A** fue seleccionado como alternativa base para el desarrollo del prototipo al obtener la mayor puntuación, con **32 puntos en la evaluación general y 3.65 en la evaluación ponderada**.

Este concepto presenta el mejor equilibrio entre precisión en la detección de grietas, portabilidad, facilidad de integración, consumo energético, autonomía, facilidad de uso, registro y almacenamiento de datos, costo de implementación y disponibilidad de componentes.

Los conceptos **B y C** obtuvieron **26 puntos** y una puntuación ponderada de **2.94**, por lo que ambos se consideran alternativas secundarias.

---

## ✅ Configuración del concepto seleccionado

| Función | Alternativa seleccionada |
|---|---|
| Capturar imagen de la grieta | XIAO ESP32S3 Sense |
| Obtener geolocalización | GPS NEO-6M |
| Conectividad | Bluetooth |
| Proteger componentes | Carcasa impresa en 3D |
| Facilitar acceso interno | Tapa desmontable |
| Alimentar el sistema | Batería recargable Li-ion 18650 |
| Recargar dispositivo | Cable |
| Controlar el sistema | XIAO ESP32S3 Sense |
| Iniciar captura | Botón físico |
| Controlar iluminación | Interruptor |
| Gestionar ubicación | Activación manual |
| Confirmar captura | LED indicador |
| Alertar al usuario | LED tipo semáforo |
| Mostrar estado del equipo | LED |
| Detectar grietas | Machine Learning |
| Obtener información territorial | Base de datos pública |
| Relacionar grieta y zona | Sistema de puntuación |
| Clasificar prioridad | Sistema de puntuación |
| Almacenar resultados | Base de datos |
| Visualizar resultados | Dashboard web |

---
