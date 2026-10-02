# Ejercicios IoT con ESP32

## Descripción

En esta práctica se desarrollaron diferentes ejercicios utilizando el **ESP32**, con el objetivo de trabajar con entradas analógicas, conexión Wi-Fi, sensores, plataformas IoT y control de dispositivos mediante una interfaz web.

---

## Ejercicio 1 - Lectura ADC y conversión a voltaje

### Objetivo

Mejorar la lectura de un potenciómetro conectado al ESP32 mediante el **promediado de varias muestras** y convertir el valor obtenido por el ADC a su equivalente en voltaje.

### Desarrollo

El potenciómetro fue conectado a una entrada analógica del ESP32. El programa realiza varias lecturas del ADC y las acumula para posteriormente calcular un promedio.

Luego, el promedio digital obtenido se convierte a voltaje considerando que el ADC del ESP32 trabaja con valores entre **0 y 4095**, correspondientes aproximadamente al rango de **0 a 3.3 V**.

La conversión utilizada es:

```text
Voltaje = (Promedio ADC × 3.3) / 4095
```

El uso del promedio permite obtener una lectura más estable y reducir pequeñas variaciones producidas durante la adquisición de los datos.

### Resultado

En el monitor serial se visualizaron tanto el **promedio digital** como su **voltaje equivalente**. Por ejemplo, para valores cercanos a 1940 en el ADC se obtuvieron voltajes aproximados de 1.56 V.

<p align = center>
  <img width="600" height="800" alt="image" src="https://github.com/user-attachments/assets/1780c640-7383-4ed2-95a1-272ec31986e9" />
  <br>
  <em>Montaje del ESP32 y potenciómetro utilizado para realizar las lecturas analógicas.</em>
</p>

<p align = center>
  <img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/0268106b-1432-4bd6-a9d6-b48eb28f0869" />
  <br>
  <em>Visualización del promedio de las lecturas ADC y su conversión a voltaje en Arduino IDE.</em>
</p>

---

## Ejercicio 2 - Conexión Wi-Fi con ESP32

### Objetivo

Crear una red Wi-Fi utilizando un smartphone como **Hotspot** y conectar el ESP32 a dicha red, mostrando posteriormente la dirección IP asignada en el monitor serial.

### Desarrollo

Se utilizó la librería `WiFi.h` para configurar la conexión inalámbrica del ESP32.

En el programa se especificaron las credenciales de la red Wi-Fi y posteriormente se utilizó `WiFi.begin()` para iniciar la conexión.

El programa espera hasta que el ESP32 consiga conectarse correctamente. Una vez establecida la conexión, se utiliza:

```cpp
WiFi.localIP()
```

para obtener la dirección IP asignada al ESP32 dentro de la red.

### Resultado

El ESP32 consiguió conectarse correctamente al Hotspot creado desde el smartphone y el monitor serial mostró la dirección IP asignada al dispositivo.

### Evidencia

<p align = center>
<img width="1600" height="999" alt="image" src="https://github.com/user-attachments/assets/ac497d10-c750-4a72-9562-08d9fcdf75b9" />
</p>

---

## Ejercicio 3 - Envío de datos a la nube

### Objetivo

Mostrar en tiempo real la variación de un **potenciómetro conectado al ESP32** mediante una plataforma IoT.

### Desarrollo

Se conectó un potenciómetro a una entrada analógica del ESP32 para obtener diferentes valores dependiendo de la posición de este.

El ESP32 realiza las lecturas del ADC, calcula el valor correspondiente y se conecta mediante Wi-Fi a **Arduino Cloud**.

Se configuró una variable compartida para enviar los datos obtenidos desde el ESP32 hacia la nube. De esta manera, los cambios realizados físicamente en el potenciómetro pueden visualizarse desde un dashboard.

El funcionamiento general fue:

```text
Potenciómetro
     ↓
    ESP32
     ↓
Lectura ADC
     ↓
Conversión a voltaje
     ↓
Conexión Wi-Fi
     ↓
Arduino Cloud
     ↓
Dashboard
```

### Resultado

Se consiguió enviar correctamente el valor obtenido por el ESP32 hacia Arduino Cloud y visualizar su variación desde el dashboard.

### Evidencias

<p align = center>
  <img width="225" height="400" alt="image" src="https://github.com/user-attachments/assets/521b11df-294a-483e-8e70-2cebd3165378" />
  <br>
  <em>ESP32 utilizado para realizar la conexión con la plataforma IoT.</em>
</p>

<p align = center>
<img width="225" height="400" alt="image" src="https://github.com/user-attachments/assets/613f529e-cd96-46a9-b153-a799046c25fc" />
</p>

<p align = center>
<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/065cec96-11de-403c-86d8-3975b3c5d3d1" />
  <br>
  <em>Lecturas obtenidas por el ESP32 y configuración para el envío de datos.</em>
</p>

<p align = center>
<img width="800" height="175" alt="image" src="https://github.com/user-attachments/assets/f2bb8158-593b-47f0-9b8e-b0183785e5e8" />
  <br>
  <em>Visualización del valor enviado por el ESP32 en el dashboard de Arduino Cloud.</em>
</p>

---

## Ejercicio 4 - Sensor LM35 y Arduino Cloud

### Objetivo

Utilizar uno de los sensores del kit para obtener información del entorno y visualizar los datos en tiempo real mediante una plataforma IoT.

### Desarrollo

Para este ejercicio se utilizó el **sensor de temperatura LM35** conectado al ESP32.

El ESP32 obtiene la señal entregada por el sensor y la procesa para determinar la temperatura correspondiente en **grados Celsius (°C)**.

Posteriormente, el ESP32 se conecta mediante Wi-Fi a **Arduino Cloud** y actualiza una variable con la temperatura obtenida.

El funcionamiento realizado fue:

```text
Sensor LM35
     ↓
    ESP32
     ↓
Lectura del sensor
     ↓
Conversión a temperatura
     ↓
Conexión Wi-Fi
     ↓
Arduino Cloud
     ↓
Dashboard
```

### Resultado

El monitor serial mostró las mediciones realizadas por el sensor, obteniéndose durante las pruebas temperaturas aproximadas entre **26 °C y 28 °C**.

Además, los datos fueron enviados correctamente a Arduino Cloud, permitiendo visualizar la temperatura desde el dashboard.

### Evidencias

<p align = center>
  <img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/9a174745-734c-470d-a3ae-cf4dde15b15b" />
  <br>
  <em>Montaje utilizado para realizar la lectura de temperatura con el ESP32.</em>
</p>

<p align = center>
<img width="900" height="1600" alt="image" src="https://github.com/user-attachments/assets/a998eaae-d1ae-41b8-83a9-fb3f57b10fe5" />
  <br>
  <em>Lecturas de temperatura y conexión del ESP32 con Arduino IoT Cloud.</em>
</p>

<p>
  <img width="1600" height="999" alt="image" src="https://github.com/user-attachments/assets/25e907bf-dae5-485e-8919-1e6c413a64c7" />
  <br>
  <em>Temperatura enviada por el ESP32 y visualizada desde Arduino Cloud.</em>
</p>

---

## Ejercicio 5 - Control de un LED mediante una interfaz web

### Objetivo

Conectar un LED a uno de los pines digitales del ESP32 y controlar su encendido y apagado mediante una plataforma web.

### Desarrollo

Se conectó un LED al ESP32 y se configuró el **GPIO 2** como una salida digital.

El ESP32 se conecta a una red Wi-Fi y crea un servidor web utilizando:

```cpp
WiFiServer server(80);
```

Una vez conectado, el ESP32 muestra su dirección IP en el monitor serial. Esta dirección puede introducirse en el navegador de un dispositivo conectado a la misma red.

El propio ESP32 genera una página web que contiene dos botones:

```text
ENCENDER LED
APAGAR LED
```

Cuando el usuario selecciona **ENCENDER LED**, el navegador realiza una petición `/ON` y el ESP32 coloca el pin del LED en estado `HIGH`.

Cuando se selecciona **APAGAR LED**, se realiza una petición `/OFF` y el pin cambia a estado `LOW`.

El funcionamiento general es:

```text
Navegador
    ↓
Dirección IP del ESP32
    ↓
Servidor web ESP32
    ↓
   /ON  → Encender LED
   /OFF → Apagar LED
    ↓
LED conectado al GPIO 2
```

### Resultado

Se consiguió controlar el estado del LED desde una interfaz web, permitiendo encenderlo y apagarlo mediante comandos enviados por Wi-Fi al ESP32.

### Evidencia

<p align = center>
  <img width="720" height="1280" alt="image" src="https://github.com/user-attachments/assets/caac6fdd-0b65-4e6b-937c-8bc15baf5ed8" />
  <br>
  <em>Montaje del ESP32 con el LED utilizado para realizar el control mediante Wi-Fi.</em>
</p>

---

## Conclusión

Se realizaron pruebas de envío de información hacia **Arduino Cloud**, utilizando un potenciómetro y un sensor LM35. Finalmente, se implementó el proceso inverso, utilizando la conectividad del ESP32 para controlar un LED mediante una interfaz web.

De esta manera, se trabajaron dos aspectos importantes de un sistema IoT: el **monitoreo de datos obtenidos mediante sensores** y el **control de dispositivos a través de una red**.
