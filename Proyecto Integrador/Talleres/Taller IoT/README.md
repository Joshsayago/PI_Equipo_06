# 🌐 Sistema IoT con ESP32, MQTT y Node-RED

<p align="center">
  <b>Equipo 06 — Implementación, monitoreo y control de sensores mediante MQTT</b>
</p>

<p align="center">
  ESP32 • MQTT • Node-RED • DHT11 • LM35 • Potenciómetro • Dashboard 2.0
</p>

---

## 📑 Índice

1. [Introducción](#1-introducción)
2. [Objetivos](#2-objetivos)
3. [Arquitectura general](#3-arquitectura-general)
4. [Etapa 1: sistema con datos aleatorios](#4-etapa-1-sistema-con-datos-aleatorios)
5. [Etapa 2: implementación con sensores reales](#5-etapa-2-implementación-con-sensores-reales)
6. [Procesamiento en Node-RED](#6-procesamiento-en-node-red)
7. [Dashboard final](#7-dashboard-final)
8. [Comparación de ambas etapas](#8-comparación-de-ambas-etapas)
9. [Resultados y análisis](#9-resultados-y-análisis)
10. [Conclusiones](#10-conclusiones)
11. [Posibles mejoras](#11-posibles-mejoras)

---

# 1. Introducción

En este trabajo se desarrolló un sistema de **Internet de las Cosas (IoT)** utilizando un microcontrolador **ESP32**, comunicación mediante el protocolo **MQTT** y la plataforma **Node-RED** para el procesamiento y visualización de información.

La implementación se realizó progresivamente en dos etapas.

La primera etapa tuvo como objetivo comprobar el funcionamiento de la comunicación entre el ESP32, el broker MQTT y Node-RED. Para ello se generaron valores simulados de temperatura y humedad.

Posteriormente, el sistema fue ampliado mediante la incorporación de sensores físicos:

- 🌡️ DHT11 para temperatura y humedad.
- 🌡️ LM35 para una segunda medición de temperatura.
- 🎚️ Potenciómetro como entrada analógica.
- 💡 LED como actuador controlado remotamente.

Finalmente, se desarrolló un dashboard de monitoreo con indicadores, gráficas históricas, estado del sistema y control remoto del actuador.

> **Importante:** los datos de la primera etapa son simulados. Los datos de la segunda etapa provienen de sensores conectados físicamente al ESP32.

---

# 2. Objetivos

## 2.1 Objetivo general

Implementar un sistema IoT capaz de adquirir, transmitir, procesar y visualizar información mediante un ESP32, MQTT y Node-RED, incorporando posteriormente sensores físicos y control remoto de un actuador.

## 2.2 Objetivos específicos

- Establecer la conexión del ESP32 a una red Wi-Fi.
- Establecer comunicación entre el ESP32 y un broker MQTT.
- Publicar información mediante un tópico MQTT.
- Recibir comandos desde Node-RED.
- Visualizar temperatura y humedad mediante un dashboard.
- Implementar un DHT11, LM35 y potenciómetro.
- Convertir la lectura analógica del potenciómetro a voltios.
- Mostrar datos actuales e históricos.
- Controlar un LED remotamente mediante MQTT.
- Comparar el prototipo con datos simulados frente a la implementación con sensores físicos.

---

# 3. Arquitectura general

El funcionamiento general implementado fue:

```text
                    ┌───────────────┐
                    │    Sensores   │
                    │ DHT11 / LM35  │
                    │ Potenciómetro │
                    └───────┬───────┘
                            │
                            ▼
                      ┌───────────┐
                      │   ESP32   │
                      └─────┬─────┘
                            │
                         Wi-Fi
                            │
                            ▼
                      ┌───────────┐
                      │   MQTT    │
                      │  Broker   │
                      └─────┬─────┘
                            │
                            ▼
                      ┌───────────┐
                      │ Node-RED  │
                      └─────┬─────┘
                            │
             ┌──────────────┴─────────────┐
             ▼                            ▼
      ┌─────────────┐              ┌─────────────┐
      │  Dashboard  │              │ Control LED │
      └─────────────┘              └──────┬──────┘
                                          │
                                          ▼
                                     MQTT → ESP32
```

Por lo tanto, el sistema permite comunicación en ambos sentidos:

**Sensores → ESP32 → MQTT → Node-RED → Dashboard**

y:

**Dashboard → Node-RED → MQTT → ESP32 → LED**

Esto permite que el proyecto no se limite únicamente al monitoreo, sino que también incorpore **control remoto de actuadores**.

---

# 4. Etapa 1: sistema con datos aleatorios

## 4.1 Objetivo de la primera etapa

Antes de conectar todos los sensores físicos se desarrolló una versión inicial para comprobar la comunicación completa del sistema.

En esta etapa, el ESP32 generaba valores simulados de:

- temperatura;
- humedad.

Estos valores eran publicados mediante MQTT y recibidos posteriormente por Node-RED.

La ventaja de esta estrategia fue poder comprobar primero la infraestructura de comunicación antes de añadir la complejidad de los sensores físicos.

---

## 4.2 Montaje inicial

En el primer prototipo se utilizó principalmente:

- ESP32;
- protoboard;
- LED;
- resistencia;
- cables de conexión;
- conexión Wi-Fi.

<p align="center">
<img src="https://github.com/user-attachments/assets/e48f66fa-3115-4a2b-8f16-4b6a6582c6e3" width="270">
&nbsp;&nbsp;
<img src="https://github.com/user-attachments/assets/199e9b38-fb9f-4b30-9b62-f7c40f703974" width="270">
</p>

<p align="center">
<i>Figura 1. Montaje utilizado durante la etapa inicial del sistema.</i>
</p>

Como referencia para la conexión de actuadores se consideró la utilización de resistencias limitadoras de corriente en serie con los LED.

<p align="center">
<img src="https://github.com/user-attachments/assets/6a959981-5147-4a32-95af-d8af870a2b93" width="650">
</p>

<p align="center">
<i>Figura 2. Referencia de conexión de LED con ESP32 y resistencias.</i>
</p>

---

## 4.3 Generación de datos simulados

La temperatura y humedad se generaron mediante:

```cpp
float tempSimulada = 24.0 + (random(0, 100) / 10.0);
float humSimulada = 55.0 + (random(0, 200) / 10.0);
```

Con esto se obtuvieron valores variables que permitieron comprobar si el dashboard reaccionaba correctamente ante nuevas mediciones.

El JSON enviado tenía una estructura equivalente a:

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.9,
  "humedad": 63.0
}
```

---

## 4.4 Publicación mediante MQTT

Se utilizó el tópico:

```text
equipo06/sensor/datos
```

El ESP32 publicaba periódicamente el JSON y Node-RED permanecía suscrito a dicho tópico.

De esta manera, cada publicación seguía aproximadamente el recorrido:

```text
ESP32
   ↓
Wi-Fi
   ↓
Broker MQTT
   ↓
equipo06/sensor/datos
   ↓
Node-RED
   ↓
Dashboard
```

---

## 4.5 Flujo inicial en Node-RED

Una vez recibida la información mediante MQTT, el mensaje se dividió para obtener individualmente:

- `temperatura`
- `humedad`
- `dispositivo`

<p align="center">
<img src="https://github.com/user-attachments/assets/acac188c-eb9b-41ac-9aa3-3b44faf711f6" width="760">
</p>

<p align="center">
<i>Figura 3. Flujo inicial de Node-RED utilizado con temperatura y humedad simuladas.</i>
</p>

Los valores eran enviados posteriormente a indicadores gráficos del dashboard.

---

## 4.6 Dashboard de la etapa aleatoria

El dashboard inicial permitió visualizar los valores generados por el ESP32.

<p align="center">
<img src="https://github.com/user-attachments/assets/48637115-a6c4-489b-8a49-a3aa9fb240bd" width="390">
</p>

<p align="center">
<i>Figura 4. Dashboard correspondiente a la etapa de datos simulados.</i>
</p>

En la captura se observan, por ejemplo:

- Temperatura: **27.9 °C**
- Humedad relativa: **63 %**

La función de esta primera interfaz no fue realizar una medición física del ambiente, sino comprobar que:

1. el ESP32 podía conectarse correctamente;
2. los datos podían publicarse mediante MQTT;
3. Node-RED recibía los mensajes;
4. los valores podían separarse;
5. el dashboard se actualizaba correctamente.

---

## 4.7 Control remoto del LED

Además del envío de datos, se implementó comunicación en sentido contrario.

El dashboard enviaba comandos hacia:

```text
equipo06/actuadores/led
```

Los mensajes utilizados fueron:

```text
ON
OFF
```

El ESP32 permanecía suscrito al tópico y ejecutaba:

```cpp
if (mensaje == "ON") {
    digitalWrite(2, HIGH);
}
else if (mensaje == "OFF") {
    digitalWrite(2, LOW);
}
```

Esto permitió comprobar una característica fundamental de IoT: la comunicación **bidireccional**.

---

## 4.8 Código de la etapa con datos aleatorios

> 🔐 Las credenciales privadas se muestran como campos genéricos para evitar publicar contraseñas en un repositorio público.

```cpp
#include <WiFi.h>
#include <PubSubClient.h>
#include <ArduinoJson.h>

// ================= WIFI =================

const char* WIFI_SSID = "TU_RED_WIFI";
const char* WIFI_PASS = "TU_PASSWORD_WIFI";

// ================= MQTT =================

const char* MQTT_SERVER = "mqtt.rcr-labs.com";
const int MQTT_PORT = 1883;

const char* MQTT_USER = "TU_USUARIO_MQTT";
const char* MQTT_PASSWORD = "TU_PASSWORD_MQTT";

const char* CLIENT_ID = "ESP32_Equipo06";

const char* TOPIC_PUB = "equipo06/sensor/datos";
const char* TOPIC_SUB = "equipo06/actuadores/led";

WiFiClient espClient;
PubSubClient client(espClient);

unsigned long ultimoEnvio = 0;
const long intervaloEnvio = 5000;

// ================= WIFI =================

void setupWiFi() {

  delay(10);

  Serial.println();
  Serial.print("Conectando a Wi-Fi: ");
  Serial.println(WIFI_SSID);

  WiFi.mode(WIFI_STA);
  WiFi.begin(WIFI_SSID, WIFI_PASS);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nWiFi conectado con éxito");
  Serial.print("Dirección IP local: ");
  Serial.println(WiFi.localIP());
}

// ================= MQTT CALLBACK =================

void callback(char* topic, byte* payload, unsigned int length) {

  String mensaje = "";

  for (unsigned int i = 0; i < length; i++) {
    mensaje += (char)payload[i];
  }

  Serial.print("Mensaje recibido: ");
  Serial.println(mensaje);

  if (String(topic) == TOPIC_SUB) {

    if (mensaje == "ON") {
      digitalWrite(2, HIGH);
      Serial.println("LED encendido");
    }

    else if (mensaje == "OFF") {
      digitalWrite(2, LOW);
      Serial.println("LED apagado");
    }
  }
}

// ================= RECONEXIÓN MQTT =================

void reconnect() {

  while (!client.connected()) {

    Serial.print("Intentando conectar con MQTT...");

    if (client.connect(CLIENT_ID, MQTT_USER, MQTT_PASSWORD)) {

      Serial.println("Conectado");

      client.subscribe(TOPIC_SUB);

    } else {

      Serial.print("Error: ");
      Serial.println(client.state());

      delay(5000);
    }
  }
}

// ================= SETUP =================

void setup() {

  Serial.begin(115200);

  pinMode(2, OUTPUT);

  setupWiFi();

  client.setServer(MQTT_SERVER, MQTT_PORT);
  client.setCallback(callback);
}

// ================= LOOP =================

void loop() {

  if (!client.connected()) {
    reconnect();
  }

  client.loop();

  unsigned long ahora = millis();

  if (ahora - ultimoEnvio >= intervaloEnvio) {

    ultimoEnvio = ahora;

    float tempSimulada =
        24.0 + (random(0, 100) / 10.0);

    float humSimulada =
        55.0 + (random(0, 200) / 10.0);

    StaticJsonDocument<200> doc;

    doc["dispositivo"] = CLIENT_ID;
    doc["temperatura"] = tempSimulada;
    doc["humedad"] = humSimulada;

    char jsonBuffer[256];

    serializeJson(doc, jsonBuffer);

    Serial.println(jsonBuffer);

    client.publish(TOPIC_PUB, jsonBuffer);
  }
}
```

---

# 5. Etapa 2: implementación con sensores reales

Una vez validada la comunicación, se pasó a una implementación de mayor complejidad utilizando sensores físicos.

Se incorporaron:

| Elemento | Variable | Función |
|---|---|---|
| DHT11 | `temperatura` | Temperatura ambiental |
| DHT11 | `humedad` | Humedad relativa |
| LM35 | `temperatura_lm35` | Segunda medición de temperatura |
| Potenciómetro | `potenciometro` | Entrada analógica variable |
| LED | `ON/OFF` | Actuador remoto |

---

## 5.1 Montaje final

<p align="center">
<img src="https://github.com/user-attachments/assets/c9f04c4b-5ad1-4333-83e1-f79f927703b5" width="300">
&nbsp;&nbsp;
<img src="https://github.com/user-attachments/assets/0160b023-b9f5-4b36-bc2f-137eeb9f8233" width="300">
</p>

<p align="center">
<i>Figura 5. Implementación física del sistema con los sensores conectados al ESP32.</i>
</p>

En esta etapa el ESP32 dejó de depender de valores simulados y comenzó a adquirir información directamente de las entradas físicas.

---

## 5.2 DHT11

El DHT11 se utilizó para medir simultáneamente:

```text
Temperatura → °C
Humedad     → %
```

La lectura se realizó mediante:

```cpp
float tempDHT = dht.readTemperature();
float humDHT = dht.readHumidity();
```

También se incorporó una comprobación para evitar procesar una lectura inválida:

```cpp
if (isnan(tempDHT) || isnan(humDHT)) {
    Serial.println("Error leyendo el DHT11");
}
```

---

## 5.3 Sensor LM35

El LM35 proporciona una señal analógica relacionada con la temperatura.

Primero se obtiene la lectura del ADC:

```cpp
int lecturaLM35 = analogRead(LM35_PIN);
```

Posteriormente se convierte a voltaje:

```cpp
float voltajeLM35 =
    lecturaLM35 * (3.3 / 4095.0);
```

Finalmente:

```cpp
float tempLM35 =
    voltajeLM35 * 100.0;
```

Por lo tanto:

\[
V = ADC\left(\frac{3.3}{4095}\right)
\]

y, bajo la conversión empleada:

\[
T = V(100)
\]

El resultado se expresa en °C.

---

## 5.4 Potenciómetro

El potenciómetro fue conectado a:

```cpp
#define POT_PIN 35
```

La lectura original se obtiene mediante:

```cpp
int valorPot = analogRead(POT_PIN);
```

El ADC del ESP32 entrega un valor digital que posteriormente puede transformarse a voltaje.

En Node-RED se utilizó:

\[
V_{pot} =
ADC\left(\frac{3.3}{4095}\right)
\]

Por ejemplo, una lectura aproximada de:

```text
2378
```

corresponde aproximadamente a:

\[
V =
2378\left(\frac{3.3}{4095}\right)
\approx 1.916\ V
\]

De esta forma, el dashboard muestra directamente una magnitud física más fácil de interpretar.

---

# 6. Procesamiento en Node-RED

La segunda versión del flujo aumentó considerablemente su complejidad.

<p align="center">
<img src="https://github.com/user-attachments/assets/318ddfe2-8cbd-42fd-9a60-d1192050ade2" width="820">
</p>

<p align="center">
<i>Figura 6. Flujo final de Node-RED con procesamiento de los sensores.</i>
</p>

El nodo MQTT recibe toda la información mediante:

```text
equipo06/sensor/datos
```

Un mensaje puede presentar la siguiente estructura:

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.0,
  "humedad": 65.0,
  "temperatura_lm35": 27.3,
  "potenciometro": 1840
}
```

A partir de un único mensaje MQTT, Node-RED procesa diferentes ramas.

### DHT11

```text
JSON
 ├── temperatura
 └── humedad
```

### LM35

```text
temperatura_lm35
        ↓
Procesamiento
        ↓
Indicador + Gauge + Historial
```

### Potenciómetro

```text
potenciometro
       ↓
Conversión ADC → V
       ↓
Valor + Gauge + Historial
```

### Información adicional

También se incorporaron funciones para:

- estado ambiental;
- última actualización;
- contador de paquetes MQTT;
- identificación del dispositivo;
- control del LED.

---

# 7. Dashboard final

Para mejorar la presentación se desarrolló una interfaz con estética tecnológica/futurista denominada:

# ⚡ NEON IoT CONTROL CENTER

<p align="center">
<img src="https://github.com/user-attachments/assets/117795d1-872a-4c18-a4a2-cc342e7e53db" width="900">
</p>

<p align="center">
<i>Figura 7. Vista principal del dashboard final.</i>
</p>

El dashboard muestra simultáneamente:

- 🌡️ temperatura DHT11;
- 💧 humedad relativa;
- 📈 historial de temperatura;
- 📈 historial de humedad;
- 🚦 estado ambiental;
- ⏱️ hora de la última actualización;
- 📡 número de paquetes MQTT recibidos;
- 💻 dispositivo conectado;
- 💡 control remoto del LED.

---

## 7.1 Visualización del potenciómetro y LM35

La segunda zona del dashboard incorpora las variables analógicas.

<p align="center">
<img src="https://github.com/user-attachments/assets/318ddfe2-8cbd-42fd-9a60-d1192050ade2" width="900">
</p>

> En caso de utilizar esta misma captura también como evidencia del flujo, puede sustituirse aquí posteriormente por la captura específica del dashboard de potenciómetro/LM35.

El dashboard diseñado permite representar:

### Potenciómetro

- valor instantáneo en voltios;
- gauge de **0 a 3.3 V**;
- gráfica histórica del voltaje.

### LM35

- temperatura instantánea;
- gauge en °C;
- historial de temperatura.

Esta incorporación permite observar no solo el valor actual sino también su **comportamiento temporal**.

---

# 8. Código de los tres sensores

```cpp
#include <WiFi.h>
#include <PubSubClient.h>
#include <ArduinoJson.h>
#include <DHT.h>

// ================= WIFI =================

const char* WIFI_SSID = "TU_RED_WIFI";
const char* WIFI_PASS = "TU_PASSWORD_WIFI";

// ================= MQTT =================

const char* MQTT_SERVER = "mqtt.rcr-labs.com";
const int MQTT_PORT = 1883;

const char* MQTT_USER = "TU_USUARIO_MQTT";
const char* MQTT_PASSWORD = "TU_PASSWORD_MQTT";

const char* CLIENT_ID = "ESP32_Equipo06";

const char* TOPIC_PUB =
    "equipo06/sensor/datos";

const char* TOPIC_SUB =
    "equipo06/actuadores/led";

// ================= OBJETOS =================

WiFiClient espClient;
PubSubClient client(espClient);

// ================= DHT11 =================

#define DHT_PIN 4
#define DHT_TYPE DHT11

DHT dht(DHT_PIN, DHT_TYPE);

// ================= PINES =================

#define LM35_PIN 34
#define POT_PIN 35

// ================= TIEMPO =================

unsigned long ultimoEnvio = 0;
const long intervaloEnvio = 1000;

// ================= WIFI =================

void setupWiFi() {

  delay(10);

  Serial.println();
  Serial.print("Conectando a Wi-Fi: ");
  Serial.println(WIFI_SSID);

  WiFi.mode(WIFI_STA);
  WiFi.begin(WIFI_SSID, WIFI_PASS);

  while (WiFi.status() != WL_CONNECTED) {

    delay(500);
    Serial.print(".");
  }

  Serial.println("\nWiFi conectado con éxito");

  Serial.print("Dirección IP local: ");
  Serial.println(WiFi.localIP());
}

// ================= MQTT CALLBACK =================

void callback(
    char* topic,
    byte* payload,
    unsigned int length) {

  String mensaje = "";

  for (unsigned int i = 0; i < length; i++) {
    mensaje += (char)payload[i];
  }

  Serial.print("Mensaje recibido: ");
  Serial.println(mensaje);

  if (String(topic) == TOPIC_SUB) {

    if (mensaje == "ON") {

      digitalWrite(2, HIGH);
      Serial.println("LED encendido");

    } else if (mensaje == "OFF") {

      digitalWrite(2, LOW);
      Serial.println("LED apagado");
    }
  }
}

// ================= MQTT =================

void reconnect() {

  while (!client.connected()) {

    Serial.print(
        "Intentando conectar con broker MQTT...");

    if (client.connect(
        CLIENT_ID,
        MQTT_USER,
        MQTT_PASSWORD)) {

      Serial.println("Conectado");

      client.subscribe(TOPIC_SUB);

    } else {

      Serial.print("Error rc=");
      Serial.println(client.state());

      delay(5000);
    }
  }
}

// ================= SETUP =================

void setup() {

  Serial.begin(115200);

  dht.begin();

  pinMode(2, OUTPUT);

  pinMode(LM35_PIN, INPUT);
  pinMode(POT_PIN, INPUT);

  setupWiFi();

  client.setServer(
      MQTT_SERVER,
      MQTT_PORT);

  client.setCallback(callback);
}

// ================= LOOP =================

void loop() {

  if (!client.connected()) {
    reconnect();
  }

  client.loop();

  unsigned long ahora = millis();

  if (ahora - ultimoEnvio >= intervaloEnvio) {

    ultimoEnvio = ahora;

    // ---------- DHT11 ----------

    float tempDHT =
        dht.readTemperature();

    float humDHT =
        dht.readHumidity();

    if (isnan(tempDHT) ||
        isnan(humDHT)) {

      Serial.println(
          "Error leyendo el DHT11");
    }

    // ---------- LM35 ----------

    int lecturaLM35 =
        analogRead(LM35_PIN);

    float voltajeLM35 =
        lecturaLM35 *
        (3.3 / 4095.0);

    float tempLM35 =
        voltajeLM35 * 100.0;

    // ---------- POTENCIÓMETRO ----------

    int valorPot =
        analogRead(POT_PIN);

    // ---------- JSON ----------

    StaticJsonDocument<300> doc;

    doc["dispositivo"] =
        CLIENT_ID;

    doc["temperatura"] =
        tempDHT;

    doc["humedad"] =
        humDHT;

    doc["temperatura_lm35"] =
        tempLM35;

    doc["potenciometro"] =
        valorPot;

    char jsonBuffer[350];

    serializeJson(
        doc,
        jsonBuffer);

    // ---------- MQTT ----------

    Serial.print("Publicando: ");
    Serial.println(jsonBuffer);

    client.publish(
        TOPIC_PUB,
        jsonBuffer);
  }
}
```

---

# 9. Comparación de ambas etapas

| Característica | Etapa inicial | Etapa final |
|---|---|---|
| Temperatura | Simulada | DHT11 + LM35 |
| Humedad | Simulada | DHT11 |
| Potenciómetro | ❌ | ✅ |
| LM35 | ❌ | ✅ |
| MQTT | ✅ | ✅ |
| Node-RED | ✅ | ✅ |
| Control LED | ✅ | ✅ |
| Historiales | Básico | ✅ |
| Conversión ADC → V | ❌ | ✅ |
| Estado ambiental | ❌ | ✅ |
| Contador MQTT | ❌ | ✅ |
| Última actualización | ❌ | ✅ |
| Dashboard avanzado | ❌ | ✅ |
| Datos físicos | ❌ | ✅ |

La primera etapa permitió **validar la infraestructura de comunicación**, mientras que la segunda convirtió el prototipo en un sistema de adquisición y monitoreo físico.

Esta metodología redujo la cantidad de variables que debían verificarse simultáneamente durante las primeras pruebas.

---

# 10. Resultados y análisis

## 10.1 Comunicación MQTT

Se consiguió establecer comunicación entre:

```text
ESP32 ↔ Broker MQTT ↔ Node-RED
```

El ESP32 publica las mediciones y también recibe instrucciones destinadas al actuador.

Esto demuestra que la arquitectura implementada permite comunicación bidireccional.

---

## 10.2 Procesamiento de múltiples variables

La versión final transmite cuatro variables principales dentro de un único JSON:

```text
temperatura
humedad
temperatura_lm35
potenciometro
```

Además se incluye:

```text
dispositivo
```

Esto evita utilizar una publicación MQTT independiente para cada sensor y permite mantener agrupadas las mediciones generadas por el mismo dispositivo.

---

## 10.3 Dos mediciones de temperatura

Una característica interesante de la implementación es la existencia de dos mediciones de temperatura:

```text
DHT11 → temperatura ambiental digital
LM35  → temperatura obtenida mediante señal analógica
```

Esto permite observar las diferencias entre dos tecnologías de adquisición.

No necesariamente ambos sensores deben mostrar exactamente el mismo valor debido a diferencias de precisión, resolución, ubicación, respuesta temporal, conversión analógica y condiciones del montaje.

---

## 10.4 Conversión del potenciómetro

El potenciómetro demuestra el funcionamiento de una entrada analógica del ESP32.

En lugar de mostrar únicamente el valor ADC, el dashboard transforma la lectura a voltios:

\[
V =
ADC\left(\frac{3.3}{4095}\right)
\]

Esto facilita la interpretación de la señal.

---

## 10.5 Visualización histórica

Las gráficas permiten analizar la evolución de las variables y no solamente su valor instantáneo.

Esto resulta especialmente útil para:

- detectar cambios;
- identificar tendencias;
- observar variaciones bruscas;
- verificar la respuesta del potenciómetro;
- analizar la estabilidad de los sensores.

---

## 10.6 Estado ambiental

Se incorporó un indicador de estado ambiental para transformar las mediciones en información más fácil de interpretar.

Por ejemplo, el dashboard puede presentar:

```text
🟢 ESTABLE
```

cuando los valores se encuentran dentro de los criterios definidos en la lógica de Node-RED.

Esta función representa un paso adicional respecto a simplemente mostrar datos, ya que Node-RED también puede ejecutar **lógica sobre la información recibida**.

---

## 10.7 Contador de paquetes MQTT

El contador permite visualizar la cantidad de mensajes recibidos.

Su incorporación resulta útil para comprobar visualmente que el sistema continúa transmitiendo información.

Por ejemplo:

```text
📡 Paquetes MQTT: 145
```

Si el valor continúa aumentando, significa que siguen llegando nuevas publicaciones al flujo.

---

## 10.8 Última actualización

También se añadió la hora correspondiente al último mensaje procesado.

Ejemplo:

```text
⏱ Último dato: 19:28:39
```

Esto permite detectar fácilmente si el sistema ha dejado de recibir información.

---

# 11. Prueba del actuador

El sistema también fue probado físicamente mediante el LED.

El comando enviado desde el dashboard sigue el recorrido:

```text
Usuario
   ↓
Switch del Dashboard
   ↓
Node-RED
   ↓
MQTT
   ↓
equipo06/actuadores/led
   ↓
ESP32
   ↓
LED
```

Por lo tanto, el LED constituye una demostración física de que el sistema no solo recibe información, sino que también puede actuar sobre un dispositivo remoto.

---

# 12. Aspectos IoT demostrados

El proyecto permite identificar diferentes elementos fundamentales de una arquitectura IoT:

### 🔌 Dispositivo físico

ESP32.

### 🌡️ Sensores

DHT11, LM35 y potenciómetro.

### 💡 Actuador

LED.

### 📶 Comunicación

Wi-Fi.

### 📡 Protocolo

MQTT.

### ☁️ Intermediario

Broker MQTT.

### 🧠 Procesamiento

Node-RED.

### 📊 Interfaz

Dashboard 2.0.

Esto puede resumirse mediante:

```text
Percepción
   ↓
Comunicación
   ↓
Procesamiento
   ↓
Visualización
   ↓
Actuación
```

---

# 13. Diferencia entre sensor y actuador

Dentro del proyecto se pueden diferenciar claramente ambos conceptos.

**Sensor:** obtiene información del entorno o de una variable física.

Ejemplos:

```text
DHT11
LM35
Potenciómetro
```

**Actuador:** recibe una instrucción y genera una acción física.

Ejemplo:

```text
LED
```

Por ello, el proyecto integra tanto **adquisición de información** como **actuación remota**.

---

# 14. Ventajas del uso de MQTT

MQTT fue apropiado para este proyecto debido a su modelo de publicación y suscripción.

El ESP32 no necesita comunicarse directamente con el dashboard.

En cambio:

```text
ESP32 → publica → broker MQTT
Node-RED → se suscribe → broker MQTT
```

Para el control:

```text
Node-RED → publica → broker MQTT
ESP32 → se suscribe → broker MQTT
```

Esto desacopla los componentes del sistema y facilita agregar nuevos clientes o funciones posteriormente.

---

# 15. Posibles fallas observables

Durante una implementación IoT pueden aparecer diferentes situaciones.

| Problema | Posible causa |
|---|---|
| Dashboard sin datos | ESP32 desconectado |
| MQTT no recibe mensajes | Problema de broker o tópico |
| DHT11 devuelve error | Lectura inválida o conexión |
| LM35 muestra valores extraños | Conversión ADC o conexión |
| Potenciómetro no varía | Pin o cableado incorrecto |
| LED no responde | Tópico o comando incorrecto |
| Gráfica se detiene | Pérdida de comunicación |

La separación del desarrollo en dos etapas facilita identificar en qué parte se encuentra el problema.

---

# 16. Mejoras implementadas respecto al prototipo inicial

El sistema evolucionó desde:

```text
ESP32
  ↓
datos simulados
  ↓
MQTT
  ↓
dashboard básico
```

hasta:

```text
        DHT11
          │
        LM35
          │
   Potenciómetro
          │
          ▼
        ESP32
          │
          ▼
         MQTT
          │
          ▼
       Node-RED
          │
 ┌────────┼────────┐
 ▼        ▼        ▼
Gauge  Historial Estado
          │
          ▼
      Dashboard
          │
          ▼
      Control LED
```

Por lo tanto, la segunda implementación no consistió únicamente en añadir sensores. También se amplió la capa de **procesamiento, visualización y diagnóstico**.

---

# 17. Conclusiones

1. Se implementó correctamente una arquitectura IoT utilizando ESP32, MQTT y Node-RED.

2. La utilización inicial de datos simulados permitió comprobar el funcionamiento de la comunicación antes de integrar los sensores físicos.

3. Posteriormente se integraron DHT11, LM35 y potenciómetro, permitiendo adquirir diferentes variables desde el entorno y las entradas del ESP32.

4. El protocolo MQTT permitió implementar comunicación bidireccional, debido a que el ESP32 publica información de los sensores y recibe comandos para controlar el LED.

5. Node-RED permitió procesar un mismo mensaje JSON y distribuir sus diferentes variables hacia indicadores, gráficas y funciones adicionales.

6. La conversión de la lectura del potenciómetro desde ADC hacia voltios permitió presentar una magnitud física más interpretable para el usuario.

7. La presencia del DHT11 y LM35 permitió trabajar con dos mecanismos diferentes de adquisición de temperatura: uno digital y otro basado en una señal analógica.

8. Las gráficas históricas, el contador de paquetes, la última actualización y el estado ambiental permiten realizar un monitoreo más completo que una interfaz limitada únicamente a valores instantáneos.

9. El control físico del LED demostró que la arquitectura desarrollada puede utilizarse no solamente para monitoreo, sino también para control remoto de actuadores.

---

# 18. Posibles mejoras futuras

El sistema puede ampliarse posteriormente mediante:

- 🚨 alertas automáticas cuando la temperatura supere un límite;
- 📱 notificaciones;
- 💾 almacenamiento de datos históricos;
- 📊 cálculo de máximos, mínimos y promedios;
- 🔔 alarmas visuales;
- 📡 indicador de conexión MQTT;
- 🌐 acceso remoto;
- 🤖 automatización de actuadores según sensores;
- 📉 comparación automática entre DHT11 y LM35;
- 🔋 monitoreo de consumo energético;
- ☁️ almacenamiento en una base de datos.

Una evolución particularmente interesante sería implementar reglas como:

```text
SI temperatura > límite
        ↓
activar alerta
        ↓
registrar evento
        ↓
accionar actuador
```

Esto transformaría el sistema desde un sistema de monitoreo hacia uno de **monitoreo y control automático**.

---

# 19. Resumen del desarrollo

```text
ETAPA 1
Datos simulados
      ↓
ESP32
      ↓
MQTT
      ↓
Node-RED
      ↓
Dashboard básico
      ↓
Control LED

          ↓ EVOLUCIÓN ↓

ETAPA 2
DHT11 + LM35 + Potenciómetro
      ↓
ESP32
      ↓
JSON
      ↓
MQTT
      ↓
Node-RED
      ↓
Procesamiento
      ↓
Dashboard avanzado
      ↓
Gauges + históricos + estado
      ↓
Control remoto del LED
```

---

# 20. Enlaces del proyecto

### 🔧 Node-RED

https://equipo6.rcr-labs.com/#flow/f6f2187d.f17ca8

### 📊 Dashboard

https://equipo6.rcr-labs.com/dashboard/page1

---

<p align="center">
  <b>⚡ EQUIPO 06 — IoT MONITORING & CONTROL SYSTEM ⚡</b>
</p>

<p align="center">
  ESP32 • MQTT • Node-RED
</p>
