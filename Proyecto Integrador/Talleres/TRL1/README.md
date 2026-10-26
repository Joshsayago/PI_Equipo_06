# TRL 1: Estado del arte de la tecnología aplicada a CrackScan

## Aprendizaje autosupervisado y modelos de visión fundacionales para detectar grietas en concreto

**Equipo:** Equipo 06  
**Proyecto:** CrackScan  

---

## 1. Descripción de la tecnología

El aprendizaje autosupervisado (*self-supervised learning*) permite aprender representaciones visuales a partir de imágenes mediante tareas de entrenamiento construidas con los propios datos. En la detección de grietas, existen antecedentes que emplean este enfoque para reducir la dependencia de imágenes emparejadas y máscaras elaboradas manualmente [1].

Los modelos de visión fundacionales amplían esta posibilidad mediante el preentrenamiento con grandes colecciones de imágenes. Un ejemplo es DINOv2, que genera características visuales reutilizables en diferentes tareas, como clasificación y análisis a nivel de píxel [2].

Estas características pueden adaptarse al reconocimiento de grietas. Sin embargo, el preentrenamiento autosupervisado no significa que todas las etapas posteriores prescindan de etiquetas: la adaptación y evaluación de una aplicación concreta pueden requerir datos anotados.

Para CrackScan, esta tecnología se considera una alternativa de investigación para el análisis visual. Su selección definitiva dependerá de la calidad de los resultados, el costo computacional y la posibilidad de utilizarla en condiciones reales de inspección.

---

## 2. Relación con el proyecto CrackScan

CrackScan propone un sistema portátil de apoyo a la inspección preliminar de grietas en superficies de concreto de viviendas de Lima Metropolitana.

Los parámetros principales considerados por el proyecto son:

- **Ancho:** abertura transversal de la grieta.
- **Longitud:** extensión del recorrido de la grieta.
- **Orientación:** dirección predominante respecto de una referencia.
- **Patrón o tipo:** configuración visual de la grieta y sus ramificaciones.

El GPS, si se incorpora, se utilizará como **metadato de georreferenciación del registro**, separado de los parámetros geométricos.

### 2.1. Aporte esperado de la tecnología

El aprendizaje autosupervisado permitiría aprovechar fotografías sin anotaciones para aprender características útiles de las superficies. Posteriormente, el modelo podría adaptarse para identificar grietas o delimitar sus píxeles.

Es necesario distinguir dos resultados:

- **Clasificación:** determina si una imagen o una región contiene una grieta.
- **Segmentación:** identifica los píxeles correspondientes a la grieta.

La segmentación sería especialmente útil para desarrollar procedimientos posteriores de medición. No obstante, obtener dimensiones en milímetros requiere una referencia de escala o calibración; una máscara de píxeles por sí sola no proporciona medidas físicas.

### 2.2. Alcance de esta revisión

Esta revisión documenta los fundamentos y antecedentes de una tecnología candidata. No demuestra que CrackScan ya haya implementado o validado un sistema basado en DINOv2.

La identificación visual de una grieta tampoco determina, por sí sola, la seguridad estructural de una vivienda.

---

## 3. Estado del arte: artículos científicos

Los trabajos revisados presentan distintas estrategias para reducir la necesidad de anotaciones y mejorar el análisis visual de grietas. Incluyen aprendizaje de estructuras, modelos fundacionales, pseudoetiquetado, adaptación de dominio y segmentación autosupervisada.

| Ref. | Año | Trabajo | Aporte principal | Relación con CrackScan y limitaciones |
|---|---|---|---|---|
| [1] | 2020 | Zhang et al.: aprendizaje estructural con redes adversarias de consistencia cíclica. | Propone aprender la estructura de las grietas sin requerir pares de imágenes de entrada y salida ni las máscaras de referencia tradicionales. | Es un antecedente para reducir el trabajo de anotación. Su arquitectura es distinta de DINOv2 y debe evaluarse con imágenes representativas del proyecto. |
| [2] | 2023 | Oquab et al.: DINOv2. | Presenta características visuales generales obtenidas mediante preentrenamiento autosupervisado. | Ofrece una base reutilizable para adaptar modelos al análisis de grietas. El trabajo original no constituye una solución específica para viviendas de Lima ni un sistema de medición física. |
| [3] | 2024 | Sohaib et al.: SS-YOLO para grietas finas en concreto. | Combina YOLOv8, mecanismos de atención y pseudoetiquetado para detectar y segmentar grietas finas. | Aporta una alternativa especializada en concreto. Sus resultados no deben trasladarse directamente al proyecto sin validación local. |
| [4] | 2025 | Shim: adaptación de dominio con un modelo generativo de inpainting. | Ajusta Stable Diffusion mediante DreamBooth para generar imágenes y etiquetas adaptadas a un entorno objetivo. | Es relevante cuando cambian la textura, iluminación o apariencia de las superficies. Debe comprobarse que los datos sintéticos representen adecuadamente las imágenes reales. |
| [5] | 2026 | Zhu et al.: detección de grietas mediante DINOv2. | Estudia DINOv2 como extractor de características acompañado de una cabeza de clasificación lineal para reconocer grietas. | Conecta directamente los modelos fundacionales con la detección de grietas. La clasificación no equivale a una máscara de segmentación ni a una medición de ancho o longitud. |
| [6] | 2026 | Kyem et al.: Crack-Segmenter. | Presenta un transformador multiescala con fusión guiada por atención para segmentar grietas sin anotaciones manuales durante el entrenamiento propuesto. | Aporta una referencia para delimitar grietas a nivel de píxel. Se centra en pavimentos, por lo que su aplicación a paredes requiere evaluación y adaptación. |

### 3.1. Evolución de los enfoques

El trabajo de Zhang et al. muestra una alternativa temprana para aprender estructuras de grietas con menor dependencia de anotaciones convencionales [1]. DINOv2 amplía las posibilidades de reutilización al proporcionar representaciones visuales generales [2].

SS-YOLO desarrolla una estrategia especializada que combina atención y pseudoetiquetado para grietas finas [3]. Por su parte, Shim aborda el cambio de dominio mediante imágenes sintéticas adaptadas al lugar de inspección [4].

Los trabajos de Zhu et al. y Kyem et al. muestran dos direcciones complementarias: reutilizar características fundacionales para clasificación y desarrollar segmentación autosupervisada especializada, respectivamente [5], [6].

### 3.2. Análisis crítico

De la comparación se identifican las siguientes necesidades para CrackScan:

1. **Distinguir detección y medición.** Reconocer una grieta no implica conocer sus dimensiones físicas.
2. **Validar con imágenes locales.** Los resultados obtenidos en otros conjuntos de datos no garantizan el mismo desempeño en viviendas de Lima.
3. **Evaluar el cambio de dominio.** Las sombras, manchas, juntas, recubrimientos y variaciones de textura pueden afectar los resultados.
4. **Comprobar la viabilidad computacional.** Debe medirse el tiempo de procesamiento y el consumo de memoria en el equipo elegido.
5. **Mantener datos de referencia para evaluación.** Aunque el entrenamiento reduzca las anotaciones, comprobar la calidad de las predicciones requiere referencias confiables.

Estas necesidades constituyen una síntesis de la revisión y orientan las siguientes etapas del proyecto.

---

## 4. Patentes y solicitudes relacionadas

Se revisaron documentos relacionados con detección de defectos mediante imágenes, detección portátil de grietas en concreto e inspección visual activa.

Los documentos siguientes son antecedentes tecnológicos cercanos. No se presentan como patentes de la combinación específica “DINOv2 autosupervisado aplicado a CrackScan”.

| Ref. | Documento y fecha de publicación | Tipo de documento | Tecnología descrita | Relación y diferencia con CrackScan |
|---|---|---|---|---|
| [7] | **US12260538B2**, 25 de marzo de 2025. *Defect detection in image space*. | Patente concedida de Estados Unidos. | Describe procesamiento de imágenes y entrenamiento de redes para resaltar características de defectos, incluidas grietas, frente a información del fondo. | Se relaciona con la separación visual entre grieta y superficie. No corresponde específicamente a DINOv2 ni demuestra el sistema completo propuesto por CrackScan. |
| [8] | **CN118505597B**, 7 de noviembre de 2025. *Concrete member crack detection method based on deep learning algorithm*. | Patente concedida de China. | Describe un método de detección de grietas en elementos de concreto basado en aprendizaje profundo, con componentes orientados a su aplicación móvil. | Es un antecedente para detección portátil. Su enfoque no equivale a la propuesta de aprendizaje autosupervisado con modelos fundacionales. |
| [9] | **US20250378545A1**, 11 de diciembre de 2025. *Active damage detection system and method for detecting cracks in a surface*. | Publicación de solicitud de patente de Estados Unidos. | Describe inspección activa mediante un agente robótico y una cámara, utilizando observaciones desde diferentes puntos de vista. | Aporta un antecedente de captura visual adaptativa. Se diferencia del dispositivo portátil de mano considerado por CrackScan. |

### 4.1. Síntesis de los antecedentes patentados

Los documentos revisados muestran tres líneas de desarrollo:

- Procesamiento de imágenes para distinguir defectos del fondo [7].
- Detección de grietas mediante aprendizaje profundo en aplicaciones portátiles [8].
- Inspección activa con múltiples puntos de vista y plataformas robóticas [9].

Su revisión ayuda a reconocer soluciones existentes y comparar funciones. La existencia de estos documentos no demuestra por sí sola la novedad de CrackScan ni permite concluir que pueda utilizarse libremente cualquier implementación.

---

## 5. Brecha identificada y propuesta de investigación

La literatura revisada ofrece herramientas para reconocer o segmentar grietas con menor dependencia de anotaciones extensas. Sin embargo, no demuestra directamente el funcionamiento de un sistema portátil adaptado a las condiciones de captura previstas por CrackScan.

La brecha de aplicación identificada consiste en evaluar cómo integrar:

- Análisis visual de grietas en superficies representativas de las viviendas objetivo.
- Medición de ancho y longitud mediante una escala o calibración.
- Estimación de orientación respecto de una referencia definida.
- Descripción del patrón visual.
- Registro geográfico como metadato, si se incorpora GPS.
- Procesamiento compatible con los recursos del dispositivo seleccionado.

Esta brecha representa una oportunidad de adaptación y validación del proyecto; no constituye una afirmación de novedad mundial.

### 5.1. Pregunta de investigación propuesta

**¿En qué medida un enfoque de aprendizaje autosupervisado puede reducir la necesidad de anotaciones manuales manteniendo un desempeño adecuado para detectar o segmentar grietas en imágenes representativas del entorno de aplicación de CrackScan?**

### 5.2. Hipótesis de trabajo

Un modelo con preentrenamiento autosupervisado podría aprovechar características visuales reutilizables y reducir la cantidad de anotaciones necesarias para su adaptación.

Esta hipótesis deberá contrastarse con modelos de referencia y conjuntos de evaluación independientes.

---
### 5.3. Comparación de alternativas y selección preliminar

A partir de los antecedentes revisados, se comparan tres rutas tecnológicas para orientar las siguientes etapas de CrackScan. La valoración corresponde al análisis del equipo y deberá comprobarse experimentalmente.

| Alternativa | Ventaja para el proyecto | Principal limitación | Decisión preliminar |
|---|---|---|---|
| DINOv2 como extractor de características y clasificador. | Permite estudiar la reutilización de representaciones visuales para reconocer imágenes con grietas [2], [5]. | La clasificación no proporciona directamente el contorno necesario para medir la grieta. | Evaluarlo como alternativa para reconocimiento inicial. |
| Detector o segmentador especializado, como SS-YOLO. | Su enfoque está relacionado con grietas finas en concreto e incorpora mecanismos de atención y pseudoetiquetado [3]. | Requiere comprobar su desempeño y costo computacional en las condiciones del proyecto. | Considerarlo como candidato para detección y segmentación. |
| Segmentación autosupervisada, como Crack-Segmenter. | Propone delimitar grietas a nivel de píxel reduciendo la dependencia de anotaciones manuales durante su entrenamiento [6]. | Su aplicación original a pavimentos exige evaluar la transferencia a superficies de viviendas. | Explorar su adaptación si los recursos y datos disponibles lo permiten. |

**Selección preliminar:** Debido a que CrackScan busca obtener ancho, longitud, orientación y patrón visual, se priorizará investigar una ruta que produzca una máscara de segmentación. DINOv2 con una cabeza de clasificación se considerará una alternativa de reconocimiento, pero no se asumirá que resuelve por sí solo la medición geométrica.

Esta selección es provisional. La decisión final dependerá de los resultados de validación y de los recursos disponibles.

### 5.4. Plan propuesto de validación

Para comprobar la utilidad de la tecnología se propone evaluar tanto la calidad del análisis visual como la precisión de las mediciones posteriores.

| Componente | Procedimiento propuesto | Indicador |
|---|---|---|
| Reconocimiento de grietas. | Comparar las predicciones con imágenes clasificadas manualmente. | Precisión, sensibilidad y F1. |
| Segmentación. | Comparar las máscaras predichas con máscaras de referencia revisadas manualmente. | Intersección sobre unión (IoU) y Dice. |
| Ancho y longitud. | Comparar las medidas del sistema con mediciones de referencia, utilizando una escala visible o calibración. | Error absoluto medio en milímetros. |
| Orientación. | Comparar el ángulo estimado con una referencia definida sobre la misma superficie. | Error angular en grados. |
| Patrón visual. | Definir categorías y comparar las predicciones con un etiquetado de referencia. | Matriz de confusión y F1 por categoría. |
| Viabilidad portátil. | Ejecutar el modelo en el equipo seleccionado y registrar sus recursos. | Tiempo por imagen y memoria utilizada. |

#### Condiciones de evaluación

Las imágenes deberán incluir variaciones de iluminación, distancia, textura y abertura de grieta, además de superficies sin grietas que contengan manchas, sombras o juntas.

Para evitar resultados artificialmente favorables, las fotografías de una misma grieta o vivienda deberán permanecer en una sola partición: entrenamiento, validación o prueba. Así se reduce el riesgo de evaluar el modelo con imágenes demasiado parecidas a las utilizadas durante su desarrollo.

También se propone comparar los métodos usando el mismo conjunto de prueba y diferentes cantidades de datos anotados. Esto permitirá comprobar si el enfoque autosupervisado reduce realmente la necesidad de anotaciones frente al modelo de referencia.

Los valores mínimos aceptables de desempeño se definirán antes de la evaluación, considerando los requerimientos del proyecto. No se atribuirán a CrackScan las métricas publicadas por otros autores.

---
## 6. Posibles aplicaciones y evolución futura

Las líneas revisadas podrían aplicarse al análisis visual de grietas en edificios, puentes, túneles y pavimentos, considerando las diferencias entre cada entorno [1], [3]–[6].

Para CrackScan, las siguientes acciones se proponen como trabajo futuro:

1. **Construir un conjunto de imágenes representativo:** incluir superficies con y sin grietas y distintas condiciones de captura.
2. **Definir un modelo de referencia:** comparar una alternativa supervisada con un enfoque de preentrenamiento autosupervisado.
3. **Evaluar clasificación y segmentación por separado:** utilizar métricas apropiadas para cada tarea.
4. **Desarrollar la medición geométrica:** incorporar una referencia de escala y comparar las medidas con un método manual.
5. **Evaluar el despliegue portátil:** medir memoria, tiempo de inferencia y recursos requeridos.
6. **Integrar el registro de resultados:** asociar imágenes, características medidas y metadatos de ubicación, cuando corresponda.

Estas actividades son propuestas de desarrollo y no resultados ya obtenidos.

---
## 7. Conclusiones

1. El aprendizaje autosupervisado ofrece alternativas para reducir la dependencia de anotaciones manuales en el análisis de grietas. Los trabajos revisados utilizan estrategias diferentes y no deben considerarse equivalentes.

2. DINOv2 constituye una base de representación visual reutilizable, mientras que SS-YOLO y Crack-Segmenter presentan enfoques especializados en detección o segmentación de grietas.

3. Las patentes y solicitudes revisadas documentan antecedentes de procesamiento de imágenes, detección portátil e inspección robótica activa.

4. Para CrackScan, detectar o segmentar una grieta debe complementarse con calibración, procedimientos de medición y validación con imágenes del entorno objetivo.

5. Esta revisión proporciona una base documental para seleccionar y justificar una tecnología candidata. Su funcionamiento dentro de CrackScan deberá demostrarse mediante pruebas posteriores.

---

## 8. Referencias

[1] K. Zhang, Y. Zhang, and H. D. Cheng, “Self-supervised structure learning for crack detection based on cycle-consistent generative adversarial networks,” *Journal of Computing in Civil Engineering*, vol. 34, no. 3, Art. no. 04020004, 2020, doi: 10.1061/(ASCE)CP.1943-5487.0000883. [Online]. Available: https://doi.org/10.1061/(ASCE)CP.1943-5487.0000883

[2] M. Oquab et al., “DINOv2: Learning robust visual features without supervision,” arXiv preprint arXiv:2304.07193, 2023, doi: 10.48550/arXiv.2304.07193. [Online]. Available: https://arxiv.org/abs/2304.07193

[3] M. Sohaib, M. J. Hasan, M. A. Shah, and Z. Zheng, “A robust self-supervised approach for fine-grained crack detection in concrete structures,” *Scientific Reports*, vol. 14, no. 1, Art. no. 12646, 2024, doi: 10.1038/s41598-024-63575-x. [Online]. Available: https://doi.org/10.1038/s41598-024-63575-x

[4] S. Shim, “Self-supervised domain adaptive approach for extrapolated crack segmentation with fine-tuned inpainting generative model,” *Computer-Aided Civil and Infrastructure Engineering*, vol. 40, no. 21, pp. 3333–3358, 2025, doi: 10.1111/mice.13517. [Online]. Available: https://doi.org/10.1111/mice.13517

[5] T. Zhu et al., “Autonomous detection of concrete cracks using self-supervised DinoV2,” *Machine Intelligence Research*, vol. 23, no. 1, pp. 168–184, 2026, doi: 10.1007/s11633-025-1553-5. [Online]. Available: https://doi.org/10.1007/s11633-025-1553-5

[6] B. A. Kyem, J. K. Asamoah, E. Denteh, A. Danyo, and A. Aboah, “Self-supervised multi-scale transformer with Attention-Guided Fusion for efficient crack detection,” *Automation in Construction*, vol. 181, Art. no. 106591, 2026. [Online]. Available: https://www.sciencedirect.com/science/article/pii/S0926580525006314

[7] J. Cheng, Y. Sun, W. Xiong, W. Chen, Y. Li, and Y. Quan, “Defect detection in image space,” U.S. Patent 12,260,538 B2, Mar. 25, 2025. [Online]. Available: https://patents.google.com/patent/US12260538B2/en

[8] Tianjin Research Institute for Water Transport Engineering, MOT, assignee, “Concrete member crack detection method based on deep learning algorithm,” Chinese Patent CN118505597B, Nov. 7, 2025. [Online]. Available: https://patents.google.com/patent/CN118505597B/en

[9] M. R. Jahanshahi and W. Tang, “Active damage detection system and method for detecting cracks in a surface,” U.S. Patent Application Publication US20250378545A1, Dec. 11, 2025. [Online]. Available: https://patents.google.com/patent/US20250378545A1/en

<div align="center">

**CrackScan — Equipo 06**

</div>
