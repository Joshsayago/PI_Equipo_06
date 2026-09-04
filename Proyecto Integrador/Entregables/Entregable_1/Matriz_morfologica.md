# MATRIZ MORFOLÓGICA – Sistema portátil de detección de grietas en concreto

## DOMINIO ELECTRÓNICO

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Capturar imagen de la grieta | XIAO ESP32S3 Sense <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/8f4ab4d8-d96a-42fa-b5cc-7df87db4aa45"/> | Maix Bit / Sipeed Maix <img width="60" height="60" alt="Captura de pantalla 2026-09-03 223432" src="https://github.com/user-attachments/assets/6212e3fb-fd45-49e0-b32d-51760935cfad" /> | Raspberry Pi Pico 2 W <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/196f62bf-c90d-4559-8e64-4b111396bd51" />|  
| Obtener geolocalización | GPS NEO-6M <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/dcc3301b-dab0-4a9a-a4f3-836da300a85e" /> | GPS NEO-M8N <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/14499908-f2f4-47cf-9900-db7a039209b8" />  | GPS del celular <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/a3654560-2ba1-435e-b3df-a3ec21311f68" />|
| Iluminar superficie | GPS NEO-6M <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/5dd4899f-3ccd-4473-a9b9-c87f24e1d419" /> | Flash LED <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/4fc22113-5ba1-4fb6-831f-df025c8d6717" />  | Aro LED <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/d519b753-b2d5-4ec6-b50a-306aa5d46482" /> |
| Conectividad | Wi-Fi <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/13c16e6e-2811-4c94-a986-48b75d142e60" />  | Bluetooth <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/89e3ffa2-53e2-4d02-8171-3d1f3dc3b0e0" />| USB <img width="60" height="60" alt="image" src="https://github.com/user-attachments/assets/0af8bf2c-0ca3-414e-857c-1a1cc658d256" />|

## DOMINIO MECÁNICO

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Proteger componentes | Carcasa impresa en 3D | Carcasa de acrílico | Caja plástica |
| Facilitar sujeción | Empuñadura ergonómica | Correa de mano | Carcasa de agarre directo |
| Mantener distancia de captura | Separadores frontales | Mar LG co frontal | Guía telescópica |
| Facilitar acceso interno | Tapa desmontable | Tapa con bisagra | Carcasa modular |

## DOMINIO DE ENERGÍA

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Alimentar el sistema | Batería recargable Li-ion 18650 | Batería recargable Li-Po | Power bank |
| Regular voltaje | Regulador integrado | Convertidor DC-DC | Módulo step-down |
| Recargar dispositivo | Cable | Cargador externo | Panel solar |

## DOMINIO DE CONTROL

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Controlar el sistema | XIAO ESP32S3 Sense | Maix Bit / Sipeed Maix | Raspberry Pi Pico 2 W |
| Iniciar captura | Pulsador físico | Aplicación móvil | Captura automática |
| Controlar iluminación | Activación automática | Interruptor | Control por software |
| Gestionar ubicación | Lectura automática del GPS | Activación manual | Ubicación desde celular |

## DOMINIO DE ACTUACIÓN

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Iluminar zona de captura | Aro LED | LED de alta intensidad | Flash LED |
| Confirmar captura | LED indicador | Buzzer | Vibración |
| Alertar al usuario | LED tipo semáforo | Buzzer | Notificación digital |
| Mostrar estado del equipo | LED tipo semáforo | LED RGB | Indicadores LED |

## DOMINIO DE SOFTWARE

| FUNCIONES PARCIALES | PORTADOR 1 | PORTADOR 2 | PORTADOR 3 |
| :--- | :--- | :--- | :--- |
| Detectar grietas | Procesamiento de imágenes | Machine Learning | Detección de bordes |
| Caracterizar grieta | Convertir píxeles a medidas | Escala milimetrada | Calibración por distancia |
| Obtener información territorial | Base de datos GEPM | Mapa de riesgo | API geográfica |
| Relacionar grieta y zona | Sistema de puntuación | Umbrales | Clasificación automática |
| Clasificar prioridad | Baja / media / alta | Sistema de puntuación | Porcentaje |
| Almacenar resultados | Base de datos | MicroSD | Memoria interna |
| Visualizar resultados | Dashboard web | Aplicación móvil | Pantalla integrada |

---

**Leyenda:**
* 1era opción (Amarillo)
* 2da opción (Verde)
* 3ra opción (Magenta)

---

## 1. Criterios de evaluación y pesos

| CRITERIOS | PESO |
| :--- | :--- |
| Precisión en detección de grietas | 0.20 |
| Caracterización de la grieta | 0.15 |
| Portabilidad | 0.10 |
| Facilidad de integración | 0.10 |
| Consumo energético | 0.10 |
| Autonomía | 0.10 |
| Facilidad de uso | 0.10 |
| Registro y almacenamiento de datos | 0.05 |
| Costo de implementación | 0.05 |
| Disponibilidad de componentes | 0.05 |
| **TOTAL** | **1** |

## 2. Evaluación de los conceptos
*0 = No satisface | 1 = Aceptable | 2 = Suficiente | 3 = Bien | 4 = Excelente*

| Criterio | C.S1 Concepto A | C.S2 Concepto B | C.S3 Concepto C |
| :--- | :--- | :--- | :--- |
| Precisión en detección de grietas | 4 | 3 | 3 |
| Caracterización de la grieta | 4 | 2 | 3 |
| Portabilidad | 4 | 3 | 3 |
| Facilidad de integración | 4 | 3 | 3 |
| Consumo energético | 3 | 3 | 2 |
| Autonomía | 3 | 3 | 4 |
| Facilidad de uso | 4 | 3 | 3 |
| Registro y almacenamiento de datos | 4 | 3 | 2 |
| Costo de implementación | 3 | 2 | 3 |
| Disponibilidad de componentes | 3 | 3 | 3 |
| **Suma total** | **36** | **28** | **29** |

**RESULTADO:**
* CONCEPTO A = 36 PUNTOS
* CONCEPTO C = 29 PUNTOS
* CONCEPTO B = 28 PUNTOS

## 3. Comparación respecto al Concepto A

| Criterio | Base (A) | B vs A | C vs A |
| :--- | :--- | :--- | :--- |
| Precisión en detección de grietas | 0 | -1 | -1 |
| Capacidad de caracterización | 0 | -2 | -1 |
| Portabilidad | 0 | -1 | -1 |
| Facilidad de integración | 0 | -1 | -1 |
| Consumo energético | 0 | 0 | -1 |
| Autonomía | 0 | 0 | +1 |
| Facilidad de uso | 0 | -1 | -1 |
| Registro y almacenamiento de datos | 0 | -1 | -2 |
| Costo de implementación | 0 | -1 | 0 |
| Disponibilidad de componentes | 0 | 0 | 0 |
| **Suma** | **0** | **-8** | **-7** |

* B - A = 28 - 36 = -8
* C - A = 29 - 36 = -7

## 4. Evaluación ponderada

| Criterio | Peso | Puntaje A | Puntaje B |
| :--- | :--- | :--- | :--- |
| Precisión en detección | 0.20 | 4 | 5 |
| Caracterización | 0.15 | 4 | 5 |
| Portabilidad | 0.10 | 5 | 4 |
| Facilidad de integración | 0.10 | 5 | 3 |
| Consumo energético | 0.10 | 4 | 3 |
| Autonomía | 0.10 | 4 | 3 |
| Facilidad de uso | 0.10 | 5 | 4 |
| Registro y almacenamiento | 0.05 | 5 | 4 |
| Costo de implementación | 0.05 | 4 | 3 |
| Disponibilidad de componentes | 0.05 | 5 | 3 |
| **TOTAL** | **1.00** | **4.40** | **3.95** |

## 5. Evaluación ponderada: Concepto C

| Criterio | Peso Concepto A (Base) | Peso x Concepto B | Peso x Concepto C |
| :--- | :--- | :--- | :--- |
| Precisión en detección | 0.80 | 1.00 | 0.60 |
| Caracterización | 0.60 | 0.75 | 0.45 |
| Portabilidad | 0.50 | 0.40 | 0.50 |
| Facilidad de integración | 0.50 | 0.30 | 0.40 |
| Consumo energético | 0.40 | 0.30 | 0.50 |
| Autonomía | 0.40 | 0.30 | 0.50 |
| Facilidad de uso | 0.50 | 0.40 | 0.40 |
| Registro y almacenamiento | 0.25 | 0.20 | 0.15 |
| Costo de implementación | 0.20 | 0.15 | 0.25 |
| Disponibilidad de componentes | 0.25 | 0.15 | 0.25 |
| **TOTAL PONDERADO** | **4.40** | **3.95** | **4.00** |

## 6. Selección del concepto

| Posición | Concepto | Puntuación ponderada | Resultado |
| :--- | :--- | :--- | :--- |
| 1 | Concepto A (Base) | 4.40 | Seleccionado |
| 2 | Concepto C | 4.00 | Alternativa secundaria |
| 3 | Concepto B | 3.95 | Alternativa secundaria |

Por lo tanto, se selecciona el Concepto A al obtener la mayor puntuación (36 puntos) como alternativa base para el desarrollo del prototipo, debido a que presenta el mejor equilibrio entre precisión en la detección, caracterización de la grieta, portabilidad, facilidad de integración, consumo energético, autonomía, facilidad de uso, registro de información, costo y disponibilidad de componentes.
