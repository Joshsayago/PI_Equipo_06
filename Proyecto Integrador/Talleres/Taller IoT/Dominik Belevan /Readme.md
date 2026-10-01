<div align="center">

# 🌐 Taller de Internet de las Cosas (IoT)

### ESP32 · Adquisición de datos · Wi-Fi · IoT Cloud · Control Web

**Proyectos de Ingeniería**

---

</div>

## 📌 Descripción

En este taller se realizaron diferentes actividades prácticas utilizando el **ESP32 Dev Kit**, con el propósito de comprender el funcionamiento básico de un sistema de Internet de las Cosas (IoT).

Las actividades comenzaron con la adquisición de una señal analógica mediante un potenciómetro y continuaron con la conexión del ESP32 a una red Wi-Fi, el envío de información hacia una plataforma IoT y el control de un dispositivo mediante una interfaz web.

---

## 🎯 Objetivos

- Comprender de manera práctica el funcionamiento básico del Internet de las Cosas.
- Configurar y programar el ESP32.
- Adquirir y procesar datos provenientes de entradas analógicas.
- Establecer comunicación mediante Wi-Fi.
- Enviar y visualizar información utilizando plataformas IoT.
- Implementar el control remoto de dispositivos mediante una interfaz web.

---

## 🧰 Materiales y recursos generales

| Material / recurso | Utilización |
|---|---|
| ESP32 Dev Kit | Microcontrolador principal |
| Protoboard | Montaje de los circuitos |
| Potenciómetro | Generación de una señal analógica variable |
| LED | Actuador para la actividad de control |
| Resistencia | Limitación de corriente del LED |
| Cables jumper | Conexiones eléctricas |
| Cable USB | Programación y alimentación del ESP32 |
| Smartphone | Punto de acceso Wi-Fi |
| Arduino IDE | Programación del ESP32 |
| Arduino IoT Cloud | Visualización remota de datos |

---

# 🔹 Actividad 1 — Lectura de un potenciómetro con ESP32

## 🎯 Objetivo

Realizar la lectura de un potenciómetro mediante el ESP32, mejorar la adquisición utilizando un promedio de varias mediciones y convertir el valor obtenido por el ADC a su voltaje equivalente.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- Potenciómetro.
- Protoboard.
- Cables jumper.
- Cable USB.
- Arduino IDE.

---

## 🔌 Explicación de las conexiones

El potenciómetro cuenta con tres terminales. Los terminales laterales permiten establecer la alimentación, mientras que el terminal central proporciona una señal de voltaje variable dependiendo de la posición de la perilla.

La salida variable se conectó al **GPIO 34 del ESP32**, utilizado como entrada analógica.

De esta manera, al girar el potenciómetro cambia el voltaje entregado al ESP32 y, por lo tanto, también cambia el valor registrado por el convertidor analógico-digital (ADC).

### 📷 Montaje realizado

![Montaje del potenciómetro con ESP32](https://github.com/user-attachments/assets/24c2a6c7-9acc-4838-9fc2-4c4aff9f19da)

---

## 💻 ¿Cómo se trabajó el código?

Primero se definió el pin utilizado para recibir la señal:

```cpp
int potPin = 34;
```

También se utilizaron las variables `contador` y `suma` para almacenar temporalmente las mediciones.

La comunicación serial se inició a:

```cpp
Serial.begin(115200);
```

En lugar de utilizar una sola lectura, el programa realiza **15 mediciones consecutivas** utilizando:

```cpp
analogRead(potPin);
```

Cada valor se acumula en `suma`. Al alcanzar las 15 mediciones se calcula el promedio:

```cpp
float promedioDigital = suma / 15;
```

Después, el promedio obtenido se convierte a voltaje:

```cpp
float voltaje = (promedioDigital * 3.3) / 4095;
```

Finalmente, el promedio digital y el voltaje equivalente se muestran mediante el Monitor Serial.

Después de presentar el resultado, el contador y la suma se reinician para comenzar un nuevo conjunto de mediciones.

---

## 📊 Resultado

Durante la ejecución se obtuvieron valores digitales promedio cercanos a **1930–1957**, correspondientes aproximadamente a valores entre **1.56 y 1.58 V**.

### 📷 Evidencia

![Resultados del potenciómetro](https://github.com/user-attachments/assets/14c6890b-0423-4d9d-9455-0617959c3217)

Esto permitió comprobar la adquisición de una señal analógica mediante el ADC del ESP32 y su posterior conversión a voltaje.

---

# 🔹 Actividad 2 — Conexión del ESP32 a una red Wi-Fi

## 🎯 Objetivo

Crear una red Wi-Fi utilizando un smartphone como **Hotspot**, conectar el ESP32 a dicha red y comprobar la conexión mediante la dirección IP asignada.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- Smartphone con función Hotspot.
- Cable USB.
- Arduino IDE.
- Computadora.

En esta actividad no fue necesario conectar un sensor externo.

---

## 📡 Configuración de la conexión

El smartphone se configuró como un punto de acceso Wi-Fi.

Posteriormente, el ESP32 se programó para funcionar como una **estación Wi-Fi**, permitiéndole buscar y conectarse a la red generada por el teléfono.

---

## 💻 ¿Cómo se trabajó el código?

Para utilizar las funciones Wi-Fi del ESP32 se incorporó:

```cpp
#include <WiFi.h>
```

Luego se definieron las credenciales:

```cpp
const char* ssid = "NOMBRE_DE_LA_RED";
const char* password = "********";
```

> 🔐 **Nota de seguridad:** las contraseñas reales se ocultan en la documentación publicada en GitHub.

El ESP32 se configuró en modo estación:

```cpp
WiFi.mode(WIFI_STA);
```

Posteriormente se inició la conexión:

```cpp
WiFi.begin(ssid, password);
```

El programa utiliza:

```cpp
WiFi.status()
```

para verificar constantemente si se estableció correctamente la conexión.

Una vez conectado, se obtiene la dirección IP mediante:

```cpp
WiFi.localIP();
```

---

## 📊 Resultado

El ESP32 logró conectarse correctamente al hotspot.

El Monitor Serial mostró:

```text
¡CONEXIÓN EXITOSA!
Dirección IP asignada: 172.20.10.9
```

### 📷 Evidencia

![Conexión Wi-Fi del ESP32](https://github.com/user-attachments/assets/fc11bd45-8023-40c7-a4f5-4882e043a501)

La obtención de una dirección IP confirmó que el dispositivo se encontraba correctamente conectado a la red.

---

# 🔹 Actividad 3 — Envío y monitoreo de datos en la nube

## 🎯 Objetivo

Adquirir la señal generada por un potenciómetro conectado al ESP32 y visualizar su variación mediante una plataforma IoT.

---

## 🧰 ¿Qué se necesitó?

### Hardware

- ESP32 Dev Kit.
- Potenciómetro.
- Protoboard.
- Cables jumper.
- Cable USB.

### Software y servicios

- Arduino IDE.
- Conexión Wi-Fi.
- Arduino IoT Cloud.
- Navegador web.

---

## 🔌 Explicación de las conexiones

Se utilizó nuevamente el principio de conexión de la **Actividad 1**.

El potenciómetro genera una señal analógica variable que es adquirida por el ESP32. El microcontrolador procesa esta señal y posteriormente utiliza su conexión Wi-Fi para transmitir el valor hacia la plataforma IoT.

### 📷 ESP32 utilizado

![ESP32 para comunicación IoT](https://github.com/user-attachments/assets/181c4b81-4290-487f-bf2a-006bf6557a0f)

---

## ☁️ ¿Cómo se trabajó el código?

Para establecer comunicación con Arduino IoT Cloud se utilizaron:

```cpp
#include <ArduinoIoTCloud.h>
#include <Arduino_ConnectionHandler.h>
```

También fue necesario configurar las credenciales Wi-Fi y las credenciales correspondientes al dispositivo registrado en Arduino Cloud.

Por seguridad, en el repositorio estas deben mantenerse ocultas:

```cpp
const char SSID[] = "********";
const char PASS[] = "********";

const char DEVICE_LOGIN_NAME[] = "********";
const char DEVICE_KEY[] = "********";
```

> ⚠️ **Importante:** nunca se deben publicar contraseñas, tokens o `DEVICE_KEY` reales en un repositorio público.

---

### Variable enviada a la nube

Se utilizó una variable:

```cpp
float voltaje;
```

Esta almacena el valor procesado del potenciómetro.

El funcionamiento general fue:

```text
Potenciómetro
      ↓
Lectura ADC
      ↓
Promedio de mediciones
      ↓
Conversión a voltaje
      ↓
ESP32
      ↓
Wi-Fi
      ↓
Arduino IoT Cloud
      ↓
Dashboard
```

---

## 🖥️ Monitor Serial

El Monitor Serial permitió comprobar localmente el valor digital y el voltaje antes de visualizarlo en la nube.

### 📷 Evidencia

![Lecturas enviadas a la nube](https://github.com/user-attachments/assets/89ffab0a-3316-4258-986a-717a43530288)

---

## 📊 Dashboard IoT

Se configuró un dashboard denominado:

**Monitoreo Potenciometro**

Durante una de las pruebas se visualizó un valor de:

```text
0.674
```

### 📷 Evidencia del dashboard

![Dashboard del potenciómetro](https://github.com/user-attachments/assets/7c796511-e5a9-4108-8312-393f940dfc80)

---

## ✅ Resultado

Se consiguió integrar la adquisición de datos con la conectividad IoT:

**Sensor → ESP32 → Wi-Fi → Plataforma IoT → Usuario**

El valor procesado por el ESP32 pudo ser enviado y visualizado mediante un dashboard.

---

# 🔹 Actividad 4 — Envío de datos de un sensor a la nube

> 🚧 **Actividad en desarrollo.**

Esta sección se completará con el sensor utilizado, sus conexiones, código, plataforma IoT y resultados obtenidos.

---

# 🔹 Actividad 5 — Control de un LED mediante una interfaz web

## 🎯 Objetivo

Conectar un LED a un pin digital del ESP32 y controlar su encendido y apagado mediante una interfaz web.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- LED.
- Resistencia limitadora.
- Protoboard.
- Cables jumper.
- Cable USB.
- Smartphone utilizado como Hotspot.
- Arduino IDE.
- Navegador web.

---

## 🔌 Explicación de las conexiones

El ESP32 se instaló sobre la protoboard y el LED se conectó a una salida digital.

En el código se definió:

```cpp
const int ledPin = 2;
```

Por lo tanto, el **GPIO 2** fue utilizado para controlar el estado del LED.

La resistencia instalada junto al LED permite limitar la corriente que circula a través del componente.

El ESP32 fue alimentado y programado mediante USB.

### 📷 Montaje

![Montaje ESP32 y LED](https://github.com/user-attachments/assets/7e5dab31-9904-4e30-b98a-350beddc4293)

---

## 💻 ¿Cómo se trabajó el código?

### 1. Conexión Wi-Fi

Se utilizó:

```cpp
#include <WiFi.h>
```

y posteriormente:

```cpp
WiFi.begin(ssid, password);
```

para conectar el ESP32 al hotspot.

---

### 2. Configuración del LED

El GPIO se configuró como salida:

```cpp
pinMode(ledPin, OUTPUT);
```

El sistema comienza con el LED apagado:

```cpp
digitalWrite(ledPin, LOW);
```

---

### 3. Creación del servidor web

Se creó un servidor HTTP utilizando el puerto 80:

```cpp
WiFiServer server(80);
```

Cuando el ESP32 se conecta a la red, muestra su dirección IP mediante:

```cpp
Serial.println(WiFi.localIP());
```

Esta dirección se ingresa posteriormente en un navegador conectado a la misma red.

---

### 4. Interfaz web

Desde el propio código del ESP32 se generó una página HTML con dos botones:

```text
🟢 ENCENDER LED
🔴 APAGAR LED
```

Cada botón genera una solicitud diferente.

Para encender:

```text
/ON
```

Para apagar:

```text
/OFF
```

---

### 5. Control físico del LED

Cuando el ESP32 recibe:

```cpp
if (currentLine.endsWith("GET /ON")) {
    digitalWrite(ledPin, HIGH);
}
```

el GPIO 2 cambia a estado alto y el LED se enciende.

Cuando recibe:

```cpp
if (currentLine.endsWith("GET /OFF")) {
    digitalWrite(ledPin, LOW);
}
```

el GPIO cambia a estado bajo y el LED se apaga.

---

## 🌐 Interfaz desarrollada

La página creada mostró el título:

### **Control de LED - ESP32**

y dos botones para controlar el circuito.

![Interfaz de control del LED](https://github.com/user-attachments/assets/5ca924a9-773f-4f89-9bb0-45ac8be181aa)

---

## 💡 Comprobación física

### LED encendido

Al seleccionar **ENCENDER LED**, el GPIO 2 pasó a estado alto y el LED se encendió.

![LED encendido](https://github.com/user-attachments/assets/3b4175da-8448-4cc0-988c-1a6f130e3d2d)

### LED apagado

Al seleccionar **APAGAR LED**, el GPIO 2 regresó al estado bajo.

![LED apagado](https://github.com/user-attachments/assets/7e5dab31-9904-4e30-b98a-350beddc4293)

---

## 🔄 Flujo de funcionamiento

```text
Usuario
   ↓
Navegador web
   ↓
Botón ON / OFF
   ↓
Solicitud HTTP
   ↓
ESP32
   ↓
GPIO 2
   ↓
LED
```

---

## ✅ Resultado

Se consiguió controlar físicamente un LED desde un navegador web.

El ESP32 funcionó simultáneamente como:

- Dispositivo conectado a la red.
- Servidor web.
- Controlador del LED.

Esto permitió comprobar una aplicación básica de **control remoto dentro de una red utilizando tecnologías IoT**.

---

# 📌 Resumen de actividades

| Actividad | Tema principal | Resultado |
|---|---|---|
| **01** | Adquisición de datos | Lectura y conversión del potenciómetro a voltaje |
| **02** | Conectividad Wi-Fi | ESP32 conectado al hotspot con IP asignada |
| **03** | IoT Cloud | Visualización del dato del potenciómetro en la nube |
| **04** | Sensor + IoT Cloud | 🚧 Pendiente |
| **05** | Control web | Encendido y apagado de un LED desde el navegador |

---

# 🔄 Integración de conceptos

Las actividades siguieron una progresión desde la adquisición de información hasta el control de un dispositivo:

```text
┌─────────────────────┐
│ Adquisición de datos│
│    Potenciómetro    │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│        ESP32        │
│ Procesamiento / ADC │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│       Wi-Fi         │
│   Comunicación      │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│   Plataforma IoT    │
│ Monitoreo de datos  │
└──────────┬──────────┘
           ↓
┌─────────────────────┐
│   Control remoto    │
│     LED / Web       │
└─────────────────────┘
```

---

# 📝 Conclusiones

1. Se logró utilizar el **ESP32** tanto para adquirir señales analógicas como para controlar dispositivos mediante salidas digitales.

2. La lectura del potenciómetro permitió comprender el funcionamiento del **ADC**, el procesamiento de varias mediciones y la conversión de valores digitales a voltaje.

3. La conexión mediante **Wi-Fi** permitió ampliar el funcionamiento del ESP32, pasando de un sistema local a un dispositivo capaz de intercambiar información a través de una red.

4. El uso de una plataforma IoT permitió visualizar remotamente los datos adquiridos por el ESP32.

5. Finalmente, mediante el servidor web se logró realizar el proceso inverso: enviar una orden desde el usuario hacia el ESP32 para modificar físicamente el estado de un LED.

---

<div align="center">

### 🌐 Internet of Things

**Sensores + ESP32 + Conectividad + Nube + Control**

</div>
