 

<div align="center">

# Taller de Internet de las Cosas

### Adquisición, transmisión y control de datos con ESP32

**Mónica Huamán Bernal** · **Equipo 06** · **Proyecto Integrador**

<br>

<sub>
ESP32 · Arduino IDE · Arduino Cloud · ThingSpeak · Ubidots
</sub>

</div>

---

## 01 · Descripción

Este taller aborda el desarrollo de aplicaciones básicas de **Internet de las Cosas (IoT)** utilizando un ESP32 como dispositivo de adquisición, procesamiento y comunicación.

A lo largo de cinco ejercicios se trabajó progresivamente con la lectura de señales, conectividad inalámbrica, transmisión de información hacia plataformas en la nube y control remoto de un actuador.

### Ejercicios desarrollados

| | Actividad |
|:--:|:--|
| **01** | Adquisición de una señal mediante potenciómetro |
| **02** | Conexión del ESP32 a una red Wi-Fi |
| **03** | Transmisión del potenciómetro hacia plataformas IoT |
| **04** | Transmisión de datos de un sensor Keystudio |
| **05** | Control remoto de un LED |

---

## 02 · Herramientas

| Tecnología | Aplicación |
|:--|:--|
| **ESP32 DevKit V1** | Adquisición y comunicación |
| **Arduino IDE** | Desarrollo y carga del programa |
| **Arduino Cloud** | Gestión de variables y visualización |
| **ThingSpeak** | Registro y representación de datos |
| **Ubidots** | Monitoreo mediante widgets |
| **Protoboard** | Implementación de los circuitos |
| **Kit Keystudio** | Sensores de entrada |

---
---

# 3. Ejercicio 01 — Adquisición de datos con un potenciómetro

## Objetivo

Realizar la adquisición de una señal analógica mediante un potenciómetro conectado al ESP32. Además, se buscó mejorar la estabilidad de las mediciones mediante el promedio de varias lecturas y convertir el valor obtenido por el ADC a voltaje.

## Conexión del circuito

El potenciómetro fue conectado utilizando el **GPIO 34** como entrada analógica.

| Potenciómetro | ESP32 |
| :------------ | :---- |
| Terminal lateral | 3.3 V |
| Terminal lateral | GND |
| Terminal central | GPIO 34 |

El terminal central proporciona un voltaje variable según la posición del potenciómetro. Esta señal es adquirida mediante el ADC del ESP32.
<div align="center">

<<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/a80585ae-aefb-4208-a457-8a7e844b39d9" />
>

</div>

## Procesamiento de la señal

El ESP32 utiliza un ADC de 12 bits, por lo que las lecturas obtenidas pueden tomar valores entre **0 y 4095**.

Para obtener una medición más estable se realizaron varias lecturas consecutivas y se calculó su promedio:

 
long suma = 0;

for (int i = 0; i < numLecturas; i++) {
  suma += analogRead(potPin);
  delay(10);
}

float promedioADC = suma / (float)numLecturas;
 Posteriormente, el valor ADC promedio se convirtió a voltaje mediante:

~~~text
V = (ADC / 4095) × 3.3
~~~

~~~cpp
float voltaje = promedioADC * 3.3 / 4095.0;
~~~

De esta manera, al modificar la posición del potenciómetro, también cambia el valor de voltaje calculado.

## Resultados

La ejecución del programa permitió observar la variación del voltaje de acuerdo con la posición del potenciómetro.

**Interpretación**

Los resultados obtenidos muestran que el ESP32 puede adquirir correctamente una señal analógica y convertirla a un valor de voltaje.

---

# 4. Ejercicio 02 — Conexión del ESP32 a una red Wi-Fi

## Objetivo

Establecer una conexión inalámbrica entre el ESP32 y una red Wi-Fi con la finalidad de permitir posteriormente la comunicación con plataformas y servicios IoT.

## Conexión Wi-Fi

Para realizar la conexión se utilizó la biblioteca:
 
#include <WiFi.h>
~~~

El ESP32 fue configurado con el nombre y contraseña de la red correspondiente.

El programa verifica continuamente el estado de la conexión hasta establecer comunicación correctamente.

~~~cpp
WiFi.begin(ssid, password);

while (WiFi.status() != WL_CONNECTED) {
  delay(500);
  Serial.print(".");
}

Serial.println("WiFi conectado!");
Serial.println(WiFi.localIP());
~~~

Una vez establecida la conexión, se obtiene la dirección IP asignada al ESP32.

## Resultados

La ejecución del programa permitió comprobar la conexión del ESP32 a la red Wi-Fi y obtener la información correspondiente durante la prueba.

<div align="center">

<<img width="1600" height="906" alt="image" src="https://github.com/user-attachments/assets/e295d148-461d-4c50-b84a-ae3b2732981a" />
>

</div>

**Interpretación**

La conexión exitosa del ESP32 a la red permite establecer la comunicación inalámbrica necesaria para las siguientes aplicaciones IoT.

---
# 5. Ejercicio 03 — Enviando datos a la nube

## Objetivo

Enviar en tiempo real la variación del potenciómetro conectado al ESP32 hacia las siguientes plataformas de IoT:

- **Arduino Cloud**
- **ThingSpeak**
- **Ubidots**

Este ejercicio permitió integrar la adquisición de datos del ESP32 con servicios de almacenamiento y visualización en la nube.

## Arduino Cloud

Arduino IoT Cloud es una plataforma que permite conectar dispositivos IoT a Internet y gestionar sus datos desde una interfaz web.

Para este ejercicio se configuró un **Thing**, se vinculó el ESP32 y se creó la variable:

~~~text
voltaje
~~~

El valor calculado a partir de la lectura del potenciómetro fue asignado a esta variable.

### Fragmento de código

~~~cpp
voltaje = potValue * 3.3 / 4095.0;

ArduinoCloud.update();
~~~

La variable `voltaje` representa el dato que se transmite a Arduino Cloud, mientras que `ArduinoCloud.update()` permite actualizar la comunicación con la plataforma.

### Configuración

<div align="center">

<IMAGEN Q FALTA ">

</div>

### Visualización

Se creó un widget asociado a la variable `voltaje` para observar los datos enviados por el ESP32.

<div align="center">

<img src="URL_IMAGEN_ARDUINO_CLOUD" width="700">

</div>

## ThingSpeak

ThingSpeak es una plataforma IoT orientada al almacenamiento y visualización de datos provenientes de dispositivos conectados.

Para este ejercicio se configuró un canal para recibir los valores generados por el potenciómetro.

Los datos recibidos fueron representados mediante una gráfica temporal, permitiendo observar la variación de la señal.

<div align="center">

<img width="1600" height="882" alt="image" src="https://github.com/user-attachments/assets/7a75afd8-b247-404b-9c7f-f1a9c8b0c609" />


</div>

## Ubidots

Ubidots permite recibir, almacenar y visualizar datos provenientes de dispositivos IoT mediante variables y widgets.

Para este ejercicio se configuró el dispositivo ESP32 y una variable asociada al valor del potenciómetro.

Los datos recibidos fueron representados mediante un widget para observar la variación de la señal.

<div align="center">

<img width="1600" height="854" alt="image" src="https://github.com/user-attachments/assets/aba9f78b-b430-4bef-9112-e3df5d0ec32c" />


</div>

## Resultado

Se logró enviar la información obtenida mediante el potenciómetro hacia **Arduino Cloud, ThingSpeak y Ubidots**, permitiendo visualizar la variación de la señal mediante diferentes plataformas IoT.

---
# 6. Ejercicio 04 — Enviando datos a la nube parte 2

## Objetivo

Enviar en tiempo real la variación de un sensor del **kit Keystudio** conectado al ESP32 hacia:

- **Arduino Cloud**
- **ThingSpeak**
- **Ubidots**

Este ejercicio permitió aplicar el proceso de adquisición y transmisión de datos utilizando una fuente de información diferente al potenciómetro.

## Sensor utilizado

<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/f9ed1ad2-66f4-46c4-9b84-bc7053df2238" />

El sensor fue conectado al ESP32 y su señal fue adquirida mediante la entrada correspondiente.

## Adquisición de datos

El ESP32 realizó lecturas periódicas del sensor. Un fragmento representativo del proceso es:

~~~cpp
int sensorValue = analogRead(sensorPin);
~~~

El valor obtenido fue posteriormente enviado hacia las diferentes plataformas IoT.

## Arduino Cloud

Los datos obtenidos del sensor fueron asociados a una variable de Arduino Cloud y visualizados mediante un widget.

<div align="center">

<img width="1329" height="714" alt="image" src="https://github.com/user-attachments/assets/b8e5a316-fa6d-48fc-9549-4823d1c74d18" />


</div>

 

## Resultado

Se logró adquirir la señal del sensor del kit Keystudio y transmitir sus datos hacia diferentes plataformas IoT para su monitoreo en tiempo real.

---
# 7. Ejercicio 05 — Controlando desde la nube

## Objetivo

Conectar un LED a uno de los pines digitales del ESP32 y controlar su encendido y apagado desde una plataforma web.

## Conexión del circuito

El LED fue conectado a un pin digital del ESP32 mediante una resistencia para limitar la corriente.

En el montaje realizado se utilizó el **GPIO 2** como salida digital.

~~~text
GPIO 2 → Resistencia → LED → GND
~~~

## Programación

El pin utilizado para el LED fue configurado como salida digital:

~~~cpp
pinMode(LED_PIN, OUTPUT);
~~~

Para encender el LED se estableció la salida en nivel alto:

~~~cpp
digitalWrite(LED_PIN, HIGH);
~~~

Para apagarlo se utilizó:

~~~cpp
digitalWrite(LED_PIN, LOW);
~~~

## Control desde la plataforma IoT

Se configuró un elemento de control en la plataforma IoT para modificar remotamente el estado del LED.

La lógica utilizada fue:

~~~text
1 → LED encendido
0 → LED apagado
~~~

Al modificar el estado desde la plataforma web, el ESP32 recibe la instrucción y cambia el estado de la salida digital correspondiente.

## Resultados

### LED encendido

<div align="center">

<<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/2a68f328-1f7c-4b09-8e92-7677656a42ee" />
">

<<img width="1600" height="822" alt="image" src="https://github.com/user-attachments/assets/47a4ec90-7984-4c0f-801c-689bb5b62b7d" />
>

</div>

Las imágenes muestran el estado **ON** configurado desde la plataforma IoT y la respuesta correspondiente del LED conectado al ESP32.

### LED apagado

<div align="center">

<<img width="1200" height="1600" alt="image" src="https://github.com/user-attachments/assets/65be6d9b-5a2b-4603-ae73-8893cef5efe0" />
>

<<img width="1600" height="869" alt="image" src="https://github.com/user-attachments/assets/01f2b05b-5fc1-4a83-b096-9ad26aabd26b" />
>

</div>

Las imágenes muestran el estado **OFF** configurado desde la plataforma IoT y la respuesta correspondiente del LED conectado al ESP32.

## Resultado

Se logró controlar remotamente el estado de un LED conectado al ESP32 mediante una plataforma IoT, comprobando la comunicación entre la plataforma en la nube y el dispositivo físico.
------

---

## 08 · Conclusiones

El desarrollo del taller permitió integrar progresivamente los principales componentes de una aplicación IoT: **adquisición, procesamiento, conectividad, transmisión, visualización y actuación**.

El ESP32 fue utilizado como elemento central para obtener información desde diferentes entradas, establecer comunicación mediante Wi-Fi y transferir los datos hacia plataformas de monitoreo en la nube.

El trabajo con **Arduino Cloud, ThingSpeak y Ubidots** permitió comparar diferentes entornos de visualización y gestión de información provenientes del dispositivo.

Finalmente, el control remoto del LED permitió completar el flujo de comunicación entre una plataforma IoT y un elemento físico, demostrando la interacción entre el entorno virtual y el dispositivo.

---

## 09 · Referencias

- [Arduino IoT Cloud — Documentación oficial](https://docs.arduino.cc/arduino-cloud/guides/overview/)
- [Ubidots — Conexión de ESP32 mediante MQTT](https://help.ubidots.com/es/articles/748067-conectar-un-esp32-devkitc-a-ubidots-a-traves-de-mqtt)
- [ThingSpeak — Envío de datos mediante ESP32](https://todomaker.com/blog/envio-de-datos-a-thingspeak-usando-esp32/)

<br>

<div align="center">

<sub><b>PROYECTO INTEGRADOR · EQUIPO 06</b></sub>

<br>

<sub><i>Internet de las Cosas · ESP32 · IoT</i></sub>

</div>
