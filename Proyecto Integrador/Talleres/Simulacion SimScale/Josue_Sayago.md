## Descripción de la Simulación

Para evaluar la resistencia estructural de los puntos de montaje de la placa, se realizó una simulación aplicando una fuerza de 5 N directamente sobre las caras internas de los cuatro orificios cilíndricos. Para brindar mayor precisión a las condiciones de frontera, la carga se definió direccionalmente a lo largo del eje transversal de la pieza (vectorizada en la dirección del eje X), representando el empuje lateral o la carga de corte que experimentan las uniones (como pernos o pasadores) durante su operación. Asimismo, se configuró de manera precisa la acción de la gravedad, estableciendo una aceleración estándar de -9.81 m/s² en el eje vertical (dirección -Z) para considerar el efecto del peso propio del material en la distribución de las cargas.

 <img width="383" height="324" alt="image" src="https://github.com/user-attachments/assets/d4f0284b-a9fb-4fd3-beba-5502308f25bc" />
<img width="383" height="324" alt="image" src="https://github.com/user-attachments/assets/16a66db5-e0fb-4814-b80a-ca318f61e812" />  

Para este análisis, se restringió el movimiento del componente mediante un soporte fijo (*fixed support*) sobre el cuerpo principal de la estructura, lo que permite evaluar cómo se distribuye la tensión al resistir la tracción combinada en los anclajes.

<img width="1872" height="876" alt="Captura de pantalla 2026-08-27 194944" src="https://github.com/user-attachments/assets/f2ef3d05-96d8-4b70-9cc0-232a3abd1c00" />

## Análisis de Esfuerzos

Los resultados arrojan un esfuerzo máximo de Von Mises de 40.96 kPa localizado en el perímetro interno de las perforaciones. Para la **justificación matemática** del comportamiento estructural, se debe comparar este valor con el Límite de Fluencia (*Yield Strength*) del material seleccionado. El ácido poliláctico (PLA) presenta un límite de fluencia típico de aproximadamente 30 MPa (o 30,000 kPa). 

Calculando el Factor de Seguridad (FS) de la pieza:
*   FS = Límite de Fluencia / Esfuerzo Máximo Obtenido
*   FS = 30,000 kPa / 40.96 kPa ≈ 732

Debido a que el esfuerzo máximo obtenido (40.96 kPa) es minúsculo frente a la capacidad del material y el FS es holgadamente superior a 1, la justificación matemática corrobora que, bajo una carga estática transversal de 5 N, la zona de las fijaciones operará completamente dentro de su zona elástica, sin presentar ningún nivel de riesgo estructural.



## Conclusión

La simulación permitió identificar que los bordes de los cuatro orificios cilíndricos son puntos efectivos de concentración de tensión, como respuesta a la resistencia que oponen al recibir directamente el vector de fuerza lateral (5 N) y la influencia de la gravedad, mientras el cuerpo de la pieza permanece inmovilizado por el soporte fijo.

Sin embargo, tras evaluar numéricamente la condición expuesta, los esfuerzos de Von Mises generados representan apenas un 0.13% del límite de fluencia del plástico PLA. Por lo tanto, el diseño demuestra poseer un comportamiento estructural sumamente robusto frente a las cargas evaluadas. La relación matemática obtenida garantiza que los anclajes no sufrirán desgarros ni deformaciones plásticas permanentes, asegurando la integridad del ensamblaje transversal.
