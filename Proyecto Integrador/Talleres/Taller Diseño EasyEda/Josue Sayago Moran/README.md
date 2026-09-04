# Descripciones de las Imágenes del Proyecto PCB (EasyEDA)

Este documento contiene una breve descripción de cada una de las imágenes proporcionadas que corresponden al diseño de un circuito impreso (PCB) en la plataforma EasyEDA.

---

## 1. Diagrama Esquemático (`image_49ec86.png`)
* **Descripción:** Vista del editor de esquemáticos (`P1.Schematic1`) en EasyEDA. Muestra las conexiones lógicas entre los componentes principales del circuito:
  * **U1:** Pantalla OLED SSD1306 (128x64), conectada mediante pines SDA, SCL, VCC y GND.
  * **U2:** Componente central (microcontrolador o circuito integrado de soporte) con pines D0 a D10, alimentación y líneas de datos USB (D+, D-).
  * **U4:** Módulo GPS NEO-6M, conectado a través de pines de comunicación serial (TXD, RXD), PPS, GND y VCC.
  * **Orificios de montaje:** Varios puntos de montaje designados (MH1 a MH4) etiquetados como *Mounting Hole M3*.

---

## 2. Vista General del Diseño PCB (`image_49f392.png`)
* **Descripción:** Vista general en el editor de diseño de circuitos impresos (`PCB1`) de EasyEDA. Se observa la placa de circuito impreso en proceso de enrutamiento con su contorno morado/rosado, mostrando la distribución espacial de los componentes (la pantalla OLED a la izquierda, el circuito integrado central y el módulo GPS a la derecha), con las pistas de cobre y las capas visibles en la barra inferior.

---

## 3. Vista 3D / Renderizado de la Capa Superior (`image_49f3d0.png`)
* **Descripción:** Vista renderizada o close-up de la **capa superior (Top Layer)** de la placa de circuito impreso terminada (de color azul con pistas y serigrafía blanca). Se aprecian con claridad:
  * Los orificios metálicos dorados para los tornillos de fijación en las cuatro esquinas (MH1 a MH4).
  * Las huellas y conexiones para el display OLED, el circuito central (U2) y el módulo GPS (U4) con sus respectivas etiquetas de pines (`PPS`, `TXD`, `RXD`, `GND`, `VCC`).

---

## 4. Vista 3D / Renderizado de la Capa Inferior o Detalles de Serigrafía (`image_49f426.png`)
* **Descripción:** Vista detallada de la placa (enfocada en una de sus caras, mostrando el acabado en color azul oscuro con terminales doradas). Destaca la inclusión de elementos gráficos personalizados de serigrafía:
  * Dos escudos institucionales o decorativos con una antorcha/caduceo y la inscripción en latín *"SPIRITUS UBI VULT SPIRAT"*.
  * Pines de prueba o conexión central (`D+`, `D-`, `GND`) y los terminales de anclaje en las esquinas.
