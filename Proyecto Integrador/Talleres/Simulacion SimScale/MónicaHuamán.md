https://www.simscale.com/workbench/?pid=8284097056428431416&rru=e442d6d6-7ada-4613-bd25-728ddf262d95&ci=87e7812c-239f-4a9a-83b0-3c45a5200b03&mt=SIMULATION_RESULT&ct=SOLUTION_FIELD Justificación
<img width="1777" height="837" alt="MónicaImagen" src="https://github.com/user-attachments/assets/7b723053-41df-443c-b288-24d381e5daf1" />

Justificación de la simulación estructural en SimScale

Para realizar la simulación estructural del case de la cámara en SimScale, se establecieron las condiciones de enlace o soporte necesarias para representar la sujeción del modelo y se definió la dirección de las cargas aplicadas.

El material seleccionado para la carcasa fue PLA (ácido poliláctico), debido a que es un material comúnmente utilizado en la fabricación de piezas mediante impresión 3D. Para la simulación se consideraron sus propiedades mecánicas, las cuales permiten evaluar la respuesta estructural del case frente a las cargas externas.

La fuerza gravitacional correspondiente al peso de la cámara se calculó mediante:

$$ F_g=m\cdot g $$

donde \(m\) es la masa de la cámara y \(g=9.81\ m/s^2\) es la aceleración de la gravedad.

Considerando una masa aproximada de \(0.51\ kg\):

$$ F_g=0.51(9.81)\approx5\ N $$

Por lo tanto, se aplicó una fuerza de aproximadamente 5 N en dirección vertical hacia abajo, representando el peso de la cámara sobre el case.

Además, se aplicaron tres fuerzas de compresión de referencia de 5 N en las partes superior, inferior y posterior de la carcasa. Estas cargas representan de manera aproximada la presión ejercida por la mano del usuario al sujetar la cámara y permiten evaluar el comportamiento estructural del case ante esfuerzos externos. Debido a que no se contó con un valor específico de fuerza de agarre, se utilizó 5 N como carga de referencia, equivalente aproximadamente al peso de la cámara.

Finalmente, se analizó la distribución de la tensión de Von Mises, la cual permite identificar las zonas donde se concentran los mayores esfuerzos mecánicos. De acuerdo con los resultados obtenidos, la mayor parte del case presenta tonalidades azules, lo que indica una menor concentración de esfuerzos, mientras que las zonas con colores de mayor intensidad representan regiones donde el esfuerzo es relativamente más elevado. Este análisis permite identificar posibles puntos críticos del diseño y evaluar si la carcasa de PLA presenta un comportamiento estructural adecuado frente a las cargas aplicadas.
