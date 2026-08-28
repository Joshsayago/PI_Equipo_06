### Diego Murga - Simulación de fuerza de tracción en la correa

Para evaluar la resistencia estructural de la zona de sujeción de la cámara, se realizó una simulación aplicando una **fuerza de tracción de 5 N** sobre el asa destinada a la colocación de la correa.

La fuerza aplicada busca representar la carga generada cuando la cámara es sostenida o levantada mediante la correa. Considerando una masa estimada del dispositivo de aproximadamente **500 g**.

Se utilizó una fuerza de **5 N**, aproximando al peso estático estimado de la cámara.

La simulación permite observar una mayor concentración de esfuerzos en los **puntos de unión entre el asa y la carcasa**, debido a que estas zonas transmiten la carga hacia el cuerpo principal de la cámara.

<img width="1917" height="932" alt="image" src="https://github.com/user-attachments/assets/35c244b6-2220-4cb9-89d4-2d4df9047d7a" />

En la simulación, la fuerza de 5 N se aplica en la zona del asa. El resultado mostrado corresponde al esfuerzo de Von Mises, que permite identificar las zonas donde el material está siendo sometido a mayor esfuerzo.

La mayor concentración de esfuerzo aparece en los puntos donde el asa se une con la carcasa. Esto ocurre porque toda la carga aplicada sobre el asa debe transmitirse hacia el cuerpo de la cámara a través de esas dos uniones. Por esa razón, esas zonas aparecen en colores amarillo, naranja o rojo.

En este caso, el valor máximo observado es aproximadamente:

494.2 kPa

Este esfuerzo es relativamente bajo para una pieza fabricada en PLA, por lo que bajo una carga estática de 5 N el diseño no presenta, según esta simulación, un nivel de esfuerzo elevado.
