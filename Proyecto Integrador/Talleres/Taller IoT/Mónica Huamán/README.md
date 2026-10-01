<div align="center">

# Taller de Internet de las Cosas (IoT)

### Adquisición, transmisión y control de datos mediante ESP32

**Estudiante:** Mónica Huamán Bernal  
**Equipo:** Equipo 06  
**Curso:** [Nombre del curso]

<br>

![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white)
![Arduino](https://img.shields.io/badge/Arduino-00979D?style=for-the-badge&logo=arduino&logoColor=white)
![Arduino Cloud](https://img.shields.io/badge/Arduino_Cloud-00979D?style=for-the-badge&logo=arduino&logoColor=white)
![ThingSpeak](https://img.shields.io/badge/ThingSpeak-2D8CFF?style=for-the-badge)
![Ubidots](https://img.shields.io/badge/Ubidots-111827?style=for-the-badge)

</div>

---

## 1. Descripción

En este taller se desarrollaron cinco ejercicios orientados al uso del **ESP32** en aplicaciones de Internet de las Cosas (IoT).

Se trabajó con la adquisición y procesamiento de señales, conexión inalámbrica, transmisión de datos hacia plataformas en la nube y control remoto de un actuador.

Los ejercicios desarrollados fueron:

- **Ejercicio 01:** Adquisición de datos mediante un potenciómetro.
- **Ejercicio 02:** Conexión del ESP32 a una red Wi-Fi.
- **Ejercicio 03:** Envío de datos del potenciómetro a plataformas IoT.
- **Ejercicio 04:** Envío de datos de un sensor del kit Keystudio a plataformas IoT.
- **Ejercicio 05:** Control de un LED desde una plataforma IoT.

---

## 2. Herramientas y plataformas utilizadas

| Herramienta / plataforma | Uso |
| :----------------------- | :--------------------------------------------- |
| **ESP32 DevKit V1** | Adquisición, procesamiento y comunicación |
| **Arduino IDE** | Programación y carga del código |
| **Arduino Cloud** | Gestión y visualización de datos IoT |
| **ThingSpeak** | Almacenamiento y visualización de datos |
| **Ubidots** | Monitoreo y visualización de variables |
| **Protoboard** | Montaje de los circuitos |
| **Sensores Keystudio** | Generación de señales de entrada |

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

```cpp
long suma = 0;

for (int i = 0; i < numLecturas; i++) {
  suma += analogRead(potPin);
  delay(10);
}

float promedioADC = suma / (float)numLecturas;
