# Diseño electrónico del sistema

Para el desarrollo del sistema portátil de detección y registro de grietas se realizó el diseño electrónico considerando como componente principal la **XIAO ESP32S3 Sense**. El proceso comprende la elaboración del esquemático, el diseño de la placa de circuito impreso (PCB) y su posterior visualización mediante un modelo 3D.

---

## 1. Esquemático electrónico

<img width="828" height="583" alt="Esquemático electrónico" src="https://github.com/user-attachments/assets/4c2ff090-9545-4caf-979d-26896b50b646" />

El esquemático representa la **estructura eléctrica y las conexiones del circuito** desarrollado para el sistema portátil de detección de grietas. El componente principal es la **XIAO ESP32S3 Sense**, encargada del procesamiento de la información y de la integración con los demás componentes electrónicos.

En el diseño se muestran las conexiones de **alimentación de 5 V y GND**, así como los pines destinados a la conexión de la **pantalla LCD 20×4**, que permitirá visualizar información obtenida durante el funcionamiento del dispositivo.

Esta etapa permite establecer y verificar previamente las conexiones eléctricas entre los componentes, reduciendo posibles errores antes de realizar el diseño físico de la PCB.

---

## 2. Diseño de la PCB

<img width="392" height="402" alt="Diseño PCB" src="https://github.com/user-attachments/assets/669e2e0e-3cdc-4b30-9941-69f56d2b6b38" />

El diseño de la **placa de circuito impreso (PCB)** corresponde a la implementación física de las conexiones establecidas previamente en el esquemático. En esta etapa se realizó la distribución de la **XIAO ESP32S3 Sense**, los conectores y los puntos de alimentación necesarios para el funcionamiento del sistema.

Las conexiones eléctricas fueron transformadas en **pistas de cobre**, buscando mantener una distribución compacta y ordenada que facilite la integración de los componentes.

Además, se incorporaron **orificios de montaje**, destinados a permitir la fijación mecánica de la PCB dentro de la carcasa del dispositivo. De esta manera, se busca obtener una placa estable y adecuada para su utilización en un sistema portátil.

---

## 3. Modelo 3D de la PCB

### Vista frontal

<img width="687" height="678" alt="Modelo 3D - Vista frontal" src="https://github.com/user-attachments/assets/f027e86b-85ab-4b83-bfe4-3f5905e5b3d6" />

### Vista posterior

<img width="557" height="600" alt="Modelo 3D - Vista posterior" src="https://github.com/user-attachments/assets/fb5908a2-ffb4-492f-b9de-7fd4080eac76" />

El **modelo 3D** permite visualizar cómo quedaría físicamente la PCB antes de su fabricación. En las vistas frontal y posterior se puede observar la posición de la **XIAO ESP32S3 Sense**, los conectores, los orificios de montaje y la distribución general de los elementos de la placa.

Esta representación permite comprobar la **distribución espacial de los componentes**, identificar posibles interferencias y verificar que exista espacio suficiente para el montaje. Asimismo, facilita la evaluación de la compatibilidad entre la PCB y la **carcasa del sistema portátil de detección y registro de grietas**.

---

## Resultado

El desarrollo del **esquemático, PCB y modelo 3D** permitió transformar las conexiones eléctricas iniciales en una propuesta física de la placa electrónica. El diseño busca mantener una estructura **compacta, ordenada y de fácil montaje**, adecuada para su posterior integración dentro del prototipo portátil de detección y registro de grietas.
