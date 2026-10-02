# 🌐 Taller de Internet of Things (IoT) con ESP32

<p align="center">
  <b>Implementación de adquisición de datos, conectividad Wi-Fi, Arduino IoT Cloud y control remoto utilizando ESP32</b>
</p>

---

## 📑 Índice

1. [Introducción](#-introducción)
2. [Objetivos](#-objetivos)
3. [Materiales y herramientas](#-materiales-y-herramientas)
4. [Ejercicio 1 – Lectura analógica con potenciómetro](#-ejercicio-1--lectura-analógica-con-potenciómetro)
5. [Ejercicio 2 – Conexión de la ESP32 a Wi-Fi](#-ejercicio-2--conexión-de-la-esp32-a-wi-fi)
6. [Ejercicio 3 – Arduino IoT Cloud](#-ejercicio-3--arduino-iot-cloud)
7. [Ejercicio 4 – Medición de temperatura](#-ejercicio-4--medición-de-temperatura)
8. [Ejercicio 5 – Control remoto de un LED](#-ejercicio-5--control-remoto-de-un-led)
9. [Flujo general de funcionamiento](#-flujo-general-de-funcionamiento)
10. [Conclusiones](#-conclusiones)

---

# 📌 Introducción

En este taller se trabajó con la tarjeta **ESP32** para desarrollar diferentes aplicaciones relacionadas con el Internet de las Cosas (**IoT**).

Las actividades se realizaron progresivamente. Primero se trabajó con la adquisición de señales analógicas mediante un potenciómetro; posteriormente se configuró la conexión de la ESP32 a una red Wi-Fi, se realizó la transmisión de información mediante una plataforma IoT, se trabajó con mediciones de temperatura y finalmente se implementó el control remoto de un LED mediante una interfaz web.

De esta manera, se aplicaron conceptos fundamentales de un sistema IoT:

```text
Sensor / Entrada
       ↓
     ESP32
       ↓
Procesamiento
       ↓
Comunicación
       ↓
Internet / Plataforma
       ↓
Visualización o control
```

---

# 🎯 Objetivos

## Objetivo general

Implementar diferentes aplicaciones IoT utilizando la ESP32, integrando adquisición de datos, procesamiento, comunicación mediante Wi-Fi, transmisión de información y control remoto.

## Objetivos específicos

- Realizar lecturas analógicas mediante el ADC de la ESP32.
- Convertir valores digitales a valores de voltaje.
- Conectar la ESP32 a una red Wi-Fi.
- Utilizar Arduino IoT Cloud para transmitir información.
- Obtener mediciones de temperatura mediante sensores.
- Implementar el control remoto de un LED.
- Comprender la relación entre hardware, software y comunicación dentro de un sistema IoT.

---

# 🧰 Materiales y herramientas

Durante las diferentes actividades se utilizaron los siguientes elementos:

| Componente / herramienta | Función |
|---|---|
| ESP32 | Microcontrolador principal del sistema |
| Protoboard | Montaje de los circuitos |
| Potenciómetro | Generación de una señal analógica variable |
| Sensor de temperatura | Medición de temperatura |
| LED | Actuador visual |
| Resistencia | Limitación de corriente del LED |
| Cables jumper | Interconexión de componentes |
| Cable USB | Alimentación y programación de la ESP32 |
| Arduino IDE | Programación de la ESP32 |
| Wi-Fi | Comunicación con servicios externos |
| Arduino IoT Cloud | Visualización de variables mediante Internet |

---

# 🔵 Ejercicio 1 – Lectura analógica con potenciómetro

## 🎯 Objetivo

Realizar la lectura de una señal analógica utilizando el ADC de la ESP32 y convertir el valor digital obtenido a su voltaje equivalente.

---

## 🧰 Materiales utilizados

- ESP32
- Potenciómetro
- Protoboard
- Cables jumper
- Cable USB
- Computadora
- Arduino IDE

---

## 🔌 Explicación de las conexiones

El potenciómetro se utilizó como una entrada analógica variable.

La salida del potenciómetro se conectó a una entrada ADC de la ESP32. En el código utilizado se definió:

```cpp
int potPin = 34;
```

Por lo tanto, la adquisición de la señal se realizó mediante el **GPIO 34**.

El funcionamiento general puede representarse de la siguiente manera:

```text
          POTENCIÓMETRO
        ┌───────────────┐
        │               │
3.3 V ──┤               │
        │               ├──── Señal analógica ──── GPIO 34
GND  ───┤               │
        └───────────────┘
                              │
                              ▼
                            ESP32
```

Al girar el potenciómetro se modifica el voltaje de salida. Este cambio es detectado por el convertidor analógico-digital de la ESP32.

---

## 💻 ¿Cómo se trabajó el código?

El programa comienza definiendo el pin utilizado para la lectura y las variables necesarias para calcular un promedio:

```cpp
int potPin = 34;
int contador = 0;
float suma = 0;
```

La ESP32 realiza múltiples lecturas analógicas.

Posteriormente, estas lecturas son acumuladas para obtener un valor promedio.

El procesamiento realizado fue:

```text
Lectura analógica
       ↓
Valor ADC
       ↓
Acumulación de muestras
       ↓
Promedio digital
       ↓
Conversión
       ↓
Voltaje equivalente
```

Para un ADC de 12 bits, el intervalo digital utilizado es:

```text
0 ───────────────────── 4095
│                         │
0 V                      3.3 V
```

La relación utilizada conceptualmente para obtener el voltaje es:

```text
Voltaje = (Lectura ADC / 4095) × 3.3 V
```

---

## ⚙️ Procedimiento

1. Se colocó el potenciómetro en la protoboard.
2. Se conectó la salida del potenciómetro al GPIO 34.
3. Se conectaron alimentación y tierra.
4. Se conectó la ESP32 a la computadora mediante USB.
5. Se abrió Arduino IDE.
6. Se cargó el programa.
7. Se realizaron varias lecturas analógicas.
8. Se calculó el promedio digital.
9. Se convirtió el valor promedio a voltaje.
10. Los resultados fueron visualizados mediante el monitor serial.

---

## 📊 Resultados

Durante las pruebas se obtuvieron valores como los siguientes:

| Promedio digital | Voltaje equivalente |
|---:|---:|
| 1942.20 | 1.565 V |
| 1949.73 | 1.571 V |
| 1936.07 | 1.560 V |
| 1931.40 | 1.556 V |
| 1944.27 | 1.567 V |
| 1956.73 | 1.577 V |

Los valores presentan pequeñas variaciones entre mediciones. El promedio permite reducir el efecto de variaciones instantáneas y obtener una lectura más estable.

---

## 📸 Evidencias

<p align="center">
<img width="500" alt="Montaje del ejercicio 1" src="https://github.com/user-attachments/assets/f7692390-8595-47a7-a1e7-e07e893f9802" />
</p>

<p align="center">
<b>Figura 1.</b> Montaje experimental del potenciómetro conectado a la ESP32.
</p>

<p align="center">
<img width="900" alt="Resultados del ejercicio 1" src="https://github.com/user-attachments/assets/1c2c74c2-22b7-49b6-9bb0-faf53d14ec71" />
</p>

<p align="center">
<b>Figura 2.</b> Lecturas obtenidas mediante el monitor serial.
</p>

---

# 📡 Ejercicio 2 – Conexión de la ESP32 a Wi-Fi

## 🎯 Objetivo

Configurar la ESP32 para conectarse correctamente a una red Wi-Fi y comprobar la conexión mediante la dirección IP asignada al dispositivo.

---

## 🧰 Materiales y recursos

- ESP32
- Cable USB
- Computadora
- Arduino IDE
- Red Wi-Fi o punto de acceso móvil
- Nombre de la red
- Contraseña de la red

---

## 🔌 Conexión

En este ejercicio no fue necesario utilizar un sensor externo.

La arquitectura utilizada fue:

```text
┌──────────┐          USB          ┌──────────────┐
│  ESP32   │◄────────────────────►│ Computadora  │
└────┬─────┘                       └──────────────┘
     │
     │ Wi-Fi
     ▼
┌───────────────┐
│ Router /      │
│ Hotspot móvil │
└───────────────┘
```

La ESP32 posee conectividad Wi-Fi integrada, por lo que no fue necesario utilizar un módulo externo.

---

## 💻 ¿Cómo se trabajó el código?

Primero se utilizó la librería:

```cpp
#include <WiFi.h>
```

Esta librería permite acceder a las funciones Wi-Fi de la ESP32.

Posteriormente se definieron las credenciales de la red.

> 🔐 **Nota:** por seguridad, las credenciales reales no deben publicarse en un repositorio.

```cpp
const char* ssid = "TU_RED_WIFI";
const char* password = "TU_PASSWORD";
```

La ESP32 se configuró en modo estación:

```cpp
WiFi.mode(WIFI_STA);
```

Posteriormente se inició la conexión:

```cpp
WiFi.begin(ssid, password);
```

Mientras la conexión no estuviera establecida, el programa comprobaba continuamente su estado:

```cpp
while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
}
```

Cuando la conexión fue exitosa se obtuvo la dirección IP asignada:

```cpp
Serial.println(WiFi.localIP());
```

---

## ⚙️ Procedimiento

```text
Encendido de ESP32
        ↓
Inicialización Wi-Fi
        ↓
Búsqueda de la red
        ↓
Ingreso de credenciales
        ↓
Autenticación
        ↓
Conexión exitosa
        ↓
Asignación de dirección IP
```

1. Se conectó la ESP32 a la computadora.
2. Se abrió Arduino IDE.
3. Se configuraron las credenciales Wi-Fi.
4. Se compiló el programa.
5. Se cargó el programa en la ESP32.
6. La ESP32 buscó la red configurada.
7. Se realizó la autenticación.
8. Se estableció la conexión.
9. Se obtuvo la dirección IP.
10. El resultado fue observado en el monitor serial.

---

## 📊 Resultado

El monitor serial confirmó que la ESP32 logró conectarse correctamente a la red y recibió una dirección IP.

Esto permitió comprobar la capacidad de comunicación inalámbrica del dispositivo y preparó la ESP32 para las siguientes actividades IoT.

---

## 📸 Evidencia

<p align="center">
<img width="950" alt="Conexión WiFi ESP32" src="https://github.com/user-attachments/assets/e5cfa29f-886e-4ec5-9785-d19279bbc5f9" />
</p>

<p align="center">
<b>Figura 3.</b> Conexión exitosa de la ESP32 a una red Wi-Fi.
</p>

---

# ☁️ Ejercicio 3 – Arduino IoT Cloud

## 🎯 Objetivo

Integrar la ESP32 con una plataforma IoT para transmitir una variable obtenida físicamente y visualizarla mediante Internet.

---

## 🧰 Materiales y recursos

- ESP32
- Potenciómetro
- Protoboard
- Cables jumper
- Cable USB
- Arduino IDE
- Conexión Wi-Fi
- Arduino IoT Cloud

---

## 🔌 Conexiones

Se utilizó nuevamente un potenciómetro como entrada analógica.

La arquitectura general fue:

```text
┌────────────────┐
│ Potenciómetro  │
└───────┬────────┘
        │
        │ Señal analógica
        ▼
┌────────────────┐
│     ESP32      │
│      ADC       │
└───────┬────────┘
        │
        │ Wi-Fi
        ▼
┌────────────────┐
│    Internet    │
└───────┬────────┘
        │
        ▼
┌────────────────────┐
│ Arduino IoT Cloud  │
└────────────────────┘
```

---

## 💻 ¿Cómo se trabajó el código?

Para establecer la comunicación con Arduino IoT Cloud se utilizaron las librerías:

```cpp
#include <ArduinoIoTCloud.h>
#include <Arduino_ConnectionHandler.h>
```

También se definió una variable para almacenar el voltaje:

```cpp
float voltaje;
```

El funcionamiento del programa fue:

```text
Lectura del potenciómetro
          ↓
       Valor ADC
          ↓
 Cálculo del promedio
          ↓
Conversión a voltaje
          ↓
 Variable "voltaje"
          ↓
     Conexión Wi-Fi
          ↓
  Arduino IoT Cloud
```

De esta manera, un dato obtenido físicamente por la ESP32 pudo ser enviado a través de Internet.

---

## ⚙️ Procedimiento

1. Se conectó el potenciómetro a la ESP32.
2. Se configuró la conexión Wi-Fi.
3. Se configuró el dispositivo en Arduino IoT Cloud.
4. Se creó la variable correspondiente al voltaje.
5. Se vinculó la variable con el programa.
6. Se cargó el código en la ESP32.
7. Se realizaron las lecturas analógicas.
8. Se calculó el voltaje.
9. La ESP32 transmitió el valor hacia la nube.
10. Se verificaron los resultados.

---

## 📊 Resultado

Durante la prueba se observaron registros como:

```text
Promedio Digital: 4095.00
Voltaje en la Nube: 3.300 V
```

Cuando el ADC alcanzó su valor máximo, el voltaje calculado también alcanzó aproximadamente el máximo utilizado en la conversión.

Esto permitió comprobar la comunicación:

```text
Mundo físico → ESP32 → Internet → Plataforma IoT
```

---

## 📸 Evidencias

<p align="center">
<img width="430" alt="ESP32 ejercicio 3" src="https://github.com/user-attachments/assets/204e30b3-dea7-45df-83ae-5d561f6c2e1a" />
</p>

<p align="center">
<b>Figura 4.</b> Montaje utilizado para la adquisición de la señal.
</p>

<p align="center">
<img width="950" alt="Arduino IoT Cloud ejercicio 3" src="https://github.com/user-attachments/assets/18337ea3-10b3-425b-9173-233a8568fcab" />
</p>

<p align="center">
<b>Figura 5.</b> Programa y resultados obtenidos durante la comunicación con Arduino IoT Cloud.
</p>

---

# 🌡️ Ejercicio 4 – Medición de temperatura

## 🎯 Objetivo

Obtener mediciones de temperatura mediante la ESP32 y procesar los datos para expresarlos en grados Celsius.

---

## 🧰 Materiales y recursos

- ESP32
- Sensor utilizado para la medición de temperatura
- Cables jumper
- Cable USB
- Computadora
- Arduino IDE
- Conexión requerida para la plataforma utilizada

---

## 🔌 Funcionamiento

El sensor adquiere información relacionada con la temperatura del entorno.

La ESP32 recibe esta información y la procesa para obtener una lectura expresada en grados Celsius.

```text
🌡️ Temperatura ambiental
           ↓
        Sensor
           ↓
         ESP32
           ↓
  Adquisición de datos
           ↓
     Procesamiento
           ↓
  Temperatura en °C
           ↓
Visualización del resultado
```

---

## 💻 ¿Cómo se trabajó el código?

El programa fue estructurado para realizar de forma repetitiva las siguientes operaciones:

```text
1. Inicializar el sistema
           ↓
2. Leer el sensor
           ↓
3. Procesar la señal
           ↓
4. Obtener la temperatura
           ↓
5. Mostrar el valor en °C
           ↓
6. Realizar una nueva lectura
```

La repetición continua permite observar cómo cambia la temperatura con el tiempo.

---

## ⚙️ Procedimiento

1. Se preparó la ESP32.
2. Se realizaron las conexiones necesarias.
3. Se cargó el programa mediante Arduino IDE.
4. Se inicializó el sistema.
5. Se adquirieron los datos del sensor.
6. La ESP32 procesó las mediciones.
7. Los valores fueron convertidos a temperatura.
8. Se visualizaron los resultados.

---

## 📊 Resultados

Durante la prueba se observaron mediciones cercanas a:

```text
27 °C – 28 °C
```

Las lecturas consecutivas presentaron pequeñas variaciones, correspondientes a los cambios detectados durante la adquisición.

---

## 📸 Evidencias

<p align="center">
<img width="850" alt="Medición de temperatura" src="https://github.com/user-attachments/assets/d57e5881-2892-4e8b-9931-1ce1d8bed4ca" />
</p>

<p align="center">
<b>Figura 6.</b> Obtención de valores de temperatura mediante la ESP32.
</p>

<p align="center">
<img width="430" alt="Montaje temperatura" src="https://github.com/user-attachments/assets/d6536bf7-5134-49ab-81fa-037ab0c66239" />
</p>

<p align="center">
<b>Figura 7.</b> Evidencia experimental del sistema utilizado.
</p>

---

# 💡 Ejercicio 5 – Control remoto de un LED

## 🎯 Objetivo

Implementar un servidor web utilizando la ESP32 para controlar remotamente el encendido y apagado de un LED mediante una interfaz accesible desde un navegador.

---

## 🧰 Materiales utilizados

- ESP32
- LED
- Resistencia
- Protoboard
- Cables jumper
- Cable USB
- Computadora
- Arduino IDE
- Red Wi-Fi
- Navegador web

---

## 🔌 Explicación de las conexiones

El LED funciona como un actuador digital.

En el código se definió:

```cpp
const int ledPin = 2;
```

Por lo tanto, el control lógico se realizó mediante el **GPIO 2**.

La conexión general fue:

```text
ESP32
GPIO 2
   │
   ▼
Resistencia
   │
   ▼
  LED
   │
   ▼
  GND
```

La resistencia se utiliza para limitar la corriente que circula a través del LED.

---

## 🌐 Arquitectura del sistema

En esta actividad la ESP32 no solamente se conecta a la red, sino que también funciona como un pequeño servidor web.

```text
┌─────────────────┐
│ Navegador web   │
│ PC / Teléfono   │
└────────┬────────┘
         │
         │ Wi-Fi / HTTP
         ▼
┌─────────────────┐
│      ESP32      │
│  Servidor Web   │
└────────┬────────┘
         │
         │ GPIO 2
         ▼
┌─────────────────┐
│       LED       │
└─────────────────┘
```

---

## 💻 ¿Cómo se trabajó el código?

Primero se incluyó:

```cpp
#include <WiFi.h>
```

Luego se configuró el servidor web:

```cpp
WiFiServer server(80);
```

El puerto **80** corresponde al puerto comúnmente utilizado para comunicación HTTP.

El LED fue configurado como salida:

```cpp
const int ledPin = 2;

pinMode(ledPin, OUTPUT);
digitalWrite(ledPin, LOW);
```

Al iniciar el sistema, el LED permanece apagado.

---

### 📡 Conexión Wi-Fi

El programa establece la conexión mediante:

```cpp
WiFi.begin(ssid, password);
```

Después espera hasta obtener una conexión:

```cpp
while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
}
```

Finalmente muestra la dirección IP:

```cpp
Serial.println(WiFi.localIP());
```

Esta dirección IP es utilizada desde el navegador para ingresar al servidor de la ESP32.

---

### 🌐 Interfaz web

La ESP32 genera una página HTML con dos botones:

```text
┌─────────────────────────────┐
│   Control de LED - ESP32    │
│                             │
│     [ ENCENDER LED ]        │
│                             │
│      [ APAGAR LED ]         │
└─────────────────────────────┘
```

Los botones generan solicitudes diferentes.

Para encender:

```text
GET /ON
```

Para apagar:

```text
GET /OFF
```

---

### 💡 Control del LED

El programa analiza la solicitud recibida.

Para encender:

```cpp
if (currentLine.endsWith("GET /ON")) {
    digitalWrite(ledPin, HIGH);
}
```

Para apagar:

```cpp
if (currentLine.endsWith("GET /OFF")) {
    digitalWrite(ledPin, LOW);
}
```

Por lo tanto:

```text
Botón ENCENDER
      ↓
GET /ON
      ↓
ESP32
      ↓
GPIO = HIGH
      ↓
💡 LED ENCENDIDO
```

y:

```text
Botón APAGAR
      ↓
GET /OFF
      ↓
ESP32
      ↓
GPIO = LOW
      ↓
⚫ LED APAGADO
```

---

## 🧾 Código utilizado

> 🔐 Las credenciales originales fueron reemplazadas por valores genéricos para evitar publicar información privada.

```cpp
#include <WiFi.h>

// Credenciales Wi-Fi
const char* ssid = "TU_RED_WIFI";
const char* password = "TU_PASSWORD";

// Servidor web en puerto 80
WiFiServer server(80);

// Pin digital del LED
const int ledPin = 2;

void setup() {

  Serial.begin(115200);

  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW);

  Serial.print("Conectando a la red ");
  Serial.println(ssid);

  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("WiFi conectado");

  Serial.print("Direccion IP para controlar el LED: ");
  Serial.println(WiFi.localIP());

  server.begin();
}

void loop() {

  WiFiClient client = server.available();

  if (client) {

    String currentLine = "";

    while (client.connected()) {

      if (client.available()) {

        char c = client.read();

        if (c == '\n') {

          if (currentLine.length() == 0) {

            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println();

            client.print("<html>");
            client.print("<head>");
            client.print("<meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">");

            client.print("<style>");
            client.print("body{font-family:Arial;text-align:center;margin-top:50px;}");
            client.print(".btn{background-color:#4CAF50;color:white;padding:15px 32px;font-size:20px;text-decoration:none;border-radius:8px;}");
            client.print(".btn-off{background-color:#f44336;}");
            client.print("</style>");

            client.print("</head>");

            client.print("<body>");

            client.print("<h1>Control de LED - ESP32</h1>");

            client.print("<p>");
            client.print("<a href=\"/ON\">");
            client.print("<button class=\"btn\">ENCENDER LED</button>");
            client.print("</a>");
            client.print("</p>");

            client.print("<p>");
            client.print("<a href=\"/OFF\">");
            client.print("<button class=\"btn btn-off\">APAGAR LED</button>");
            client.print("</a>");
            client.print("</p>");

            client.print("</body>");
            client.print("</html>");

            client.println();

            break;

          } else {

            currentLine = "";
          }

        } else if (c != '\r') {

          currentLine += c;
        }

        if (currentLine.endsWith("GET /ON")) {
          digitalWrite(ledPin, HIGH);
        }

        if (currentLine.endsWith("GET /OFF")) {
          digitalWrite(ledPin, LOW);
        }
      }
    }

    client.stop();
  }
}
```

---

## ⚙️ Procedimiento

1. Se montó la ESP32 en la protoboard.
2. Se conectó el LED.
3. Se agregó la resistencia correspondiente.
4. Se conectó el LED al GPIO configurado.
5. Se configuró la red Wi-Fi.
6. Se cargó el programa.
7. La ESP32 se conectó a la red.
8. Se obtuvo la dirección IP mediante el monitor serial.
9. Se ingresó la dirección IP desde un navegador.
10. Se abrió la interfaz web.
11. Se presionó **ENCENDER LED**.
12. La ESP32 recibió `/ON`.
13. El LED se encendió.
14. Se presionó **APAGAR LED**.
15. La ESP32 recibió `/OFF`.
16. El LED se apagó.

---

## 📸 Evidencias

### LED apagado

<p align="center">
<img width="430" alt="LED apagado" src="https://github.com/user-attachments/assets/e398a353-8a5f-40eb-8e62-8b7b2de1a47a" />
</p>

<p align="center">
<b>Figura 8.</b> Estado del montaje con el LED apagado.
</p>

### LED encendido

<p align="center">
<img width="430" alt="LED encendido" src="https://github.com/user-attachments/assets/c7840334-b03e-4f52-a085-53c79a4d6236" />
</p>

<p align="center">
<b>Figura 9.</b> Activación del LED mediante la ESP32.
</p>

---

# 🔄 Flujo general de funcionamiento

Las cinco actividades permitieron avanzar progresivamente desde una lectura local hasta un sistema conectado.

```text
┌──────────────────────────────┐
│ 1. ADQUISICIÓN DE DATOS      │
│ Potenciómetro / Sensor       │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 2. ESP32                     │
│ Lectura mediante ADC/GPIO    │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 3. PROCESAMIENTO             │
│ Promedio / Conversión        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 4. CONECTIVIDAD              │
│ Wi-Fi                        │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 5. IoT                       │
│ Arduino IoT Cloud / Web      │
└──────────────┬───────────────┘
               ↓
┌──────────────────────────────┐
│ 6. VISUALIZACIÓN / CONTROL   │
│ Datos o control del LED      │
└──────────────────────────────┘
```

---

# 🧠 ¿Qué se aprendió durante estas actividades?

Las actividades permitieron comprender que un sistema IoT no está compuesto únicamente por un sensor o una conexión a Internet.

Existe una cadena completa de funcionamiento:

```text
ENTRADA
   ↓
ADQUISICIÓN
   ↓
PROCESAMIENTO
   ↓
COMUNICACIÓN
   ↓
PLATAFORMA
   ↓
VISUALIZACIÓN
   ↓
CONTROL
```

En los primeros ejercicios, la ESP32 trabajó principalmente como un sistema de adquisición.

Posteriormente se incorporó Wi-Fi, permitiendo que el dispositivo se comunicara con otros sistemas.

Finalmente, la comunicación dejó de ser únicamente de salida, ya que mediante el servidor web fue posible enviar una instrucción desde un usuario hacia la ESP32 para controlar físicamente un LED.

---

# 📊 Resumen de actividades

| Ejercicio | Entrada | Procesamiento | Comunicación | Resultado |
|---|---|---|---|---|
| **1** | Potenciómetro | ADC + promedio + conversión | Serial | Voltaje |
| **2** | Credenciales Wi-Fi | Gestión de conexión | Wi-Fi | Dirección IP |
| **3** | Potenciómetro | ADC → voltaje | Wi-Fi + IoT Cloud | Variable en la nube |
| **4** | Sensor de temperatura | Conversión a °C | Sistema digital | Temperatura |
| **5** | Orden del usuario | Solicitud HTTP | Wi-Fi | Control del LED |

---

# 🔍 Diferencia entre monitoreo y control

Durante el taller se trabajaron dos conceptos importantes.

### 📊 Monitoreo

Consiste en adquirir información del entorno y enviarla hacia el usuario.

```text
Sensor → ESP32 → Internet → Usuario
```

Ejemplos desarrollados:

- Voltaje del potenciómetro.
- Temperatura.
- Variables transmitidas hacia una plataforma IoT.

### 🎮 Control

Consiste en que el usuario envíe una orden hacia el dispositivo.

```text
Usuario → Internet / Wi-Fi → ESP32 → Actuador
```

Ejemplo desarrollado:

```text
Usuario
   ↓
Botón web
   ↓
ESP32
   ↓
LED
```

La combinación de ambos conceptos permite desarrollar sistemas IoT más completos.

---

# 💡 Importancia de la ESP32 en el sistema

La ESP32 funcionó como el elemento central de las actividades.

Sus principales funciones fueron:

- Adquirir señales analógicas.
- Procesar información.
- Convertir lecturas digitales a magnitudes físicas.
- Conectarse a redes Wi-Fi.
- Comunicarse con plataformas IoT.
- Ejecutar un servidor web.
- Recibir instrucciones remotas.
- Controlar actuadores.

Por lo tanto, puede representarse como:

```text
                 ┌───────────────┐
Sensores ───────►│               │──────► Internet
                 │     ESP32     │
Usuario ◄───────►│               │──────► Actuadores
                 └───────────────┘
```

---

# ⚠️ Consideraciones importantes

- Verificar siempre las conexiones antes de energizar el circuito.
- Compartir una tierra común (`GND`) cuando sea necesario.
- Verificar qué pines de la ESP32 permiten lectura analógica.
- No superar los niveles de voltaje permitidos por las entradas de la ESP32.
- Utilizar resistencias de protección con los LED.
- Verificar el puerto serial correcto antes de cargar un programa.
- Confirmar que la ESP32 y el dispositivo de control estén conectados a la red correspondiente cuando la actividad lo requiera.
- No publicar contraseñas Wi-Fi, claves privadas o credenciales de servicios IoT en GitHub.

---

# 🔐 Seguridad de credenciales

Durante las actividades se utilizaron credenciales de Wi-Fi y servicios IoT.

Estas credenciales **no deben mantenerse visibles en un repositorio público**.

En lugar de:

```cpp
const char* ssid = "RED_REAL";
const char* password = "CONTRASEÑA_REAL";
```

se recomienda publicar:

```cpp
const char* ssid = "TU_RED_WIFI";
const char* password = "TU_PASSWORD";
```

Lo mismo aplica para:

- Device Keys
- API Keys
- Tokens
- Contraseñas
- Credenciales MQTT
- Secret Keys de plataformas IoT

---

# ✅ Conclusiones

1. Se logró utilizar la **ESP32 como plataforma principal para adquisición, procesamiento y comunicación de datos**, comprobando su utilidad en aplicaciones de Internet de las Cosas.

2. La lectura del potenciómetro permitió comprender el funcionamiento del **convertidor analógico-digital (ADC)** y la relación entre un valor digital y su voltaje equivalente.

3. La conexión Wi-Fi permitió ampliar el funcionamiento de la ESP32 desde un dispositivo local hacia un dispositivo capaz de comunicarse mediante una red.

4. La integración con **Arduino IoT Cloud** permitió comprobar que una variable obtenida físicamente puede ser transmitida y utilizada dentro de una plataforma IoT.

5. La adquisición de temperatura permitió aplicar el concepto de **sensor → procesamiento → información**, obteniendo una magnitud física interpretable por el usuario.

6. El control del LED mediante un servidor web demostró que la comunicación también puede realizarse en sentido contrario, permitiendo que un usuario envíe instrucciones hacia la ESP32.

7. En conjunto, las actividades permitieron comprender la estructura básica de un sistema IoT, integrando **sensores, ESP32, procesamiento, Wi-Fi, servicios de Internet, visualización y actuadores**.

---

<p align="center">
  <b>🌐 ESP32 + Sensores + Wi-Fi + IoT = Sistema conectado</b>
</p>

<p align="center">
  <i>Taller de Internet of Things (IoT)</i>
</p>
