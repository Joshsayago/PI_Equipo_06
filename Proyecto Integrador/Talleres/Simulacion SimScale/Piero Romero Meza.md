# Justificación Técnica del Torque de Ensamblaje

En esta sección se detalla la selección y validación del momento de fuerza aplicado en la simulación de la columna plástica.

## Parámetros de Diseño
* **Componente:** Columna plástica de fijación (*boss*)
* **Material:** Ácido Poliláctico (**PLA**)
* **Torque Seleccionado:** **5 Nmm** (0.005 Nm)

## Justificación del Torque

Elegí un torque de **5 Nmm** porque es la fuerza ideal para ajustar un tornillo pequeño en una pieza de 
**plástico PLA** sin romperla. Como el PLA es un material que se puede agrietar o barrer fácilmente si se 
aprieta de más, este valor asegura que el tornillo quede **firme y bien sujeto**. Al mismo tiempo, es lo 
suficientemente suave para cuidar la estructura de la columna plástica, evitando que las capas se separen o 
que la rosca interna se dañe durante el armado.

### ¿Por qué tiene sentido este número con el PLA?
* **Cuida el material:** El PLA impreso en 3D es rígido pero quebradizo; 5 Nmm es un toque sutil que no lo estresa.
* **Fijación segura:** Es la fuerza justa para que las piezas no queden sueltas en su posición final.

## Resultados de la Simulación
![Resultados de la simulación de torque](Recursos/Imágenes/PIERO_taller2.png)
