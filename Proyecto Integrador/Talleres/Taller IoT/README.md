# 🌐 Taller IoT — ESP32, MQTT, Node-RED y Sensores

<p align="center">
  <b>Implementación de un sistema IoT para monitoreo, visualización y control remoto</b>
</p>

<p align="center">
  ESP32 • MQTT • Node-RED • DHT11 • LM35 • Potenciómetro
</p>

---

## 📑 Contenido

1. [Objetivo](#-1-objetivo)
2. [Arquitectura general](#-2-arquitectura-general)
3. [Etapa 1 — Sistema con datos aleatorios](#-3-etapa-1--sistema-con-datos-aleatorios)
4. [Etapa 2 — Sistema con 3 sensores reales](#-4-etapa-2--sistema-con-3-sensores-reales)
5. [Comparación de ambas implementaciones](#-5-comparación-de-ambas-implementaciones)
6. [Resultados](#-6-resultados)
7. [Conclusiones](#-7-conclusiones)

---

# 🎯 1. Objetivo

El objetivo de la actividad fue desarrollar progresivamente un sistema IoT utilizando un **ESP32**, comunicación mediante **MQTT** y visualización mediante **Node-RED Dashboard**.

El desarrollo se dividió en dos etapas.

### 🎲 Etapa 1 — Datos aleatorios

Primero se implementó un sistema con valores generados desde el ESP32 para comprobar:

- conexión Wi-Fi;
- conexión con el broker MQTT;
- publicación de información;
- recepción de información en Node-RED;
- visualización de temperatura y humedad;
- control remoto de un LED.

### 🔬 Etapa 2 — Sensores reales

Después de comprobar la comunicación, el sistema fue ampliado utilizando:

- 🌡️ DHT11;
- 🌡️ LM35;
- 🎚️ potenciómetro;
- 💡 LED como actuador.

Finalmente, Node-RED fue utilizado para construir un dashboard más completo con indicadores, gráficas históricas, estado del sistema y control remoto.

---

# 🔗 2. Arquitectura general

La arquitectura utilizada fue:

```text
                ┌─────────────┐
                │    ESP32    │
                └──────┬──────┘
                       │
                     Wi-Fi
                       │
                       ▼
                ┌─────────────┐
                │ MQTT Broker │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │  Node-RED   │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │  Dashboard  │
                └─────────────┘
```

El ESP32 funciona como dispositivo encargado de generar o adquirir información.

MQTT permite transportar los mensajes entre el ESP32 y Node-RED.

Node-RED procesa la información recibida y finalmente el dashboard permite visualizarla de manera gráfica.

---

# 🎲 3. ETAPA 1 — Sistema con datos aleatorios

## 3.1 Objetivo de la primera implementación

Antes de conectar los sensores físicos se realizó una primera implementación utilizando valores de **temperatura y humedad generados por software**.

El propósito principal fue comprobar que toda la infraestructura IoT funcionara correctamente antes de aumentar la complejidad del sistema.

---

## 3.2 Generación de temperatura y humedad

En esta etapa el ESP32 generaba valores mediante:

```cpp
float tempSimulada = 24.0 + (random(0, 100) / 10.0);
float humSimulada = 55.0 + (random(0, 200) / 10.0);
```

Por lo tanto, los valores no correspondían todavía a mediciones físicas.

Estos datos fueron utilizados únicamente para probar el envío, recepción y representación de información.

---

## 3.3 Publicación mediante MQTT

El ESP32 construía un documento JSON con la identificación del dispositivo, temperatura y humedad.

La estructura utilizada fue equivalente a:

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.90,
  "humedad": 63.00
}
```

Posteriormente el mensaje era publicado mediante el tópico:

```text
equipo06/sensor/datos
```

Mientras que para el control del LED se utilizó:

```text
equipo06/actuadores/led
```

De esta manera se implementó comunicación en ambos sentidos:

```text
ESP32 ─────► MQTT ─────► Node-RED
  ▲                         │
  │                         │
  └──────── Control LED ◄───┘
```

---

## 3.4 Flujo inicial en Node-RED

Una vez enviados los mensajes MQTT se construyó el primer flujo en Node-RED.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8c02f9ec-9b40-4130-b26c-431951ed522e" width="700">
</p>

<p align="center">
  <i>Figura 1. Flujo inicial utilizado para recibir los datos mediante MQTT.</i>
</p>

El nodo MQTT recibe la información publicada por el ESP32.

Posteriormente los datos son separados para representar:

- 🌡️ temperatura;
- 💧 humedad;
- 🖥️ identificación del dispositivo.

También se implementó una ruta independiente para el control del LED.

---

## 3.5 Primer Dashboard

Después de configurar los nodos se creó un dashboard para representar los valores recibidos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/86d9f81d-5555-420e-b18c-9f76bd0f24b6" width="360">
</p>

<p align="center">
  <i>Figura 2. Dashboard de la primera implementación con datos generados por software.</i>
</p>

En la prueba mostrada se obtuvieron:

| Variable | Valor mostrado |
|---|---:|
| 🌡️ Temperatura | 27.9 °C |
| 💧 Humedad relativa | 63 % |

Los gauges permiten observar los valores de una manera más rápida que mediante datos numéricos aislados.

> **Importante:** estos valores corresponden a la etapa de prueba con datos generados y no deben interpretarse como mediciones de los sensores físicos.

---

## 3.6 Control remoto del LED

Además del monitoreo se implementó comunicación desde Node-RED hacia el ESP32.

El dashboard envía:

```text
ON
```

para encender el LED y:

```text
OFF
```

para apagarlo.

El ESP32 recibe el mensaje mediante el tópico:

```text
equipo06/actuadores/led
```

y modifica el estado del GPIO correspondiente.

---

## 3.7 Prueba física del actuador

El funcionamiento fue comprobado físicamente utilizando un LED conectado al ESP32.

<p align="center">
  <img src="https://github.com/user-attachments/assets/22875d73-a230-4c76-a5c7-53102dfe85af" width="300">
  &nbsp;&nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/ed799270-50f0-4c74-bbe8-1aab023db39e" width="300">
</p>

<p align="center">
  <i>Figura 3. Montaje utilizado durante la primera etapa y prueba del LED.</i>
</p>

La prueba permitió comprobar que el sistema no solamente podía **recibir información del ESP32**, sino también **enviar comandos desde Node-RED hacia el dispositivo físico**.

Esto demuestra una comunicación IoT bidireccional.

---

## 3.8 Resultado de la primera etapa

La primera implementación permitió verificar correctamente la cadena:

```text
Generación de datos
        ↓
      ESP32
        ↓
      Wi-Fi
        ↓
       MQTT
        ↓
     Node-RED
        ↓
     Dashboard
```

Además:

```text
Dashboard
    ↓
Node-RED
    ↓
 MQTT
    ↓
 ESP32
    ↓
  LED
```

Por lo tanto, antes de incorporar los sensores reales ya se había comprobado el funcionamiento de la comunicación y del control remoto.

---

# 🔬 4. ETAPA 2 — Sistema con 3 sensores reales

## 4.1 Evolución del sistema

Una vez validada la infraestructura IoT, los valores generados por software fueron reemplazados por información proveniente de sensores físicos.

Se incorporaron:

| Componente | Función |
|---|---|
| ESP32 | Procesamiento y comunicación |
| DHT11 | Temperatura y humedad |
| LM35 | Temperatura analógica |
| Potenciómetro | Entrada analógica variable |
| LED | Actuador remoto |
| Node-RED | Procesamiento y dashboard |
| MQTT | Comunicación |

Esto permitió transformar la prueba inicial en un sistema de adquisición de datos físicos.

---

## 4.2 Montaje físico completo

El circuito fue ampliado incorporando los sensores y el potenciómetro.

<p align="center">
  <img src="https://github.com/user-attachments/assets/a57a8f7a-773c-4b28-99c4-5b1595543fd7" width="300">
  &nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/a4f99271-a522-4416-a2b8-b723ad13782c" width="300">
</p>

<p align="center">
  <i>Figura 4. Implementación física del sistema con los sensores conectados al ESP32.</i>
</p>

El ESP32 pasó a adquirir información directamente de los dispositivos conectados en la protoboard.

---

# 🌡️ 4.3 Sensor DHT11

El DHT11 fue utilizado para obtener:

- temperatura ambiental;
- humedad relativa.

Se configuró mediante:

```cpp
#define DHT_PIN 4
#define DHT_TYPE DHT11

DHT dht(DHT_PIN, DHT_TYPE);
```

Las lecturas se realizan con:

```cpp
float tempDHT = dht.readTemperature();
float humDHT = dht.readHumidity();
```

También se incorporó una comprobación:

```cpp
if (isnan(tempDHT) || isnan(humDHT)) {
    Serial.println("Error leyendo el DHT11");
}
```

Esto evita interpretar como válidos datos incorrectos producidos por un fallo de lectura.

---

# 🌡️ 4.4 Sensor LM35

El LM35 proporciona una salida analógica relacionada con la temperatura.

Se conectó a:

```cpp
#define LM35_PIN 34
```

Primero se obtiene la lectura ADC:

```cpp
int lecturaLM35 = analogRead(LM35_PIN);
```

Luego se transforma a voltaje:

```cpp
float voltajeLM35 = lecturaLM35 * (3.3 / 4095.0);
```

Finalmente:

```cpp
float tempLM35 = voltajeLM35 * 100.0;
```

Por lo tanto:

```text
ADC
 ↓
Voltaje
 ↓
Temperatura LM35
```

---

# 🎚️ 4.5 Potenciómetro

El potenciómetro fue conectado a:

```cpp
#define POT_PIN 35
```

El ESP32 obtiene inicialmente un valor ADC mediante:

```cpp
int valorPot = analogRead(POT_PIN);
```

El rango esperado es aproximadamente:

```text
0 ───────────────────────── 4095
```

Para mostrarlo como voltaje en el dashboard se puede aplicar:

```text
Voltaje = ADC × 3.3 / 4095
```

Por ejemplo:

```text
ADC = 1840
```

entonces:

```text
V ≈ 1840 × 3.3 / 4095
V ≈ 1.48 V
```

Esto hace que la información mostrada sea más interpretable que presentar únicamente el valor ADC.

---

# 📦 4.6 JSON con los sensores reales

Con los sensores incorporados, el mensaje enviado mediante MQTT pasó a contener más variables.

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.0,
  "humedad": 65.0,
  "temperatura_lm35": 27.3,
  "potenciometro": 1840
}
```

Cada campo representa:

| Campo | Información |
|---|---|
| `dispositivo` | Identificación del ESP32 |
| `temperatura` | Temperatura DHT11 |
| `humedad` | Humedad DHT11 |
| `temperatura_lm35` | Temperatura LM35 |
| `potenciometro` | Lectura ADC |

---

# 🔀 4.7 Flujo avanzado en Node-RED

Node-RED fue ampliado para procesar todas las variables.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ec732bf6-f965-496a-8f3c-1f1fd47cc021" width="720">
</p>

<p align="center">
  <i>Figura 5. Flujo ampliado de Node-RED para el procesamiento de sensores y control del sistema.</i>
</p>

A diferencia del flujo inicial, esta versión incorpora procesamiento para:

```text
                    ┌──► Temperatura DHT11
                    │
                    ├──► Humedad
                    │
MQTT ─► Node-RED ───┼──► Temperatura LM35
                    │
                    ├──► Potenciómetro
                    │
                    ├──► Estado ambiental
                    │
                    ├──► Históricos
                    │
                    └──► Contador MQTT
```

Además se mantiene:

```text
Dashboard ─► MQTT ─► ESP32 ─► LED
```

---

# 🚀 4.8 Dashboard final — NEON IoT CONTROL CENTER

Para mejorar la presentación y facilitar la interpretación de la información se desarrolló un dashboard más completo.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e5efb0dd-2be5-46fc-acf1-a61354e02d07" width="780">
</p>

<p align="center">
  <i>Figura 6. Vista superior del dashboard final desarrollado en Node-RED.</i>
</p>

El dashboard incluye información numérica, gauges y gráficas históricas.

---

## 4.9 Temperatura y humedad

La primera zona permite visualizar:

- temperatura;
- humedad relativa;
- historial de temperatura;
- historial de humedad.

Los históricos permiten analizar no solamente el valor instantáneo, sino también cómo cambia la variable con el tiempo.

Esto representa una mejora importante respecto al dashboard inicial.

---

# ⚡ 4.10 Voltaje del potenciómetro

El dashboard muestra el potenciómetro en unidades de voltaje.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8a850cd9-450b-4814-8de3-babcf2592bc2" width="780">
</p>

<p align="center">
  <i>Figura 7. Visualización del potenciómetro y temperatura LM35.</i>
</p>

El gauge trabaja aproximadamente entre:

```text
0 V ───────────────────────── 3.3 V
```

Además se incorporó una gráfica histórica.

```text
Valor actual
     +
Gauge
     +
Historial
```

Esto permite observar tanto el estado instantáneo como las variaciones de la entrada analógica.

---

# 🌡️ 4.11 Temperatura del LM35

El LM35 cuenta con su propio:

- valor digital;
- gauge;
- historial temporal.

Esto permite comparar posteriormente la lectura de temperatura obtenida por el LM35 con la obtenida mediante el DHT11.

---

# 📈 4.12 Gráficas históricas

Una de las mejoras más importantes del dashboard final fue la incorporación de históricos.

Se implementaron gráficas para:

### 🌡️ Temperatura

Permite analizar la evolución de la temperatura en el tiempo.

### 💧 Humedad

Permite observar variaciones en la humedad relativa.

### 🎚️ Potenciómetro

Permite observar inmediatamente los cambios realizados manualmente en el potenciómetro.

### 🌡️ LM35

Permite observar la evolución de la temperatura medida mediante el sensor analógico.

Los históricos son importantes porque una medición IoT no necesariamente debe limitarse a mostrar el **valor actual**.

También resulta útil conocer:

```text
Valor actual + comportamiento temporal
```

---

# 🚦 4.13 Estado ambiental

Se agregó un indicador de estado para interpretar rápidamente las condiciones recibidas.

Por ejemplo:

```text
🟢 ESTABLE
```

De esta manera, el usuario no necesita interpretar individualmente cada número para obtener una indicación general del sistema.

---

# 📡 4.14 Contador de paquetes MQTT

También se incorporó un contador de mensajes MQTT recibidos.

Este elemento permite verificar visualmente que el sistema continúa recibiendo información.

Por ejemplo:

```text
📡 Paquetes MQTT: 145
```

Si el contador aumenta continuamente, significa que Node-RED continúa recibiendo publicaciones.

Esto funciona también como una herramienta básica de diagnóstico.

---

# ⏱️ 4.15 Última actualización

El dashboard muestra la hora correspondiente al último dato procesado.

Ejemplo:

```text
Último dato: 19:28:39
```

Esto permite identificar si los datos mostrados son recientes o si la comunicación dejó de actualizarse.

---

# 💡 4.16 Control del LED

El control del actuador se mantuvo en el dashboard avanzado.

El funcionamiento es:

```text
Usuario
   ↓
Switch Node-RED
   ↓
MQTT
   ↓
ESP32
   ↓
LED
```

Por lo tanto, el sistema integra dos características fundamentales de IoT:

```text
MONITOREO + CONTROL
```

---

# 🔧 4.17 Flujo completo del sistema

La versión final puede resumirse mediante:

```text
              ┌──────── DHT11
              │
              ├──────── LM35
              │
              └──────── Potenciómetro
                       │
                       ▼
                    ESP32
                       │
                     Wi-Fi
                       │
                       ▼
                 Broker MQTT
                       │
                       ▼
                   Node-RED
                       │
       ┌───────────────┼────────────────┐
       │               │                │
       ▼               ▼                ▼
    Gauges         Históricos       Indicadores
       │               │                │
       └───────────────┼────────────────┘
                       ▼
                    Usuario
                       │
                       ▼
                  Control LED
                       │
                       ▼
                     MQTT
                       │
                       ▼
                     ESP32
```

---

# ⚖️ 5. Comparación de ambas implementaciones

Después de completar ambas etapas se pueden observar claramente las mejoras realizadas.

| Característica | 🎲 Datos aleatorios | 🔬 3 sensores reales |
|---|---|---|
| ESP32 | ✅ | ✅ |
| Wi-Fi | ✅ | ✅ |
| MQTT | ✅ | ✅ |
| Node-RED | ✅ | ✅ |
| Temperatura | Generada | DHT11 + LM35 |
| Humedad | Generada | DHT11 |
| Potenciómetro | ❌ | ✅ |
| LM35 | ❌ | ✅ |
| Control LED | ✅ | ✅ |
| Gauge temperatura | ✅ | ✅ |
| Gauge humedad | ✅ | ✅ |
| Gauge LM35 | ❌ | ✅ |
| Gauge voltaje | ❌ | ✅ |
| Históricos | Básicos/no principales | ✅ |
| Estado ambiental | ❌ | ✅ |
| Última actualización | ❌ | ✅ |
| Contador MQTT | ❌ | ✅ |
| Complejidad | Baja | Mayor |

---

## 5.1 Diferencia fundamental

La diferencia principal entre ambas etapas está en el **origen de los datos**.

### Primera implementación

```text
Software
   ↓
Valores generados
   ↓
MQTT
   ↓
Dashboard
```

### Implementación final

```text
Entorno físico
     ↓
  Sensores
     ↓
    ESP32
     ↓
    MQTT
     ↓
  Node-RED
     ↓
 Dashboard
```

La primera etapa fue útil para validar la infraestructura.

La segunda permitió comprobar el funcionamiento del sistema con variables adquiridas físicamente.

---

# 📊 6. Resultados

Durante el desarrollo se logró:

- establecer comunicación Wi-Fi con el ESP32;
- establecer comunicación MQTT;
- publicar información desde el ESP32;
- recibir mensajes en Node-RED;
- representar temperatura;
- representar humedad;
- adquirir temperatura mediante LM35;
- adquirir información analógica mediante potenciómetro;
- convertir la lectura del potenciómetro a voltaje para el dashboard;
- implementar gauges;
- implementar gráficas históricas;
- mostrar la última actualización;
- contar paquetes MQTT;
- incorporar un indicador de estado ambiental;
- controlar un LED remotamente.

---

## 6.1 Evolución obtenida

El desarrollo siguió una estrategia incremental:

```text
1. ESP32
       ↓
2. Wi-Fi
       ↓
3. MQTT
       ↓
4. Datos generados
       ↓
5. Node-RED
       ↓
6. Dashboard básico
       ↓
7. Control LED
       ↓
8. Sensores físicos
       ↓
9. Procesamiento adicional
       ↓
10. Dashboard avanzado
```

Esta metodología permitió probar cada componente antes de avanzar hacia una implementación de mayor complejidad.

---

# 🧠 7. Conclusiones

1. Se logró implementar correctamente una arquitectura IoT basada en **ESP32, Wi-Fi, MQTT y Node-RED**, permitiendo transmitir y visualizar información mediante un dashboard.

2. La utilización inicial de datos aleatorios permitió validar la comunicación antes de incorporar los sensores físicos, facilitando la identificación de posibles problemas en cada etapa.

3. Posteriormente se integraron **DHT11, LM35 y potenciómetro**, permitiendo reemplazar los datos generados por mediciones obtenidas directamente del montaje.

4. El DHT11 permitió obtener temperatura y humedad, mientras que el LM35 proporcionó una segunda medición de temperatura mediante una señal analógica.

5. La lectura del potenciómetro fue procesada para representar su comportamiento mediante voltaje, facilitando la interpretación del dato analógico.

6. Node-RED permitió no solamente visualizar valores instantáneos, sino también incorporar gauges, históricos, indicadores de estado, contador de paquetes y hora de actualización.

7. El control del LED demuestra que la comunicación implementada es bidireccional: el ESP32 puede enviar información al dashboard y, al mismo tiempo, recibir órdenes desde Node-RED.

8. La evolución desde un dashboard básico hasta un sistema con sensores físicos permitió demostrar de forma progresiva los principales conceptos de un sistema IoT: **adquisición, comunicación, procesamiento, visualización y actuación**.

---

# 🚀 Resultado final

```text
┌──────────────────────────────────────────────────────┐
│                SISTEMA IoT — EQUIPO 06               │
├──────────────────────────────────────────────────────┤
│                                                      │
│  🌡️ DHT11             Temperatura + Humedad          │
│  🌡️ LM35              Temperatura analógica          │
│  🎚️ Potenciómetro      Entrada analógica / voltaje    │
│  💡 LED                Actuador remoto                │
│                                                      │
│  📡 MQTT               Comunicación                  │
│  🔀 Node-RED           Procesamiento                 │
│  📊 Dashboard          Monitoreo en tiempo real      │
│                                                      │
└──────────────────────────────────────────────────────┘
```

<p align="center">
  <b>ESP32 + MQTT + Node-RED = Sistema IoT de monitoreo y control</b>
</p>
