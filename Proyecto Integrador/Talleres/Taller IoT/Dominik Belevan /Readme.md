<div align="center">

# 🌐 TALLER DE INTERNET DE LAS COSAS (IoT)

### ESP32 • Sensores • Wi-Fi • IoT Cloud • Control Web

**Proyectos de Ingeniería**

---

</div>

## 📖 Descripción

En el presente taller se desarrollaron diferentes actividades prácticas utilizando el **ESP32 Dev Kit**, con el propósito de comprender el funcionamiento de un sistema de Internet de las Cosas (IoT).

Las actividades realizadas abarcaron desde la adquisición y procesamiento de una señal analógica hasta la conexión del ESP32 a una red Wi-Fi, el envío de información hacia una plataforma IoT y el control de un dispositivo mediante una interfaz web.

---

## 🎯 Objetivos

- Comprender de manera práctica el funcionamiento básico del Internet de las Cosas.
- Configurar y programar el ESP32.
- Adquirir y procesar señales provenientes de sensores y entradas analógicas.
- Establecer una conexión Wi-Fi con el ESP32.
- Enviar información hacia una plataforma IoT.
- Visualizar información obtenida por el ESP32.
- Implementar el control de un dispositivo mediante una interfaz web.

---

## 🧰 Materiales y recursos utilizados

| Material / recurso | Utilización |
|:---|:---|
| ESP32 Dev Kit | Microcontrolador principal |
| Protoboard | Montaje de los circuitos |
| Potenciómetro | Generación de una señal analógica variable |
| LED | Actuador utilizado para el control web |
| Resistencia | Limitación de corriente |
| Cables jumper | Conexiones entre componentes |
| Cable USB | Programación y alimentación |
| Smartphone | Punto de acceso Wi-Fi |
| Arduino IDE | Programación del ESP32 |
| Arduino IoT Cloud | Monitoreo de información |

---

# 1️⃣ ACTIVIDAD 1 — Lectura de un potenciómetro con ESP32

## 🎯 Objetivo

Realizar la lectura de un potenciómetro mediante el ESP32, mejorar la adquisición utilizando un promedio de varias mediciones y convertir el valor obtenido por el ADC a su voltaje equivalente.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- Potenciómetro.
- Protoboard.
- Cables jumper.
- Cable USB.
- Computadora.
- Arduino IDE.

---

## 🔌 Explicación de las conexiones

El potenciómetro cuenta con tres terminales. Los terminales laterales permiten establecer su alimentación, mientras que el terminal central proporciona una señal de voltaje variable dependiendo de la posición del potenciómetro.

La señal variable del potenciómetro fue conectada al **GPIO 34 del ESP32**, utilizado como entrada analógica.

De esta manera, al modificar la posición del potenciómetro cambia el voltaje entregado al ESP32 y, por lo tanto, también cambia el valor registrado por su convertidor analógico-digital (ADC).

### 📷 Montaje realizado

<p align="center">
  <img src="https://github.com/user-attachments/assets/24c2a6c7-9acc-4838-9fc2-4c4aff9f19da" width="350">
</p>

---

## 💻 ¿Cómo se trabajó el código?

Primero se definió el pin encargado de recibir la señal analógica:

```cpp
int potPin = 34;
```

También se utilizaron variables para almacenar la suma de las mediciones y llevar un conteo de las lecturas realizadas.

La comunicación serial se inició a:

```cpp
Serial.begin(115200);
```

Esto permitió visualizar los resultados directamente desde el **Monitor Serial**.

### 📥 Lectura del ADC

El ESP32 obtiene el valor del potenciómetro mediante:

```cpp
int valorDigital = analogRead(potPin);
```

En lugar de trabajar únicamente con una medición, el programa realiza **15 lecturas consecutivas**.

Cada lectura obtenida se agrega a una suma acumulada.

Después de completar las 15 mediciones, se calcula el promedio:

```cpp
float promedioDigital = suma / 15;
```

### ⚡ Conversión a voltaje

Posteriormente, el promedio digital se convierte a voltaje utilizando:

```cpp
float voltaje = (promedioDigital * 3.3) / 4095;
```

En esta operación:

- `promedioDigital` corresponde al promedio de las mediciones.
- `3.3` corresponde al voltaje considerado como referencia.
- `4095` corresponde al valor digital máximo utilizado en la conversión.

Finalmente, el promedio digital y el voltaje calculado se muestran en el Monitor Serial.

Después de mostrar los resultados, las variables utilizadas para acumular las mediciones se reinician para comenzar un nuevo conjunto de 15 lecturas.

---

## 📊 Resultado obtenido

El programa permitió realizar correctamente la lectura del potenciómetro y convertir el valor obtenido a voltaje.

Durante las pruebas se observaron valores digitales promedio cercanos a:

```text
1930 – 1957
```

Estos correspondieron aproximadamente a:

```text
1.56 – 1.58 V
```

### 📷 Resultados en el Monitor Serial

<p align="center">
  <img src="https://github.com/user-attachments/assets/14c6890b-0423-4d9d-9455-0617959c3217" width="650">
</p>

### ✅ ¿Qué se comprobó?

Se comprobó que el ESP32 puede adquirir una señal analógica mediante su ADC, procesar varias mediciones y convertir el resultado digital a un valor de voltaje.

---

# 2️⃣ ACTIVIDAD 2 — Conexión del ESP32 a una red Wi-Fi

## 🎯 Objetivo

Crear una red Wi-Fi utilizando un smartphone como **Hotspot**, conectar el ESP32 a dicha red y comprobar la conexión mediante la dirección IP asignada al dispositivo.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- Smartphone con función Hotspot.
- Cable USB.
- Computadora.
- Arduino IDE.

> En esta actividad no fue necesario utilizar sensores externos.

---

## 📡 Configuración de la conexión

Primero se configuró un smartphone como punto de acceso Wi-Fi.

Posteriormente, el ESP32 fue programado para conectarse a dicha red utilizando su módulo Wi-Fi integrado.

La conexión siguió el siguiente esquema:

```text
Smartphone
    │
    │ Hotspot Wi-Fi
    ▼
  ESP32
    │
    ▼
Dirección IP
```

---

## 💻 ¿Cómo se trabajó el código?

Para utilizar la conectividad inalámbrica del ESP32 se incorporó la biblioteca:

```cpp
#include <WiFi.h>
```

Luego se configuraron las credenciales correspondientes a la red:

```cpp
const char* ssid = "NOMBRE_DE_LA_RED";
const char* password = "********";
```

> 🔐 **Nota:** las credenciales reales se mantienen ocultas para evitar publicar contraseñas en GitHub.

El ESP32 se configuró para conectarse a la red y posteriormente se inició la conexión utilizando:

```cpp
WiFi.begin(ssid, password);
```

El programa comprueba el estado de la conexión mediante:

```cpp
WiFi.status()
```

Mientras el ESP32 no se encuentre conectado, el programa continúa esperando.

Una vez establecida la conexión, se utiliza:

```cpp
WiFi.localIP();
```

para obtener la dirección IP asignada al dispositivo.

---

## 📊 Resultado obtenido

El ESP32 consiguió conectarse correctamente al hotspot creado mediante el smartphone.

El Monitor Serial mostró un mensaje indicando que la conexión fue exitosa.

Además, se obtuvo la dirección IP:

```text
172.20.10.9
```

### 📷 Evidencia de la conexión

<p align="center">
  <img src="https://github.com/user-attachments/assets/fc11bd45-8023-40c7-a4f5-4882e043a501" width="650">
</p>

### ✅ ¿Qué se comprobó?

La obtención de una dirección IP permitió confirmar que el ESP32 se encontraba correctamente conectado a la red Wi-Fi.

Esta conexión sería posteriormente necesaria para realizar actividades relacionadas con el envío y recepción de información mediante Internet.

---

# 3️⃣ ACTIVIDAD 3 — Envío y monitoreo de datos en la nube

## 🎯 Objetivo

Adquirir la señal generada por un potenciómetro conectado al ESP32 y enviar la información mediante Wi-Fi para visualizarla utilizando una plataforma IoT.

---

## 🧰 ¿Qué se necesitó?

### 🔧 Hardware

- ESP32 Dev Kit.
- Potenciómetro.
- Protoboard.
- Cables jumper.
- Cable USB.

### 💻 Software y servicios

- Arduino IDE.
- Conexión Wi-Fi.
- Arduino IoT Cloud.
- Navegador web.

---

## 🔌 Explicación de las conexiones

Para esta actividad se utilizó nuevamente el potenciómetro como dispositivo de entrada.

El potenciómetro genera una señal analógica variable que es adquirida por el ESP32.

El ESP32 procesa esta información y posteriormente utiliza su conexión Wi-Fi para transmitir el dato hacia la plataforma IoT.

### 📷 ESP32 utilizado

<p align="center">
  <img src="https://github.com/user-attachments/assets/181c4b81-4290-487f-bf2a-006bf6557a0f" width="350">
</p>

---

## ☁️ ¿Cómo se trabajó el código?

Para establecer la comunicación con Arduino IoT Cloud se utilizaron las bibliotecas:

```cpp
#include <ArduinoIoTCloud.h>
#include <Arduino_ConnectionHandler.h>
```

También fue necesario configurar la conexión Wi-Fi y los datos correspondientes al dispositivo registrado en Arduino IoT Cloud.

Por seguridad, estos datos deben mantenerse ocultos en un repositorio público:

```cpp
const char SSID[] = "********";
const char PASS[] = "********";

const char DEVICE_LOGIN_NAME[] = "********";
const char DEVICE_KEY[] = "********";
```

> ⚠️ **Importante:** las contraseñas, tokens y claves de acceso no deben publicarse directamente en GitHub.

---

## 📡 Variable enviada

Se utilizó una variable para almacenar el voltaje:

```cpp
float voltaje;
```

Esta variable contiene el valor procesado que posteriormente es enviado hacia la plataforma IoT.

El proceso realizado puede representarse de la siguiente manera:

```text
Potenciómetro
     │
     ▼
Lectura ADC
     │
     ▼
Promedio de mediciones
     │
     ▼
Conversión a voltaje
     │
     ▼
   ESP32
     │
     ▼
   Wi-Fi
     │
     ▼
Arduino IoT Cloud
     │
     ▼
 Dashboard
```

---

## 🖥️ Comprobación mediante el Monitor Serial

Antes de visualizar los datos en la nube, el Monitor Serial permitió comprobar que el ESP32 estaba realizando correctamente las mediciones y procesando los valores.

### 📷 Lectura y envío de datos

<p align="center">
  <img src="https://github.com/user-attachments/assets/89ffab0a-3316-4258-986a-717a43530288" width="650">
</p>

---

## 📊 Visualización mediante Dashboard

Dentro de Arduino IoT Cloud se configuró un dashboard denominado:

### `Monitoreo Potenciometro`

Este dashboard permitió visualizar el valor enviado por el ESP32.

Durante una de las pruebas se registró un valor de:

```text
0.674
```

### 📷 Dashboard de monitoreo

<p align="center">
  <img src="https://github.com/user-attachments/assets/7c796511-e5a9-4108-8312-393f940dfc80" width="650">
</p>

---

## ✅ Resultado obtenido

Se consiguió establecer comunicación entre el ESP32 y la plataforma IoT.

El sistema permitió:

1. Obtener la señal del potenciómetro.
2. Procesar la lectura mediante el ESP32.
3. Convertir la lectura a voltaje.
4. Conectar el ESP32 a Internet mediante Wi-Fi.
5. Enviar el dato hacia la plataforma IoT.
6. Visualizar el resultado mediante un dashboard.

De esta manera se integraron diferentes etapas fundamentales de un sistema IoT:

```text
Sensor → ESP32 → Wi-Fi → Nube → Usuario
```

---

# ☁️ ACTIVIDAD 4 — MONITOREO DE TEMPERATURA CON ARDUINO IoT CLOUD

## 🎯 Objetivo
Conectar el ESP32 a Arduino IoT Cloud para obtener una medición de
temperatura y transmitirla mediante Internet.

---

## 🧰 Materiales

- ESP32
- Sensor de temperatura utilizado en la práctica
- Jumpers
- Cable USB
- Computadora
- Arduino IDE / Arduino Cloud
- Conexión Wi-Fi

---

## ☁️ Funcionamiento

En este ejercicio se implementó un sistema IoT en el cual el ESP32
realiza la lectura de temperatura y posteriormente se conecta mediante
Wi-Fi a Arduino IoT Cloud.

El funcionamiento general fue:

Sensor de temperatura
        ↓
      ESP32
        ↓
      Wi-Fi
        ↓
 Arduino IoT Cloud
        ↓
Visualización de datos

---

## 1️⃣ Configuración de Arduino IoT Cloud

Para establecer la comunicación con Arduino IoT Cloud se utilizaron
las librerías:

```cpp
#include <ArduinoIoTCloud.h>
#include <Arduino_ConnectionHandler.h>

# 5️⃣ ACTIVIDAD 5 — Control de un LED mediante una interfaz web

## 🎯 Objetivo

Conectar un LED a un pin digital del ESP32 y controlar su encendido y apagado mediante una interfaz web accesible desde un dispositivo conectado a la misma red.

---

## 🧰 ¿Qué se necesitó?

- ESP32 Dev Kit.
- LED.
- Resistencia limitadora de corriente.
- Protoboard.
- Cables jumper.
- Cable USB.
- Smartphone utilizado como Hotspot.
- Computadora.
- Arduino IDE.
- Navegador web.

---

## 🔌 Explicación de las conexiones

El ESP32 se instaló sobre la protoboard junto con el circuito correspondiente al LED.

En el programa se definió:

```cpp
const int ledPin = 2;
```

Por lo tanto, se utilizó el **GPIO 2** como salida digital para controlar el estado del LED.

También se utilizó una resistencia en el circuito para limitar la corriente que circula por el LED.

El ESP32 fue alimentado y programado mediante USB, mientras que su conexión Wi-Fi permitió recibir las instrucciones enviadas desde el navegador.

### 📷 Montaje del circuito

<p align="center">
  <img src="https://github.com/user-attachments/assets/df994350-ed88-403a-a9e2-2c3860b0621a" width="550">
</p>
---

## 💻 ¿Cómo se trabajó el código?

El programa se dividió principalmente en cuatro etapas:

### 1. 📡 Conexión Wi-Fi

Primero se incorporó:

```cpp
#include <WiFi.h>
```

Las credenciales fueron definidas mediante:

```cpp
const char* ssid = "NOMBRE_DE_LA_RED";
const char* password = "********";
```

Posteriormente, el ESP32 inicia la conexión:

```cpp
WiFi.begin(ssid, password);
```

---

### 2. 💡 Configuración del LED

El GPIO 2 se configuró como salida:

```cpp
pinMode(ledPin, OUTPUT);
```

Al iniciar el programa, el LED permanece apagado:

```cpp
digitalWrite(ledPin, LOW);
```

---

### 3. 🌐 Creación del servidor web

Se creó un servidor web utilizando el puerto 80:

```cpp
WiFiServer server(80);
```

Después de establecer la conexión Wi-Fi, el ESP32 muestra su dirección IP mediante:

```cpp
Serial.println(WiFi.localIP());
```

Esta dirección IP se introduce posteriormente en el navegador de un dispositivo conectado a la misma red.

---

### 4. 🖥️ Creación de la interfaz

Dentro del código se generó una página HTML sencilla.

La interfaz presenta dos botones:

```text
🟢 ENCENDER LED

🔴 APAGAR LED
```

El botón para encender genera una solicitud:

```text
/ON
```

Mientras que el botón para apagar utiliza:

```text
/OFF
```

---

## ⚙️ Control del LED

Cuando el ESP32 detecta la solicitud:

```cpp
if (currentLine.endsWith("GET /ON")) {
    digitalWrite(ledPin, HIGH);
}
```

el GPIO 2 cambia a estado alto y el LED se enciende.

Para apagarlo:

```cpp
if (currentLine.endsWith("GET /OFF")) {
    digitalWrite(ledPin, LOW);
}
```

el GPIO cambia a estado bajo y el LED se apaga.

---

## 🌐 Interfaz web desarrollada

Al ingresar la dirección IP del ESP32 desde el navegador se mostró la interfaz:

### `Control de LED - ESP32`

La página presenta un botón verde para encender el LED y un botón rojo para apagarlo.

<p align="center">
  <img src="https://github.com/user-attachments/assets/5ca924a9-773f-4f89-9bb0-45ac8be181aa" width="650">
</p>

---

## 💡 Comprobación física

### 🟢 LED encendido

Al seleccionar **ENCENDER LED**, el navegador envía la solicitud correspondiente al ESP32.

El GPIO 2 cambia a estado alto y el LED se enciende.

<p align="center">
  <img src="https://github.com/user-attachments/assets/3b4175da-8448-4cc0-988c-1a6f130e3d2d" width="350">
</p>

### ⚫ LED apagado

Al seleccionar **APAGAR LED**, el GPIO regresa al estado bajo y el LED se apaga.

<p align="center">
  <img src="https://github.com/user-attachments/assets/7e5dab31-9904-4e30-b98a-350beddc4293" width="350">
</p>

---

## 🔄 Flujo de funcionamiento

```text
        Usuario
           │
           ▼
     Navegador web
           │
           ▼
    Botón ON / OFF
           │
           ▼
    Solicitud HTTP
           │
           ▼
         ESP32
           │
           ▼
        GPIO 2
           │
           ▼
          LED
```

---

## ✅ Resultado obtenido

Se logró controlar correctamente el estado físico del LED mediante una interfaz web.

El ESP32 funcionó simultáneamente como:

- Dispositivo conectado a una red Wi-Fi.
- Servidor web.
- Receptor de solicitudes HTTP.
- Controlador de una salida digital.

De esta manera, se comprobó una aplicación básica de control remoto utilizando el ESP32.

---

# 📊 Resumen de las actividades

| N.° | Actividad | Concepto trabajado | Resultado |
|:---:|:---|:---|:---|
| **01** | Potenciómetro | Adquisición de datos | Lectura ADC y conversión a voltaje |
| **02** | Conexión Wi-Fi | Comunicación | ESP32 conectado y con IP asignada |
| **03** | Plataforma IoT | Monitoreo remoto | Visualización del potenciómetro en la nube |
| **04** | Sensor + IoT | Adquisición y nube | 🚧 Pendiente |
| **05** | Control de LED | Control remoto | Encendido y apagado mediante navegador |

---

# 🔄 Integración de las actividades

A lo largo del taller se trabajaron diferentes etapas relacionadas con un sistema IoT:

```text
┌──────────────────────┐
│  Adquisición de datos│
│     Potenciómetro    │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│        ESP32         │
│ Procesamiento / ADC  │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│        Wi-Fi         │
│    Comunicación      │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    Plataforma IoT    │
│ Monitoreo de datos   │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│    Control remoto    │
│      LED / Web       │
└──────────────────────┘
```

---

# 📝 Conclusiones

1. Se logró utilizar el **ESP32** para adquirir y procesar señales analógicas, así como para controlar dispositivos mediante sus salidas digitales.

2. La lectura del potenciómetro permitió trabajar con el **ADC del ESP32**, realizando varias mediciones y convirtiendo posteriormente los valores digitales obtenidos a voltaje.

3. La conexión mediante **Wi-Fi** permitió ampliar las capacidades del ESP32, pasando de un sistema local a un dispositivo capaz de comunicarse mediante una red.

4. El uso de una **plataforma IoT** permitió enviar y visualizar de manera remota la información procesada por el ESP32.

5. Finalmente, mediante la implementación de un **servidor web**, fue posible enviar instrucciones desde un navegador hacia el ESP32 y controlar físicamente el encendido y apagado de un LED.

6. Las actividades realizadas permitieron integrar conceptos fundamentales de IoT como **adquisición de datos, procesamiento, conectividad, monitoreo y control remoto**.

---

<div align="center">

## 🌐 Internet of Things

### Sensores • ESP32 • Wi-Fi • Nube • Control

**Taller de Internet de las Cosas**

</div>
