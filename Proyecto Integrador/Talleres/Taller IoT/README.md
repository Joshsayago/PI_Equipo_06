
# 🌐 Sistema IoT de Monitoreo y Control con ESP32, MQTT y Node-RED

<p align="center">
  <b>Equipo 06 — Taller de Internet of Things (IoT)</b>
</p>

<p align="center">
  Sistema IoT para adquisición, transmisión, visualización y control de variables mediante ESP32, sensores físicos, protocolo MQTT y Node-RED Dashboard 2.0.
</p>

---

## 📌 1. Descripción del proyecto

El proyecto consiste en el desarrollo progresivo de un sistema IoT basado en un **ESP32**, comunicación mediante **MQTT** y visualización mediante **Node-RED Dashboard 2.0**.

El trabajo se desarrolló en dos etapas principales:

1. **Prototipo inicial con datos simulados**, utilizado para comprobar la comunicación ESP32 → MQTT → Node-RED.
2. **Sistema final con sensores físicos**, incorporando DHT11, LM35, potenciómetro y control remoto de un LED.

La estrategia de comenzar con valores simulados permitió verificar primero la infraestructura de comunicación antes de incorporar el hardware completo.

Posteriormente, el dashboard fue ampliado con indicadores digitales, gauges, gráficas históricas, estado ambiental, contador de mensajes MQTT y una interfaz gráfica de estilo futurista.

---

# 🎯 2. Objetivos

## 2.1 Objetivo general

Desarrollar un sistema IoT capaz de adquirir variables ambientales y analógicas mediante un ESP32, transmitirlas mediante MQTT y representarlas en tiempo real mediante un dashboard interactivo desarrollado en Node-RED.

## 2.2 Objetivos específicos

- Configurar la conexión Wi-Fi del ESP32.
- Establecer comunicación con un broker MQTT.
- Comprobar inicialmente la comunicación mediante datos simulados.
- Medir temperatura y humedad mediante un DHT11.
- Medir temperatura mediante un sensor LM35.
- Leer la señal analógica de un potenciómetro.
- Convertir la lectura ADC del potenciómetro a voltios.
- Transmitir las variables mediante un único mensaje JSON.
- Procesar independientemente las variables en Node-RED.
- Visualizar valores actuales mediante indicadores digitales y gauges.
- Representar la evolución temporal mediante gráficas.
- Implementar comunicación bidireccional para controlar un LED desde el dashboard.
- Incorporar indicadores adicionales de diagnóstico del sistema.
- Diseñar una interfaz gráfica organizada y de fácil interpretación.

---

# 🧰 3. Materiales y herramientas

## Hardware

| Componente | Función |
|---|---|
| ESP32 | Microcontrolador principal y conexión Wi-Fi |
| DHT11 | Medición de temperatura y humedad |
| LM35 | Medición analógica de temperatura |
| Potenciómetro | Generación de una entrada analógica variable |
| LED | Actuador controlado remotamente |
| Resistencias | Limitación de corriente de los LED |
| Protoboard | Montaje del circuito |
| Jumpers | Interconexión de componentes |
| Cable USB | Alimentación y programación del ESP32 |

## Software y servicios

| Herramienta | Función |
|---|---|
| Arduino IDE | Programación del ESP32 |
| Node-RED | Procesamiento de los mensajes IoT |
| Dashboard 2.0 | Visualización de variables |
| MQTT | Protocolo de comunicación |
| ArduinoJson | Construcción del mensaje JSON |
| PubSubClient | Comunicación MQTT desde el ESP32 |

---

# 🏗️ 4. Arquitectura general

El funcionamiento general implementado puede representarse como:

```text
┌─────────────┐
│    DHT11    │── Temperatura
│             │── Humedad
└──────┬──────┘
       │
┌──────▼──────┐
│    LM35     │── Temperatura analógica
└──────┬──────┘
       │
┌──────▼───────────┐
│  Potenciómetro   │── Lectura ADC
└──────┬───────────┘
       │
       ▼
┌─────────────────┐
│      ESP32      │
│ Adquisición de  │
│     datos       │
└────────┬────────┘
         │ Wi-Fi
         ▼
┌─────────────────┐
│      MQTT       │
│     Broker      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│    Node-RED     │
│ Procesamiento   │
└────────┬────────┘
         │
         ▼
┌────────────────────────┐
│   Dashboard IoT 2.0    │
│ Gauges + gráficas +    │
│ indicadores + control  │
└────────────────────────┘
```

También existe comunicación en sentido contrario para el control del actuador:

```text
Dashboard
    │
    ▼
Switch LED
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

Por lo tanto, el proyecto implementa tanto **monitoreo** como **control remoto**.

---

# 🧪 5. Etapa 1 — Desarrollo con datos simulados

Antes de utilizar los sensores físicos se desarrolló una primera versión destinada a comprobar la comunicación entre los diferentes componentes del sistema.

El ESP32 generaba valores simulados de temperatura y humedad:

```cpp
float tempSimulada = 24.0 + (random(0, 100) / 10.0);
float humSimulada = 55.0 + (random(0, 200) / 10.0);
```

Posteriormente, ambos valores eran almacenados dentro de un documento JSON y publicados mediante MQTT.

Esta etapa fue importante porque permitió verificar independientemente:

- conexión Wi-Fi;
- conexión con el broker MQTT;
- publicación de mensajes;
- recepción de información en Node-RED;
- interpretación del JSON;
- funcionamiento de los widgets;
- control remoto del LED.

De esta manera, cualquier problema podía ser identificado antes de añadir la complejidad asociada a los sensores físicos.

---

## 5.1 Primer flujo desarrollado en Node-RED

<p align="center">
  <img src="https://github.com/user-attachments/assets/45a3b7a1-77ee-47e4-ab92-b6bc3f511f96" width="750">
</p>

El nodo MQTT recibe la información publicada por el ESP32.

A partir de este mensaje se utilizaron nodos de procesamiento para separar las variables:

```text
msg.payload.temperatura
msg.payload.humedad
msg.payload.dispositivo
```

Cada variable podía entonces enviarse independientemente hacia diferentes elementos del dashboard.

---

# 📊 6. Primer Dashboard

La primera versión del dashboard fue diseñada para comprobar que los datos transmitidos podían visualizarse correctamente.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e5efb0dd-2be5-46fc-acf1-a61354e02d07" width="780">
</p>

Esta primera interfaz permitía visualizar principalmente:

- temperatura;
- humedad relativa;
- dispositivo conectado;
- control del LED.

Los indicadores tipo gauge facilitaron la interpretación de los valores sin necesidad de observar directamente los mensajes MQTT.

---

# 🚀 7. Mejora del Dashboard

Una vez comprobado el funcionamiento de la comunicación, se amplió considerablemente el dashboard.

Se incorporaron:

- valores digitales;
- gauges;
- gráficas históricas;
- estado ambiental;
- hora de la última actualización;
- contador de paquetes MQTT;
- identificación del dispositivo;
- control del LED;
- voltaje del potenciómetro;
- temperatura del LM35;
- historial del potenciómetro;
- historial del LM35;
- interfaz visual de estilo futurista.

El dashboard final utiliza un tema oscuro denominado **Neon Futuristic**, con colores de alto contraste para diferenciar rápidamente las variables.

---

## 7.1 Dashboard mejorado

<p align="center">
  <img src="https://github.com/user-attachments/assets/8a850cd9-450b-4814-8de3-babcf2592bc2" width="800">
</p>

El diseño permite observar simultáneamente los valores instantáneos y su comportamiento temporal.

---

# 🔌 8. Implementación del hardware

Después de validar el funcionamiento mediante datos simulados se realizó el montaje físico de los sensores.

<p align="center">
  <img src="https://github.com/user-attachments/assets/1dc2fbb1-b138-40a1-81fd-5e445c31e9f2" width="300">
  &nbsp;&nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/5248420a-1abf-46fa-b971-90cf0f71880c" width="300">
</p>

En esta versión se incorporaron físicamente:

- DHT11;
- LM35;
- potenciómetro;
- ESP32;
- LED;
- resistencias.

El ESP32 funciona como unidad central de adquisición y comunicación.

---

# 🌡️ 9. Sensor DHT11

El DHT11 permite obtener dos variables ambientales:

- temperatura;
- humedad relativa.

La lectura se realiza mediante:

```cpp
float tempDHT = dht.readTemperature();
float humDHT = dht.readHumidity();
```

Además, se implementó una comprobación para evitar utilizar mediciones inválidas:

```cpp
if (isnan(tempDHT) || isnan(humDHT)) {
    Serial.println("Error leyendo el DHT11");
}
```

Esto permite detectar posibles errores de comunicación con el sensor.

---

# 🌡️ 10. Sensor LM35

Como segunda fuente de temperatura se incorporó un sensor analógico **LM35**.

El ESP32 realiza primero una lectura ADC:

```cpp
int lecturaLM35 = analogRead(LM35_PIN);
```

La lectura digital se transforma posteriormente en voltaje:

```cpp
float voltajeLM35 = lecturaLM35 * (3.3 / 4095.0);
```

Finalmente se calcula la temperatura:

```cpp
float tempLM35 = voltajeLM35 * 100.0;
```

Por lo tanto:

\[
V_{LM35}=ADC\left(\frac{3.3}{4095}\right)
\]

y posteriormente:

\[
T_{LM35}=V_{LM35}\times100
\]

El valor obtenido se transmite mediante MQTT como:

```json
"temperatura_lm35": 27.3
```

---

# 🎚️ 11. Potenciómetro

El potenciómetro se utilizó como entrada analógica variable.

La lectura se obtiene mediante:

```cpp
int valorPot = analogRead(POT_PIN);
```

El ESP32 posee un ADC de 12 bits, por lo que en el modelo utilizado para el dashboard se considera un intervalo:

```text
0 ─────────────── 4095
```

Sin embargo, mostrar únicamente el número ADC resulta menos intuitivo para el usuario.

Por ello se decidió convertir la lectura a voltios.

---

## 11.1 Conversión del potenciómetro a voltios

En Node-RED se implementó:

```javascript
let adc = Number(msg.payload.potenciometro);

if (!Number.isFinite(adc)) return null;

msg.payload = Number(
    ((adc * 3.3) / 4095.0).toFixed(3)
);

msg.topic = "Potenciómetro";

return msg;
```

La ecuación utilizada es:

\[
V=\frac{ADC\times3.3}{4095}
\]

### Ejemplo

Para una lectura:

\[
ADC=1840
\]

se obtiene:

\[
V=\frac{1840\times3.3}{4095}
\]

\[
\boxed{V\approx1.48\ V}
\]

De esta manera, el dashboard presenta una magnitud física más fácil de interpretar.

---

# 📡 12. Comunicación mediante MQTT

MQTT se utilizó como protocolo principal de comunicación.

El ESP32 publica los datos en:

```text
equipo06/sensor/datos
```

y recibe comandos mediante:

```text
equipo06/actuadores/led
```

El flujo lógico es:

```text
SENSORES
   ↓
 ESP32
   ↓
  JSON
   ↓
 MQTT
   ↓
NODE-RED
   ↓
DASHBOARD
```

Para el actuador:

```text
DASHBOARD
   ↓
SWITCH
   ↓
 MQTT
   ↓
 ESP32
   ↓
  LED
```

---

# 📦 13. Estructura JSON

En la versión final, los diferentes datos se agrupan en un único mensaje.

Ejemplo:

```json
{
  "dispositivo": "ESP32_Equipo06",
  "temperatura": 27.0,
  "humedad": 65.0,
  "temperatura_lm35": 27.3,
  "potenciometro": 1840
}
```

Esta estructura permite transportar múltiples variables en una sola publicación MQTT y posteriormente separarlas en Node-RED.

---

# 🧠 14. Procesamiento en Node-RED

El mensaje MQTT recibido es distribuido hacia diferentes ramas.

```text
                 ┌── Temperatura DHT11
                 │
                 ├── Humedad DHT11
                 │
                 ├── Dispositivo
MQTT ────────────┼── Estado ambiental
                 │
                 ├── Última actualización
                 │
                 ├── Contador MQTT
                 │
                 ├── Potenciómetro → Voltios
                 │
                 └── LM35 → Temperatura
```

Esto permite que un solo mensaje genere diferentes elementos de visualización.

---

# ⚙️ 15. Flujo final de Node-RED

<p align="center">
  <img src="https://github.com/user-attachments/assets/ec732bf6-f965-496a-8f3c-1f1fd47cc021" width="700">
</p>

El flujo final es considerablemente más completo que la primera versión.

Además de separar temperatura, humedad y dispositivo, incorpora funciones específicas para:

### 🌡️ Temperatura

```text
Temperatura
   ├── Gauge
   ├── Valor digital
   └── Historial
```

### 💧 Humedad

```text
Humedad
   ├── Gauge
   ├── Valor digital
   └── Historial
```

### 🎚️ Potenciómetro

```text
ADC
 ↓
Conversión a voltios
 ↓
 ├── Valor digital
 ├── Gauge
 └── Historial
```

### 🌡️ LM35

```text
temperatura_lm35
 ↓
Procesamiento
 ↓
 ├── Valor digital
 ├── Gauge
 └── Historial
```

---

# 📈 16. Visualización histórica

Además de mostrar valores instantáneos, se implementaron gráficas temporales.

Esto permite observar tendencias y cambios que serían difíciles de detectar utilizando solamente indicadores numéricos.

Se incorporaron historiales para:

- temperatura DHT11;
- humedad DHT11;
- voltaje del potenciómetro;
- temperatura LM35.

Por ejemplo, al modificar físicamente el potenciómetro, el cambio aparece inmediatamente en su gráfica.

Esto demuestra la recepción y procesamiento de datos prácticamente en tiempo real.

---

# 🚦 17. Estado ambiental

Se agregó un indicador automático denominado **Estado Ambiental**.

La lógica utilizada fue:

```javascript
let t = Number(msg.payload.temperatura);
let h = Number(msg.payload.humedad);

msg.payload =
    (t >= 30 || h >= 80) ? "🔴 ALERTA" :
    (t >= 27 || h >= 70) ? "🟡 PRECAUCIÓN" :
                           "🟢 ESTABLE";

return msg;
```

Se establecieron tres estados:

| Estado | Condición implementada |
|---|---|
| 🟢 ESTABLE | T < 27 °C y HR < 70 % |
| 🟡 PRECAUCIÓN | T ≥ 27 °C o HR ≥ 70 % |
| 🔴 ALERTA | T ≥ 30 °C o HR ≥ 80 % |

> **Nota:** estos umbrales se utilizaron como criterios demostrativos del funcionamiento del sistema y no como límites normativos de seguridad ambiental.

Esta función demuestra que Node-RED no solamente visualiza información, sino que también puede **procesarla y generar estados automáticamente**.

---

# ⏱️ 18. Última actualización

También se agregó un indicador de la hora de recepción del último mensaje:

```javascript
msg.payload = new Date().toLocaleTimeString(
    'es-PE',
    {hour12:false}
);

return msg;
```

Esto permite identificar rápidamente si el sistema continúa recibiendo información.

---

# 📡 19. Contador de paquetes MQTT

Para visualizar la actividad del sistema se implementó un contador:

```javascript
let n = context.get('n') || 0;

context.set('n', ++n);

msg.payload = n;

return msg;
```

Cada nuevo mensaje recibido incrementa el contador.

Esto proporciona una referencia visual del flujo de información entre el ESP32 y Node-RED.

---

# 💡 20. Control remoto del LED

Una característica importante del proyecto es que la comunicación no ocurre únicamente desde los sensores hacia el dashboard.

También puede realizarse en sentido contrario.

Desde el dashboard se utiliza un switch que genera:

```text
ON
```

o:

```text
OFF
```

El comando se publica mediante MQTT.

En el ESP32:

```cpp
if (mensaje == "ON") {
    digitalWrite(2, HIGH);
}

else if (mensaje == "OFF") {
    digitalWrite(2, LOW);
}
```

De esta manera:

```text
Usuario
   ↓
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

---

# 💡 21. Prueba física del actuador

<p align="center">
  <img src="https://github.com/user-attachments/assets/a57a8f7a-773c-4b28-99c4-5b1595543fd7" width="280">
  &nbsp;&nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/a4f99271-a522-4416-a2b8-b723ad13782c" width="280">
</p>

Las pruebas permitieron comprobar físicamente el cambio de estado del actuador mediante comandos enviados desde la interfaz.

Esto evidencia la **comunicación bidireccional** del sistema.

---

# 🎨 22. Diseño futurista del Dashboard

Además del funcionamiento técnico, se mejoró la presentación visual.

Se utilizó una interfaz oscura con colores tipo neón:

```text
Cian    → variables principales
Violeta → humedad e indicadores secundarios
Rosa    → LM35
Verde   → estados normales
Amarillo→ precaución
Rojo    → alertas
```

El encabezado identifica el sistema como:

> **NEON IoT CONTROL CENTER**

La interfaz fue organizada para mostrar información de manera jerárquica y facilitar su interpretación.

---

# 🔄 23. Evolución del proyecto

Una de las principales características del trabajo fue su desarrollo progresivo.

### Etapa inicial

```text
Datos aleatorios
      ↓
    ESP32
      ↓
     MQTT
      ↓
   Node-RED
      ↓
Dashboard básico
```

### Etapa final

```text
DHT11 ───────┐
             │
LM35 ────────┼──► ESP32
             │       │
Potenciómetro┘       ▼
                    MQTT
                     │
                     ▼
                  Node-RED
                     │
       ┌─────────────┼──────────────┐
       ▼             ▼              ▼
    Gauges       Gráficas       Análisis
       │             │              │
       └─────────────┼──────────────┘
                     ▼
             Dashboard final
                     │
                     ▼
                 Control LED
```

---

# 🆚 24. Comparación de las dos versiones

| Característica | Prototipo inicial | Sistema final |
|---|---:|---:|
| Comunicación Wi-Fi | ✅ | ✅ |
| MQTT | ✅ | ✅ |
| JSON | ✅ | ✅ |
| Temperatura | Simulada | DHT11 |
| Humedad | Simulada | DHT11 |
| LM35 | ❌ | ✅ |
| Potenciómetro | ❌ | ✅ |
| Conversión ADC → V | ❌ | ✅ |
| Valores digitales | Básicos | ✅ |
| Gauges | ✅ | ✅ |
| Historial de temperatura | ❌/Básico | ✅ |
| Historial de humedad | ❌/Básico | ✅ |
| Historial LM35 | ❌ | ✅ |
| Historial potenciómetro | ❌ | ✅ |
| Estado ambiental | ❌ | ✅ |
| Última actualización | ❌ | ✅ |
| Contador MQTT | ❌ | ✅ |
| Control LED | ✅ | ✅ |
| Diseño personalizado | Básico | Neon Futuristic |
| Comunicación bidireccional | ✅ | ✅ |

---

# 🧪 25. Pruebas realizadas

Durante el desarrollo se realizaron diferentes pruebas funcionales.

### Prueba 1 — Conexión Wi-Fi

Se verificó que el ESP32 pudiera conectarse correctamente a la red inalámbrica.

**Resultado:** satisfactorio.

### Prueba 2 — Conexión MQTT

Se comprobó la conexión entre el ESP32 y el broker MQTT.

**Resultado:** satisfactorio.

### Prueba 3 — Datos simulados

Se enviaron valores aleatorios de temperatura y humedad.

**Resultado:** Node-RED recibió y representó correctamente las variables.

### Prueba 4 — DHT11

Se reemplazaron los datos simulados por lecturas físicas.

**Resultado:** temperatura y humedad pudieron enviarse al dashboard.

### Prueba 5 — LM35

Se incorporó una segunda medición de temperatura.

**Resultado:** el valor pudo visualizarse mediante indicador, gauge e historial.

### Prueba 6 — Potenciómetro

Se modificó manualmente la posición del potenciómetro.

**Resultado:** el cambio de la lectura ADC se reflejó en el voltaje mostrado y en su gráfica histórica.

### Prueba 7 — Control LED

Se modificó el switch del dashboard.

**Resultado:** el ESP32 recibió los comandos MQTT `ON` y `OFF` para cambiar el estado del LED.

---

# 📷 26. Montaje final

<p align="center">
  <img src="https://github.com/user-attachments/assets/1dc2fbb1-b138-40a1-81fd-5e445c31e9f2" width="300">
  &nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/5248420a-1abf-46fa-b971-90cf0f71880c" width="300">
</p>

El montaje final integra los sensores y actuadores utilizados durante las pruebas.

---

# 🧩 27. Diferencia entre dato, procesamiento y visualización

El proyecto puede dividirse conceptualmente en tres niveles:

### 1️⃣ Adquisición

El ESP32 obtiene los datos de los sensores.

```text
DHT11
LM35
Potenciómetro
```

### 2️⃣ Procesamiento y comunicación

```text
ESP32
  ↓
JSON
  ↓
MQTT
  ↓
Node-RED
```

Node-RED separa, convierte y analiza las variables.

### 3️⃣ Visualización y control

```text
Valores digitales
Gauges
Gráficas
Estados
Contadores
Switch LED
```

Esta separación permite modificar una parte del sistema sin tener que reconstruir completamente las demás.

---

# 📊 28. Resultados obtenidos

El sistema desarrollado consiguió integrar correctamente diferentes elementos de un sistema IoT.

Se logró:

- adquirir información de sensores digitales y analógicos;
- estructurar múltiples variables en JSON;
- transmitir datos mediante MQTT;
- procesar información en Node-RED;
- visualizar información en tiempo real;
- almacenar temporalmente valores para mostrar tendencias;
- transformar una lectura ADC a voltaje;
- generar estados a partir de condiciones;
- contabilizar mensajes recibidos;
- registrar la hora de la última actualización;
- enviar órdenes desde Node-RED hacia el ESP32;
- controlar físicamente un actuador.

La incorporación de varias formas de visualización permitió representar un mismo sistema desde diferentes perspectivas: **valor instantáneo, rango, evolución temporal y estado lógico**.

---

# 💬 29. Análisis del sistema

La utilización inicial de datos aleatorios fue útil como mecanismo de validación, ya que permitió comprobar la infraestructura de comunicación sin depender inicialmente del funcionamiento de los sensores.

Una vez validado MQTT y Node-RED, se incorporaron las mediciones físicas.

El DHT11 permitió obtener temperatura y humedad mediante un sensor digital, mientras que el LM35 y el potenciómetro permitieron trabajar con entradas analógicas.

Esto permitió integrar en un mismo proyecto diferentes métodos de adquisición.

Asimismo, la conversión del potenciómetro de unidades ADC a voltios demuestra la importancia del procesamiento previo a la visualización. Un valor ADC aislado posee menor significado físico para el usuario que su representación aproximada en voltios.

Las gráficas históricas complementan a los gauges: mientras un gauge representa principalmente el estado actual, una gráfica permite analizar cómo cambia la variable con el tiempo.

Finalmente, el control del LED demuestra que MQTT puede emplearse tanto para **telemetría** como para **control**, obteniendo un sistema bidireccional.

---

# ⚠️ 30. Limitaciones

Aunque el sistema cumple con los objetivos planteados, existen algunas limitaciones:

- las mediciones dependen de las características y precisión de cada sensor;
- la conversión ADC utiliza 3.3 V y 4095 como modelo de referencia;
- la disponibilidad del dashboard depende de la conexión Wi-Fi y MQTT;
- las gráficas representan principalmente datos recientes del sistema;
- los umbrales del estado ambiental fueron definidos con fines demostrativos;
- no se implementó almacenamiento permanente en una base de datos;
- el montaje se realizó sobre protoboard y está orientado a prototipado.

Reconocer estas limitaciones permite identificar mejoras para futuras versiones.

---

# 🚀 31. Mejoras futuras

Como continuación del proyecto podrían incorporarse:

- almacenamiento en una base de datos;
- exportación de mediciones;
- notificaciones cuando una variable supere un límite;
- indicadores de conexión de cada sensor;
- control de más actuadores;
- autenticación del dashboard;
- análisis estadístico de las mediciones;
- visualización desde dispositivos móviles;
- comparación automática DHT11 vs. LM35;
- cálculo de valores máximos, mínimos y promedio;
- registro histórico de eventos;
- incorporación de sensores ambientales adicionales.

---

# 🏁 32. Conclusiones

1. Se desarrolló un sistema IoT basado en ESP32 capaz de comunicarse mediante Wi-Fi y MQTT con Node-RED.

2. El uso inicial de valores simulados permitió validar la comunicación antes de incorporar los sensores físicos.

3. Se integraron satisfactoriamente variables provenientes del DHT11, LM35 y potenciómetro dentro de una misma estructura JSON.

4. Node-RED permitió separar, transformar y representar las variables recibidas mediante valores digitales, gauges y gráficas históricas.

5. La lectura del potenciómetro fue transformada de ADC a voltios, permitiendo presentar una magnitud más interpretable.

6. Se implementaron funciones adicionales como estado ambiental, hora de última actualización y contador de mensajes MQTT.

7. El control del LED permitió demostrar comunicación bidireccional, ya que el sistema no solamente recibe información desde el ESP32, sino que también puede enviar comandos hacia este.

8. La evolución desde un dashboard básico hasta una interfaz de monitoreo más completa permitió integrar adquisición, comunicación, procesamiento, visualización y control dentro de un mismo sistema.

---

# 🔗 33. Recursos del proyecto

### Node-RED

`https://equipo6.rcr-labs.com/#flow/f6f2187d.f17ca8`

### Dashboard

`https://equipo6.rcr-labs.com/dashboard/page1`

---

# 👥 Equipo

**Equipo 06**

Proyecto desarrollado como parte del **Taller de Internet of Things (IoT)**.

---

<p align="center">
  <b>⚡ ESP32 • MQTT • NODE-RED ⚡</b>
</p>

<p align="center">
  <i>Monitoreo, procesamiento y control en tiempo real.</i>
</p>
