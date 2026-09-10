# Justificación Técnica del Torque de Ensamblaje

En esta sección se detalla la selección y validación del momento de fuerza aplicado en la simulación de la columna plástica.

## Parámetros de Diseño
* **Componente:** Columna plástica de fijación (*boss*)
* **Material:** Ácido Poliláctico (PLA), límite de fluencia típico σy ≈ 50–70 MPa (impresión FDM, varía según orientación de capas e infill)
* **Torque Seleccionado:** **5 Nmm** (0.005 Nm)
* **Condiciones de contorno:** Gravedad de 9.81 m/s² aplicada en dirección Y, torque de 5 Nmm aplicado sobre la cara superior del boss, simulando el momento transmitido por el tornillo durante el ensamblaje

## Justificación del Torque

Elegí un torque de 5 Nmm porque es la fuerza ideal para ajustar un tornillo pequeño en una pieza de plástico PLA sin romperla. Como el PLA es un material que se puede agrietar o barrer fácilmente si se aprieta de más, este valor asegura que el tornillo quede firme y bien sujeto. Al mismo tiempo, es lo suficientemente suave para cuidar la estructura de la columna plástica, evitando que las capas se separen o que la rosca interna se dañe durante el armado.

### ¿Por qué tiene sentido este número con el PLA?
* Cuida el material: El PLA impreso en 3D es rígido pero quebradizo; 5 Nmm es un toque sutil que no lo estresa, quedando muy por debajo de su límite de fluencia (50-70 MPa).
* Fijación segura: Es la fuerza justa para que las piezas no queden sueltas en su posición final.
  
## Resultados de la Simulación:
La simulación en SimScale (Run 2/3, análisis estático estructural) muestra la distribución de esfuerzo de Von Mises bajo la carga combinada de gravedad y torque de ensamblaje:

* Esfuerzo máximo: 8.919×10⁵ Pa (≈ 0.89 MPa)
* Ubicación del esfuerzo máximo: concentrado en la base de la columna (boss) donde se aplica el torque, mientras que el resto de la carcasa presenta esfuerzos prácticamente nulos.
* Esfuerzo mínimo: 1.834×10⁻² Pa, en las zonas alejadas del punto de aplicación de carga
<img width="1918" height="968" alt="image" src="https://github.com/user-attachments/assets/b1e02ee9-5392-473b-b451-10f2d7be4e0f" />
* Interpretación de Resultados:
Comparando el esfuerzo máximo obtenido (0.89 MPa) contra el límite de fluencia del PLA (50–70 MPa), se obtiene un factor de seguridad aproximado de 56 a 78, muy por encima del mínimo recomendado en diseño mecánico (usualmente FS ≥ 2–3 para prototipos funcionales). Esto confirma que el torque de 5 Nmm es una carga segura para el boss de PLA: el material trabaja muy por debajo de su límite elástico, sin riesgo de fractura, delaminación entre capas ni deformación permanente.

La concentración del esfuerzo en la base del boss es consistente con el comportamiento esperado de una carga torsional aplicada sobre una columna cilíndrica: es el punto de mayor momento flector/torsor, y confirma que la geometría actual del boss distribuye adecuadamente la carga hacia el resto de la estructura sin transmitir esfuerzos significativos a la carcasa.

