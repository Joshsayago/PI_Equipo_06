# 🌐 Sistema IoT con ESP32, MQTT y Node-RED

<p align="center">
  <b>Equipo 06 — Taller de Internet of Things (IoT)</b>
</p>

<p align="center">
  Desarrollo progresivo de un sistema IoT para monitoreo de variables, visualización en tiempo real y control remoto mediante ESP32, MQTT y Node-RED.
</p>

---

## 📑 Contenido

1. Descripción del proyecto
2. Objetivos
3. Materiales y herramientas
4. Arquitectura general
5. Etapa 1: Dashboard con datos aleatorios
6. Funcionamiento del primer código
7. Primer dashboard
8. Etapa 2: Implementación con sensores reales
9. Conexiones
10. DHT11
11. LM35
12. Potenciómetro
13. Estructura JSON
14. Comunicación MQTT
15. Procesamiento en Node-RED
16. Dashboard final
17. Gráficas históricas
18. Estado ambiental
19. Control remoto del LED
20. Comparación de ambas etapas
21. Pruebas realizadas
22. Resultados
23. Limitaciones y mejoras
24. Conclusiones

---

# 🎯 1. Descripción del proyecto

El proyecto consistió en desarrollar un sistema IoT utilizando un **ESP32**, comunicación mediante **MQTT** y visualización mediante **Node-RED Dashboard 2.0**.

El desarrollo se realizó de manera progresiva en dos etapas.

### 🔹 Etapa 1 — Datos simulados

Primero se desarrolló un sistema básico donde el ESP32 generaba valores aleatorios de:

- 🌡️ temperatura;
- 💧 humedad.

El objetivo fue comprobar que la comunicación entre:

**ESP32 → Wi-Fi → MQTT → Node-RED → Dashboard**

funcionara correctamente antes de conectar todos los sensores físicos.

### 🔹 Etapa 2 — Sensores reales

Una vez comprobada la comunicación, se desarrolló una versión más completa utilizando:

- 🌡️ DHT11;
- 🌡️ LM35;
- 🎚️ potenciómetro;
- 💡 LED como actuador.

También se desarrolló un dashboard más completo con gráficas históricas, gauges, valores digitales, estados del sistema y control remoto.

---

# 🎯 2. Objetivos

## Objetivo general

Desarrollar un sistema IoT capaz de adquirir, transmitir, procesar y visualizar variables mediante un ESP32, MQTT y Node-RED.

## Objetivos específicos

- Configurar la conexión Wi-Fi del ESP32.
- Establecer comunicación mediante MQTT.
- Validar inicialmente el sistema utilizando datos simulados.
- Obtener temperatura y humedad mediante un DHT11.
- Obtener una segunda medición de temperatura mediante un LM35.
- Leer una entrada analógica mediante un potenciómetro.
- Convertir la lectura ADC del potenciómetro a voltios.
- Enviar diferentes variables dentro de un mensaje JSON.
- Procesar los datos utilizando Node-RED.
- Mostrar información mediante gauges y valores digitales.
- Incorporar gráficas históricas.
- Controlar un LED remotamente.
- Implementar indicadores adicionales para facilitar el monitoreo.

---

# 🧰 3. Materiales y herramientas

## 🔩 Hardware

| Componente | Función |
|---|---|
| ESP32 | Unidad principal de procesamiento y comunicación |
| DHT11 | Temperatura y humedad |
| LM35 | Temperatura analógica |
| Potenciómetro | Entrada analógica variable |
| LED | Actuador |
| Resistencias | Limitación de corriente |
| Protoboard | Montaje del circuito |
| Jumpers | Conexiones |
| Cable USB | Programación y alimentación |

## 💻 Software

| Herramienta | Uso |
|---|---|
| Arduino IDE | Programación del ESP32 |
| Node-RED | Procesamiento de datos |
| Dashboard 2.0 | Interfaz gráfica |
| MQTT | Comunicación IoT |
| PubSubClient | Comunicación MQTT desde ESP32 |
| ArduinoJson | Construcción de mensajes JSON |
| DHT | Lectura del DHT11 |

---

# 🏗️ 4. Arquitectura general

El sistema final utiliza la siguiente arquitectura:

```text
 DHT11 ─────────────┐
                    │
 LM35 ──────────────┼──► ESP32
                    │       │
 Potenciómetro ─────┘       │
                            ▼
                          Wi-Fi
                            │
                            ▼
                      Broker MQTT
                            │
                            ▼
                        Node-RED
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
          Gauges         Gráficas       Análisis
             │              │              │
             └──────────────┼──────────────┘
                            ▼
                         Dashboard
```

Además, existe comunicación en sentido contrario:

```text
Dashboard
    │
    ▼
Switch LED
    │
    ▼
Node-RED
    │
    ▼
MQTT
    │
    ▼
ESP32
    │
    ▼
LED
```

Esto permite implementar **monitoreo y control remoto** dentro del mismo sistema.

---

# 🧪 5. ETAPA 1 — Dashboard con temperatura y humedad aleatorias

La primera etapa tuvo como objetivo comprobar el funcionamiento de la infraestructura IoT antes de incorporar todos los sensores.

En esta versión todavía no se utilizaban las mediciones físicas del DHT11, LM35 y potenciómetro.

El ESP32 generaba valores aleatorios de temperatura y humedad.

```cpp
float tempSimulada = 24.0 + (random(0, 100) / 10.0);
float humSimulada = 55.0 + (random(0, 200) / 10.0);
```

Por ejemplo, podían generarse valores como:

```text
Temperatura = 25.3 °C
Humedad = 68 %
```

Estos datos eran enviados mediante MQTT hacia Node-RED.

---

# ⚙️ 6. ¿Cómo se trabajó el primer código?

El funcionamiento del código se dividió en varias etapas.

### 1️⃣ Conexión Wi-Fi

Primero el ESP32 se conectaba a la red Wi-Fi.

```cpp
WiFi.mode(WIFI_STA);
WiFi.begin(WIFI_SSID, WIFI_PASS);
```

El programa esperaba hasta obtener conexión:

```cpp
while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
}
```

---

### 2️⃣ Conexión con MQTT

Después se configuraba el servidor MQTT.

```cpp
client.setServer(MQTT_SERVER, MQTT_PORT);
client.setCallback(callback);
```

Si la conexión se perdía, el ESP32 intentaba reconectarse automáticamente.

---

### 3️⃣ Generación de datos

La temperatura y humedad se generaban mediante `random()`.

```cpp
float tempSimulada = 24.0 + (random(0, 100) / 10.0);
float humSimulada = 55.0 + (random(0, 200) / 10.0);
```

Estos valores permitieron probar el sistema sin depender todavía de sensores físicos.

---

### 4️⃣ Construcción del JSON

Los datos se almacenaban dentro de un documento JSON.

```cpp
StaticJsonDocument<200> doc;

doc["dispositivo"] = CLIENT_ID;
doc["temperatura"] = serialized(String(tempSimulada, 2));
doc["humedad"] = serialized(String(humSimulada, 2));
```

---

### 5️⃣ Publicación MQTT

Finalmente el mensaje era publicado mediante:

```cpp
client.publish(TOPIC_PUB, jsonBuffer);
```

El flujo era:

```text
DATOS ALEATORIOS
       │
       ▼
     ESP32
       │
       ▼
      JSON
       │
       ▼
     MQTT
       │
       ▼
   NODE-RED
       │
       ▼
   DASHBOARD
```

---

# 📊 7. Primer Dashboard — Datos aleatorios

La primera interfaz fue sencilla y se utilizó principalmente para comprobar que Node-RED recibía correctamente los datos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e3dc1218-8233-4ff0-85db-6df4178e53de" width="330">
</p>

<p align="center">
  <i>Figura 1. Primer dashboard utilizado para visualizar temperatura y humedad generadas aleatoriamente.</i>
</p>

El dashboard incluía:

- identificación del dispositivo;
- control del LED;
- gauge de temperatura;
- gauge de humedad relativa.

### 🌡️ Temperatura

Se utilizó un rango visual de:

```text
0 °C ───────────────────── 45 °C
```

### 💧 Humedad

Se utilizó:

```text
0 % ───────────────────── 100 %
```

Esta etapa permitió verificar que los datos publicados por el ESP32 llegaban correctamente al dashboard.

---

# 🔄 8. ¿Por qué utilizar primero datos aleatorios?

Utilizar datos simulados antes de los sensores reales permitió separar los posibles errores.

Si el dashboard no mostraba información, se podía revisar:

```text
¿ESP32 conectado a Wi-Fi?
          ↓
¿Conectado a MQTT?
          ↓
¿Publicando JSON?
          ↓
¿Node-RED recibe el mensaje?
          ↓
¿La variable llega al widget?
```

Una vez comprobada esta cadena, se podía incorporar el hardware con mayor seguridad.

Por ello, la primera etapa funcionó como una **validación de comunicación del sistema IoT**.

---

# 🚀 9. ETAPA 2 — Implementación con sensores reales

Una vez comprobada la comunicación se sustituyeron los valores simulados por mediciones físicas.

Se incorporaron:

```text
🌡️ DHT11
   ├── Temperatura
   └── Humedad

🌡️ LM35
   └── Temperatura

🎚️ Potenciómetro
   └── Entrada analógica

💡 LED
   └── Actuador
```

El sistema pasó entonces de una prueba de comunicación a un sistema de adquisición y monitoreo de variables reales.

---

# 🔌 10. Montaje y conexiones

<p align="center">
  <img src="https://github.com/user-attachments/assets/1dc2fbb1-b138-40a1-81fd-5e445c31e9f2" width="290">
  &nbsp;&nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/5248420a-1abf-46fa-b971-90cf0f71880c" width="290">
</p>

<p align="center">
  <i>Figura 2. Montaje del ESP32 con los sensores y componentes utilizados.</i>
</p>

Las entradas definidas en el programa fueron:

```cpp
#define DHT_PIN 4
#define LM35_PIN 34
#define POT_PIN 35
```

Por lo tanto:

| Componente | ESP32 |
|---|---|
| DHT11 | GPIO 4 |
| LM35 | GPIO 34 |
| Potenciómetro | GPIO 35 |
| LED de control | GPIO 2 |

Todos los elementos deben compartir una referencia común de **GND**.

---

# 🌡️ 11. Lectura del DHT11

El DHT11 fue utilizado para medir:

- temperatura ambiental;
- humedad relativa.

Se inicializó mediante:

```cpp
#define DHT_PIN 4
#define DHT_TYPE DHT11

DHT dht(DHT_PIN, DHT_TYPE);
```

Las lecturas se obtuvieron mediante:

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

Esto permite detectar una lectura inválida.

---

# 🌡️ 12. Lectura del LM35

El LM35 proporciona una señal analógica relacionada con la temperatura.

Primero se realiza:

```cpp
int lecturaLM35 = analogRead(LM35_PIN);
```

Luego la lectura se transforma a voltaje:

```cpp
float voltajeLM35 =
    lecturaLM35 * (3.3 / 4095.0);
```

Finalmente:

```cpp
float tempLM35 =
    voltajeLM35 * 100.0;
```

La relación utilizada es:

\[
V_{LM35}=ADC\left(\frac{3.3}{4095}\right)
\]

y:

\[
T_{LM35}=V_{LM35}\times100
\]

El resultado es enviado dentro del JSON como:

```json
"temperatura_lm35": 27.3
```

---

# 🎚️ 13. Lectura del potenciómetro

El potenciómetro fue conectado al:

```cpp
#define POT_PIN 35
```

Su lectura se obtiene mediante:

```cpp
int valorPot = analogRead(POT_PIN);
```

La lectura ADC utilizada por el sistema se encuentra aproximadamente entre:

```text
0 ───────────────────── 4095
```

Posteriormente, Node-RED transforma esta lectura a voltios.

---

## ⚡ 13.1 Conversión ADC → Voltios

La ecuación implementada fue:

\[
V=\frac{ADC\times3.3}{4095}
\]

Por ejemplo:

\[
ADC=1840
\]

Entonces:

\[
V=\frac{1840\times3.3}{4095}
\]

\[
\boxed{V\approx1.48\ V}
\]

En Node-RED se utilizó:

```javascript
let adc = Number(msg.payload.potenciometro);

if (!Number.isFinite(adc)) return null;

msg.payload = Number(
    ((adc * 3.3) / 4095.0).toFixed(3)
);

msg.topic = "Potenciómetro";

return msg;
```

Esto permite mostrar **voltios** en lugar de únicamente el valor ADC.

---

# 📦 14. Construcción del JSON final

En lugar de publicar cada sensor por separado, todas las variables fueron agrupadas en un único JSON.

```cpp
StaticJsonDocument<300> doc;

doc["dispositivo"] = CLIENT_ID;

doc["temperatura"] = tempDHT;
doc["humedad"] = humDHT;

doc["temperatura_lm35"] = tempLM35;

doc["potenciometro"] = valorPot;
```

Un mensaje enviado puede tener la siguiente estructura:

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.0,
  "humedad": 65.0,
  "temperatura_lm35": 27.3,
  "potenciometro": 1840
}
```

Esta estrategia permite transmitir toda la información necesaria mediante una sola publicación MQTT.

---

# ⏱️ 15. Frecuencia de actualización

En el código final se definió:

```cpp
const long intervaloEnvio = 1000;
```

Como el valor está expresado en milisegundos:

\[
1000\ ms=1\ s
\]

Por lo tanto, el sistema intenta realizar una nueva actualización aproximadamente **cada 1 segundo**.

Además, se utiliza `millis()` en lugar de un `delay()` principal:

```cpp
unsigned long ahora = millis();

if (ahora - ultimoEnvio >= intervaloEnvio) {
    ultimoEnvio = ahora;

    // lectura y publicación
}
```

Esto evita bloquear constantemente la ejecución y permite continuar atendiendo la comunicación MQTT.

---

# 📡 16. Comunicación MQTT

El ESP32 publica los sensores mediante:

```text
equipo06/sensor/datos
```

Para el control del LED se utiliza:

```text
equipo06/actuadores/led
```

Por lo tanto existen dos sentidos de comunicación:

### 📤 Telemetría

```text
ESP32
  │
  │ temperatura
  │ humedad
  │ LM35
  │ potenciómetro
  ▼
 MQTT
  ▼
Node-RED
```

### 📥 Control

```text
Node-RED
   │
   │ ON / OFF
   ▼
 MQTT
   ▼
 ESP32
   ▼
  LED
```

Esto convierte el proyecto en un sistema **bidireccional**.

---

# 🧠 17. Procesamiento en Node-RED

El mensaje recibido mediante MQTT se distribuye hacia diferentes ramas.

```text
                     ┌── Temperatura DHT11
                     │
                     ├── Humedad DHT11
                     │
                     ├── Dispositivo
                     │
MQTT ────────────────┼── Estado ambiental
                     │
                     ├── Última actualización
                     │
                     ├── Contador MQTT
                     │
                     ├── Potenciómetro → Voltios
                     │
                     └── Temperatura LM35
```

Esto permite reutilizar un único mensaje para generar diferentes visualizaciones.

---

# ⚙️ 18. Flujo final de Node-RED

<p align="center">
  <img src="https://github.com/user-attachments/assets/ec732bf6-f965-496a-8f3c-1f1fd47cc021" width="720">
</p>

<p align="center">
  <i>Figura 3. Flujo final desarrollado en Node-RED.</i>
</p>

El flujo incluye:

### DHT11

```text
Temperatura ──► Gauge
            ├─► Valor digital
            └─► Gráfica histórica

Humedad ─────► Gauge
           ├─► Valor digital
           └─► Gráfica histórica
```

### Potenciómetro

```text
Lectura ADC
    │
    ▼
Conversión a V
    │
    ├──► Valor digital
    ├──► Gauge
    └──► Gráfica
```

### LM35

```text
Temperatura LM35
       │
       ├──► Valor digital
       ├──► Gauge
       └──► Gráfica
```

---

# 🖥️ 19. Dashboard final — Sensores reales

Después de implementar los sensores se desarrolló una interfaz más completa.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e5efb0dd-2be5-46fc-acf1-a61354e02d07" width="780">
</p>

<p align="center">
  <i>Figura 4. Dashboard final para monitoreo del sistema.</i>
</p>

El dashboard presenta:

- 🌡️ temperatura del DHT11;
- 💧 humedad;
- 🎚️ voltaje del potenciómetro;
- 🌡️ temperatura LM35;
- 📈 gráficas históricas;
- 🚦 estado ambiental;
- ⏱️ última actualización;
- 📡 contador de paquetes MQTT;
- 💡 control del LED;
- 🛰️ identificación del ESP32.

---

## 19.1 Potenciómetro y LM35

<p align="center">
  <img src="https://github.com/user-attachments/assets/8a850cd9-450b-4814-8de3-babcf2592bc2" width="780">
</p>

<p align="center">
  <i>Figura 5. Visualización del potenciómetro y LM35 en el dashboard final.</i>
</p>

El potenciómetro dispone de:

- valor digital en voltios;
- gauge entre 0 y 3.3 V;
- gráfica histórica.

El LM35 dispone de:

- temperatura digital;
- gauge;
- gráfica histórica.

---

# 📈 20. Gráficas históricas

Los gauges permiten conocer rápidamente el valor actual de una variable.

Sin embargo, no permiten identificar fácilmente cómo ha cambiado con el tiempo.

Por ello se incorporaron gráficas para:

```text
📈 Temperatura DHT11
📈 Humedad DHT11
📈 Voltaje del potenciómetro
📈 Temperatura LM35
```

Esto permite observar tendencias y variaciones.

Por ejemplo, cuando el potenciómetro se gira físicamente:

```text
Movimiento del potenciómetro
            ↓
Cambio de resistencia
            ↓
Cambio de tensión
            ↓
ADC del ESP32
            ↓
Conversión a voltios
            ↓
MQTT
            ↓
Gráfica en Node-RED
```

---

# 🚦 21. Estado ambiental

Se agregó un procesamiento adicional para clasificar las mediciones.

```javascript
let t = Number(msg.payload.temperatura);
let h = Number(msg.payload.humedad);

msg.payload =
    (t >= 30 || h >= 80) ? "🔴 ALERTA" :
    (t >= 27 || h >= 70) ? "🟡 PRECAUCIÓN" :
                           "🟢 ESTABLE";

return msg;
```

El dashboard puede mostrar:

| Estado | Condición demostrativa |
|---|---|
| 🟢 ESTABLE | T < 27 °C y HR < 70 % |
| 🟡 PRECAUCIÓN | T ≥ 27 °C o HR ≥ 70 % |
| 🔴 ALERTA | T ≥ 30 °C o HR ≥ 80 % |

> Los valores utilizados son umbrales demostrativos implementados para probar el procesamiento lógico del dashboard; no representan límites normativos.

Esto demuestra que Node-RED no solamente muestra información, sino que también puede **tomar los datos recibidos y generar información derivada**.

---

# ⏱️ 22. Última actualización

Se añadió un indicador que muestra la hora del último mensaje recibido.

Ejemplo:

```text
⏱️ Último dato: 19:28:39
```

Esto resulta útil para comprobar visualmente que el ESP32 continúa enviando información.

---

# 📡 23. Contador de paquetes MQTT

También se incorporó un contador de mensajes.

```text
📡 Paquetes MQTT: 145
```

Cada vez que Node-RED recibe un nuevo mensaje, el contador aumenta.

Esto permite observar la actividad de comunicación del sistema durante la demostración.

---

# 💡 24. Control remoto del LED

El dashboard también permite controlar un LED conectado al ESP32.

El usuario modifica el switch y Node-RED publica:

```text
ON
```

o:

```text
OFF
```

El ESP32 recibe el comando mediante la función `callback()`.

```cpp
if (mensaje == "ON") {

    digitalWrite(2, HIGH);
    Serial.println("Comando: Encender LED");

}

else if (mensaje == "OFF") {

    digitalWrite(2, LOW);
    Serial.println("Comando: Apagar LED");

}
```

La comunicación ocurre así:

```text
👤 Usuario
    │
    ▼
🖥️ Dashboard
    │
    ▼
🔘 Switch
    │
    ▼
📡 MQTT
    │
    ▼
🧠 ESP32
    │
    ▼
💡 LED
```

---

# 🧪 25. Prueba física del LED

<p align="center">
  <img src="https://github.com/user-attachments/assets/a57a8f7a-773c-4b28-99c4-5b1595543fd7" width="280">
  &nbsp;&nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/a4f99271-a522-4416-a2b8-b723ad13782c" width="280">
</p>

<p align="center">
  <i>Figura 6. Prueba del control físico del actuador.</i>
</p>

Estas pruebas permitieron comprobar que los comandos enviados desde Node-RED podían producir una acción física en el ESP32.

---

# 🎨 26. Diseño del dashboard final

Para mejorar la presentación del proyecto se utilizó una interfaz de estilo oscuro/futurista.

El encabezado utilizado fue:

```text
ESP32 • MQTT • NODE-RED

NEON IoT CONTROL CENTER

Monitoreo ambiental y control remoto en tiempo real
```

Se utilizaron diferentes colores para diferenciar visualmente las variables.

```text
🔵 Cian      → Variables principales
🟣 Violeta  → Humedad / información secundaria
🩷 Rosa     → LM35
🟢 Verde    → Estado estable
🟡 Amarillo → Precaución
🔴 Rojo     → Alerta
```

El objetivo no fue únicamente decorar la interfaz, sino facilitar la identificación rápida de cada variable.

---

# 🆚 27. Comparación entre las dos etapas

| Característica | Etapa 1 | Etapa 2 |
|---|---|---|
| Temperatura | 🎲 Aleatoria | 🌡️ DHT11 |
| Humedad | 🎲 Aleatoria | 💧 DHT11 |
| LM35 | ❌ | ✅ |
| Potenciómetro | ❌ | ✅ |
| ADC → Voltios | ❌ | ✅ |
| MQTT | ✅ | ✅ |
| JSON | ✅ | ✅ |
| Node-RED | ✅ | ✅ |
| Gauge temperatura | ✅ | ✅ |
| Gauge humedad | ✅ | ✅ |
| Gráficas históricas | Básico/No | ✅ |
| Estado ambiental | ❌ | ✅ |
| Última actualización | ❌ | ✅ |
| Contador MQTT | ❌ | ✅ |
| Control LED | ✅ | ✅ |
| Interfaz | Básica | Futurista |
| Sensores físicos | ❌ | ✅ |
| Comunicación bidireccional | ✅ | ✅ |

---

# 🔬 28. Diferencia fundamental entre ambas versiones

La principal diferencia puede resumirse de la siguiente manera:

### Primera versión

```text
ESP32
  │
  ├── Genera temperatura aleatoria
  └── Genera humedad aleatoria
          │
          ▼
         MQTT
          │
          ▼
      Dashboard
```

### Segunda versión

```text
       MUNDO FÍSICO
            │
     ┌──────┼──────┐
     │      │      │
   DHT11   LM35   POT
     │      │      │
     └──────┼──────┘
            ▼
          ESP32
            │
            ▼
           JSON
            │
            ▼
           MQTT
            │
            ▼
        NODE-RED
            │
      ┌─────┼─────┐
      ▼     ▼     ▼
   Gauges Gráficas Análisis
            │
            ▼
         Dashboard
```

En otras palabras, la primera versión permitió comprobar la **comunicación**, mientras que la segunda permitió comprobar el sistema completo de **adquisición + comunicación + procesamiento + visualización + control**.

---

# 🧪 29. Pruebas realizadas

## Prueba 1 — Wi-Fi

Se verificó la conexión del ESP32 a la red.

**Resultado:** ✅ Correcto.

---

## Prueba 2 — Broker MQTT

Se comprobó que el ESP32 pudiera publicar mensajes.

**Resultado:** ✅ Correcto.

---

## Prueba 3 — Temperatura y humedad aleatorias

Se enviaron valores generados mediante `random()`.

**Resultado:** ✅ Node-RED recibió y mostró las variables.

---

## Prueba 4 — DHT11

Se reemplazaron los datos simulados por datos obtenidos físicamente.

**Resultado:** ✅ Se visualizaron temperatura y humedad.

---

## Prueba 5 — LM35

Se incorporó una segunda fuente de temperatura.

**Resultado:** ✅ El dashboard recibió y representó la temperatura LM35.

---

## Prueba 6 — Potenciómetro

Se giró físicamente el potenciómetro.

**Resultado:** ✅ El cambio pudo observarse en el gauge y en la gráfica.

---

## Prueba 7 — LED

Se modificó el switch del dashboard.

**Resultado:** ✅ El ESP32 recibió los comandos de control.

---

## Prueba 8 — Historial

Se modificaron las variables durante varios segundos.

**Resultado:** ✅ Las gráficas mostraron la evolución temporal.

---

# 📊 30. Resultados obtenidos

El sistema final permitió integrar:

```text
ADQUISICIÓN
     +
COMUNICACIÓN
     +
PROCESAMIENTO
     +
VISUALIZACIÓN
     +
CONTROL
```

Se consiguió:

- leer sensores digitales;
- leer sensores analógicos;
- convertir ADC a voltaje;
- transmitir datos mediante MQTT;
- estructurar información mediante JSON;
- procesar diferentes variables en Node-RED;
- mostrar valores instantáneos;
- representar tendencias mediante gráficas;
- generar estados automáticamente;
- contar mensajes MQTT;
- identificar la última actualización;
- enviar comandos desde el dashboard;
- controlar un actuador físico.

---

# 🧠 31. Análisis

La implementación por etapas facilitó considerablemente el desarrollo.

Si desde el inicio se hubieran conectado todos los sensores, un error podría provenir del hardware, Wi-Fi, MQTT, JSON o Node-RED.

En cambio, utilizando inicialmente datos aleatorios se comprobó primero:

```text
ESP32 → MQTT → Node-RED → Dashboard
```

Una vez validada esta comunicación, se incorporó:

```text
Sensores → ESP32
```

Esto permitió localizar problemas de manera más ordenada.

Otra mejora importante fue la incorporación de gráficas históricas.

Un gauge responde principalmente:

> **¿Cuál es el valor actual?**

Mientras que una gráfica permite responder:

> **¿Cómo ha cambiado el valor con el tiempo?**

Por ello, utilizar ambos tipos de visualización proporciona más información sobre el sistema.

Finalmente, el LED demuestra que MQTT no solamente puede utilizarse para enviar telemetría desde un dispositivo, sino también para controlar actuadores remotamente.

---

# ⚠️ 32. Limitaciones del prototipo

El sistema desarrollado corresponde a un prototipo académico y presenta algunas limitaciones:

- depende de una conexión Wi-Fi;
- depende de la disponibilidad del broker MQTT;
- las mediciones dependen de la precisión de los sensores;
- la conversión ADC utiliza 3.3 V y 4095 como modelo de referencia;
- el montaje sobre protoboard está orientado a pruebas;
- los umbrales ambientales son demostrativos;
- no existe almacenamiento permanente en una base de datos.

Estas limitaciones representan oportunidades para continuar mejorando el proyecto.

---

# 🚀 33. Posibles mejoras futuras

Como continuación podrían incorporarse:

- 💾 base de datos para almacenar mediciones;
- 🔔 sistema de alertas;
- 📧 notificaciones automáticas;
- 📊 cálculo de promedio, máximo y mínimo;
- 📱 interfaz optimizada para celular;
- 🌐 acceso remoto autenticado;
- 📥 exportación de datos;
- 📈 comparación automática DHT11 vs LM35;
- 🚨 alarmas cuando un sensor supere un límite;
- 🔌 más actuadores;
- 🛰️ indicador de conexión MQTT;
- 📶 indicador de intensidad Wi-Fi;
- 🕒 registro histórico de eventos.

---

# 🏁 34. Conclusiones

1. Se logró establecer comunicación entre el ESP32, un broker MQTT y Node-RED.

2. La primera etapa con temperatura y humedad aleatorias permitió validar la comunicación antes de incorporar los sensores físicos.

3. Posteriormente se integraron el DHT11, LM35 y potenciómetro, permitiendo adquirir diferentes variables desde el entorno físico.

4. El uso de JSON permitió organizar las diferentes mediciones dentro de un único mensaje MQTT.

5. Node-RED permitió separar, transformar y visualizar las variables mediante gauges, valores digitales y gráficas históricas.

6. La conversión del potenciómetro de ADC a voltios permitió presentar una magnitud más interpretable.

7. El estado ambiental, contador MQTT y última actualización agregaron información adicional para conocer el funcionamiento del sistema.

8. El control del LED permitió demostrar comunicación bidireccional entre Node-RED y el ESP32.

9. El proyecto evolucionó desde una prueba básica de comunicación hasta un sistema IoT capaz de realizar **adquisición, comunicación, procesamiento, monitoreo y control**.

---

# 🔗 35. Acceso al sistema

### 🔧 Node-RED

`https://equipo6.rcr-labs.com/#flow/f6f2187d.f17ca8`

### 🖥️ Dashboard

`https://equipo6.rcr-labs.com/dashboard/page1`

---

# 🔐 36. Seguridad

Las credenciales utilizadas para Wi-Fi y MQTT **no deben almacenarse públicamente en GitHub**.

En una versión pública del código se recomienda utilizar:

```cpp
const char* WIFI_SSID = "TU_RED_WIFI";
const char* WIFI_PASS = "TU_PASSWORD";

const char* MQTT_USER = "TU_USUARIO";
const char* MQTT_PASSWORD = "TU_PASSWORD_MQTT";
```

De esta manera se evita publicar información sensible del sistema.

---

<p align="center">
  <b>⚡ ESP32 • MQTT • NODE-RED ⚡</b>
</p>

<p align="center">
  <b>Equipo 06</b>
</p>

<p align="center">
  <i>De datos simulados a un sistema IoT de monitoreo y control.</i>
</p>
