# 🔌 PCB — XIAO ESP32-S3 Sense + GPS NEO-6M V3

En esta carpeta se encuentran los archivos correspondientes al diseño de una PCB desarrollada en **EasyEDA**, utilizando un **ESP32-S3 Sense** como microcontrolador principal y un módulo **GPS NEO-6M V3** para la obtención de información de posicionamiento.

## 📐 Esquemático

El circuito conecta el módulo GPS con el ESP32-S3 Sense mediante comunicación serial **UART**.

Las conexiones principales realizadas fueron:

- **VCC:** alimentación del módulo GPS.
- **GND:** tierra común entre el ESP32-S3 Sense y el GPS.
- **TX/RX:** líneas utilizadas para la comunicación UART entre ambos dispositivos.
- **ESP32-S3 Sense:** encargado del procesamiento de los datos recibidos desde el GPS.

## 📂 Archivos

La carpeta contiene:

- **`schematic - Diego`** — Esquemático eléctrico del circuito.
- **`PCB - Diego`** — Archivos utilizados para la fabricación de la PCB.
- **`3D - Diego`**— Representación tridimensional de la PCB y sus componentes.

## 🎯 Objetivo

El objetivo del diseño fue aplicar el flujo básico de desarrollo de una PCB, pasando desde la elaboración del esquemático y asignación de footprints hasta el ruteo, verificación y generación de los archivos necesarios para fabricación.

---

**Diego Murga**  
Universidad Peruana Cayetano Heredia — 2026
