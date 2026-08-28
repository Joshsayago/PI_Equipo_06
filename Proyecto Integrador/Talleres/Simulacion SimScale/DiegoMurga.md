### Diego Murga — Simulación de fuerza de tracción en la correa

#### Descripción de la simulación

Para evaluar la **resistencia estructural de la zona de sujeción de la cámara**, se realizó una simulación aplicando una **fuerza de tracción de 5 N** sobre el asa destinada a la colocación de la correa.

La fuerza aplicada busca representar la carga generada cuando la cámara es sostenida o levantada mediante la correa. Para este análisis se consideró una masa total aproximada del dispositivo de **500 g**, teniendo en cuenta la carcasa y los componentes electrónicos internos.

El peso correspondiente a una masa de 500 g es aproximadamente **5 N**.
---

#### Resultado de la simulación

<p align="center">
  <img width="900" alt="Simulación de esfuerzo de Von Mises en el asa de la cámara" src="https://github.com/user-attachments/assets/35c244b6-2220-4cb9-89d4-2d4df9047d7a" />
</p>

**Simulación en SimScale:** https://www.simscale.com/workbench/?pid=8335400421832898015&rru=a48ad42f-f713-4bec-97ab-c73046a64167&ci=b787de89-14db-4dd8-a887-60ba47d987b0&mt=SIMULATION_RESULT&ct=SOLUTION_FIELD

La simulación muestra la distribución del **esfuerzo de Von Mises** generado por la aplicación de la carga de **5 N** sobre el asa de la cámara.

Se observa que la mayor concentración de esfuerzos se encuentra en los **puntos de unión entre el asa y la carcasa**. Esto ocurre debido a que la carga aplicada sobre el asa debe transmitirse hacia el cuerpo principal de la cámara a través de estas dos zonas.

Por esta razón, los puntos de unión presentan colores **amarillo, naranja y rojo**, indicando las regiones donde se alcanzan los mayores esfuerzos dentro del modelo. El color rojo representa el **máximo esfuerzo obtenido en la simulación** y no implica necesariamente una falla del material.

---

#### Esfuerzo máximo obtenido

El valor máximo de esfuerzo de Von Mises observado en la simulación fue de aproximadamente:

> **494.2 kPa**

Este valor representa el esfuerzo máximo localizado principalmente en las uniones del asa con la carcasa.

Debido a que el esfuerzo obtenido es relativamente bajo para una pieza fabricada en **PLA**, el análisis indica que, bajo una carga estática de **5 N**, la zona evaluada no presenta un nivel de esfuerzo elevado.

---

#### Conclusión

La simulación permitió identificar que los **puntos de unión del asa con la carcasa son las zonas más críticas del diseño**, debido a la concentración de esfuerzos producida por la transferencia de la carga.

Sin embargo, para la condición evaluada de **5 N**, equivalente aproximadamente al peso estimado de una cámara de **500 g**, los esfuerzos obtenidos permanecen en niveles bajos. Por lo tanto, el diseño presenta un comportamiento estructural adecuado frente a la carga estática considerada.

como hago que es link se abra en otra pestania
