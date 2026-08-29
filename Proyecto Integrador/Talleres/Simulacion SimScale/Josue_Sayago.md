## Descripción de la Simulación

Para evaluar la resistencia estructural de los puntos de montaje de la placa, se realizó una simulación aplicando una fuerza horizontal de 5 N directamente sobre las caras internas de los cuatro orificios cilíndricos. 

La fuerza aplicada busca representar el empuje lateral o la carga de corte que experimentan las uniones (como pernos o pasadores) cuando el ensamblaje es sometido a un esfuerzo transversal durante su operación. Para este análisis, se restringió el movimiento del componente configurando un soporte fijo (*fixed support*) sobre el cuerpo principal de la estructura, lo que permite evaluar cómo se distribuye la tensión al resistir esta tracción en los anclajes.

<img width="1872" height="876" alt="Captura de pantalla 2026-08-27 194944" src="https://github.com/user-attachments/assets/f2ef3d05-96d8-4b70-9cc0-232a3abd1c00" />


## Análisis de Esfuerzos

Debido a que el esfuerzo máximo obtenido (40.96 kPa) es extremadamente bajo para cualquier material de fabricación estándar, como el PLA o resinas de impresión, el análisis indica que, bajo una carga estática horizontal de 5 N, la zona de las fijaciones no presenta un nivel de riesgo estructural.

## Conclusión

La simulación permitió identificar que los bordes de los cuatro orificios cilíndricos son puntos donde se concentra tensión, debido a la resistencia que oponen al recibir directamente la fuerza horizontal mientras el cuerpo de la pieza se mantiene restringido por el soporte fijo.

Sin embargo, para la condición evaluada de 5 N (que representa un empuje lateral), los esfuerzos de Von Mises generados son insignificantes en comparación con el límite de fluencia de cualquier plástico, en este caso PLA. Por lo tanto, el diseño presenta un comportamiento estructural sumamente robusto frente a la carga estática considerada, garantizando que los anclajes no sufrirán desgarros ni deformaciones permanentes.
