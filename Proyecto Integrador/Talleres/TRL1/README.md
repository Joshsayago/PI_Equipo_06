# Tecnología Emergente  

## Aprendizaje autosupervisado y modelos de visión fundacionales para detectar grietas en concreto

<div align="center">

**Equipo:** Equipo 06  
**Proyecto:** CrackScan  

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Computer Vision](https://img.shields.io/badge/Computer_Vision-000000?style=for-the-badge&logo=opencv&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)

</div>

---

# 1. Descripción breve de la tecnología

El **aprendizaje autosupervisado** (*self-supervised learning*) es una técnica de inteligencia artificial que permite que un modelo aprenda representaciones útiles a partir de datos sin que todas las imágenes tengan que ser etiquetadas manualmente. En visión por computadora, el modelo aprende patrones visuales —como texturas, bordes, formas y relaciones espaciales— mediante objetivos construidos a partir de las propias imágenes para luego adaptarlas a tareas específicas, como detectar o segmentar grietas.

Una línea reciente combina este enfoque con **modelos de visión fundacionales**. Un ejemplo destacado es DINOv2, preentrenado mediante aprendizaje autosupervisado para producir representaciones visuales reutilizables en diversas tareas. Investigaciones recientes han estudiado su aplicación, junto con otros métodos autosupervisados, orientados específicamente a la detección de grietas en estructuras de concreto.

La ventaja principal es reducir la dependencia de grandes conjuntos de imágenes anotadas manualmente. No obstante, el aprendizaje autosupervisado no garantiza por sí solo una precisión total, por lo que es indispensable validarlo con imágenes representativas del entorno real de aplicación[2].

---

# 2. Relación con el proyecto CrackScan

CrackScan propone un sistema portátil de apoyo a la inspección preliminar de grietas en viviendas de concreto de Lima Metropolitana. Su flujo previsto combina dos tipos de información:

1. **Información visual:** una cámara captura la superficie y un modelo de visión por computadora identifica la grieta y obtiene sus características.
2. **Contexto geográfico:** el GPS obtiene las coordenadas del punto de inspección para consultar el nivel de riesgo o daño sísmico correspondiente en la capa geográfica seleccionada.

La tecnología estudiada se relaciona con el primer componente: el aprendizaje autosupervisado sirve para entrenar o adaptar el modelo de visión encargado de detectar y segmentar las grietas, especialmente cuando se cuenta con muchas fotografías sin etiquetar y pocos ejemplos precisos. 

**Alcance y limitación:** Se trata de una tecnología candidata para investigación y no de una implementación definitiva. Los modelos fundacionales como DINOv2 suelen ser muy pesados para ejecutarse directamente en un microcontrolador de recursos limitados, por lo que CrackScan tendría que evaluar alternativas como el procesamiento en un dispositivo móvil, un ordenador de campo o la optimización de un modelo más ligero. Además, medir el ancho real de una grieta en milímetros requiere calibración o una escala de referencia; la segmentación de píxeles por sí sola no lo proporciona.

---

# 3. Estado del arte

La investigación ha evolucionado desde métodos autosupervisados tradicionales hasta enfoques recientes que reutilizan modelos visuales preentrenados y generan datos específicos del entorno.

| Ref. | Año y trabajo | Aporte principal | Relevancia para CrackScan y límites |
|---|---|---|---|
| [1] | Zhang et al., aprendizaje estructural con redes adversarias | Propone detectar grietas a nivel de píxel sin requerir pares de imágenes de entrada/salida ni máscaras de referencia tradicionales. | Antecedente temprano para reducir la dependencia de etiquetado manual; utiliza una arquitectura generativa específica. |
| [2] | Oquab et al., DINOv2 | Presenta un modelo visual preentrenado con aprendizaje autosupervisado para generar representaciones visuales reutilizables. | Base de los modelos fundacionales aplicables a imágenes de grietas, aunque no se centra específicamente en viviendas. |
| [3] | Sohaib et al., SS-YOLO | Combina YOLOv8, módulos de atención y pseudoetiquetado autosupervisado para grietas finas. | Relacionado directamente con concreto, aunque requiere validación con el tipo de viviendas de Lima. |
| [4] | Shim, adaptación de dominio con *inpainting* | Ajusta Stable Diffusion mediante DreamBooth para generar imágenes y etiquetas de grietas adaptadas al entorno objetivo. | Aborda el cambio de condiciones entre superficies, aunque requiere validación con fotos reales. |
| [5] | Zhu et al., DINOv2 para grietas | Evalúa DINOv2 como extractor de características visuales con un clasificador lineal para identificar grietas. | Antecedente próximo que conecta modelos fundacionales con grietas, sin medir ancho ni riesgo estructural por sí solo. |
| [6] | Kyem et al., Crack-Segmenter | Propone segmentación de grietas en pavimentos sin anotaciones manuales de píxeles mediante un transformador multiescala. | Muestra la evolución hacia la segmentación autosupervisada, centrado en pavimentos (requiere adaptación a paredes). |

## 3.1. Síntesis del estado del arte

Los trabajos demuestran que el aprendizaje autosupervisado reduce la necesidad de anotaciones manuales extensas. Mientras que DINOv2 ofrece representaciones generales adaptables, los métodos especializados incorporan atención y pseudoetiquetado. Sin embargo, persisten retos como los falsos positivos por sombras o texturas y la necesidad de referencias de escala para mediciones precisas.

---

# 4. Patentes y solicitudes relacionadas
 
Durante la búsqueda se identificó documentos de patente relacionados con la detección visual de grietas mediante redes neuronales y sistemas de inspección con cámara. **No se verificó una patente que coincida exactamente con la combinación específica “DINOv2 autosupervisado para detectar grietas en concreto”;** los siguientes documentos son antecedentes tecnológicos cercanos, no prueba de que esa combinación concreta esté patentada.

| Ref. | Documento | Tecnología descrita | Relación y diferencia con CrackScan |
|---|---|---|---|
| [7] | *Defect detection in image space*, patente de EE. UU. US 12,260,538 B2. | Describe transformar imágenes para suprimir información no relacionada con la grieta y entrenar una red neuronal para detectar defectos/grietas en imágenes. Google Patents la muestra como concedida y activa. | Es pertinente por el procesamiento de imágenes para separar las grietas del fondo. No es una patente de DINOv2 y no describe el flujo completo de CrackScan con GPS y mapa de riesgo sísmico. |
| [8] | *A concrete component crack detection method based on deep learning algorithm*, patente china CN 118505597 B | Describe detección de grietas en elementos de concreto mediante un algoritmo de aprendizaje profundo y su adaptación a una aplicación móvil, usando YOLOX y bibliotecas móviles. El registro indica que se concedió en noviembre de 2025. | Es relevante por la detección portátil de grietas en concreto. Su enfoque es la implementación móvil de un detector, no la integración autosupervisada de DINOv2 con el contexto geográfico de riesgo. |
| [9] | *Active damage detection system and method for detecting cracks in a surface*, solicitud de patente estadounidense US 2025/0378545 A1. | Propone un sistema robótico que cambia adaptativamente los puntos de vista de una cámara, distingue grietas de rayones y fusiona observaciones de distintas perspectivas. Google Patents la muestra como pendiente. | Muestra una línea de evolución hacia inspecciones visuales activas. A diferencia de CrackScan, describe una plataforma robótica con cámara móvil y no el sistema portátil de mano propuesto por el equipo. |

---

# 5. Posibles aplicaciones y evolución futura

- **Inspección de infraestructura:** Detección en edificios, puentes, túneles y pavimentos.
- **Optimización de costos:** Aprovechamiento de grandes volúmenes de imágenes sin etiquetar.
- **Adaptación a condiciones reales:** Mejora ante variaciones de iluminación y texturas.
- **Despliegue portátil:** Destilación y compresión de modelos para dispositivos de borde.
- **Integración geográfica:** Asociación de resultados visuales con coordenadas para la priorización post-sismo.

---

# 6. Conclusión

El aprendizaje autosupervisado y los modelos de visión fundacionales representan una vía prometedora para la detección de grietas con menor dependencia de etiquetas manuales. Para CrackScan, esta tecnología optimiza el módulo de captura y análisis visual, el cual debe complementarse de forma estructurada con la evaluación del contexto geográfico y de riesgo sísmico.

---

# 7. Referencias (formato IEEE)

[1] K. Zhang, Y. Zhang, and H. D. Cheng, “Self-supervised structure learning for crack detection based on cycle-consistent generative adversarial networks,” *Journal of Computing in Civil Engineering*, vol. 34, no. 3, 2020. 

[2] M. Oquab *et al*., “DINOv2: Learning robust visual features without supervision,” arXiv:2304.07193, 2023. 

[3] M. Sohaib, M. J. Hasan, M. A. Shah, and Z. Zheng, “A robust self-supervised approach for fine-grained crack detection in concrete structures,” *Scientific Reports*, vol. 14, no. 1, 2024. 

[4] S. Shim, “Self-supervised domain adaptive approach for extrapolated crack segmentation with fine-tuned inpainting generative model,” *Computer-Aided Civil and Infrastructure Engineering*, vol. 40, no. 21, 2025. 

[5] T. Zhu *et al*., “Autonomous detection of concrete cracks using self-supervised DinoV2,” *Machine Intelligence Research*, vol. 23, 2026. 

[6] B. A. Kyem *et al*., “Self-supervised multi-scale transformer with attention-guided fusion for efficient crack detection,” *Automation in Construction*, vol. 181, 2026. 

[7] J. Cheng *et al*., “Defect detection in image space,” U.S. Patent 12,260,538 B2, Mar. 25, 2025. 
[8] P. Zhu *et al*., “A concrete component crack detection method based on deep learning algorithm,” Chinese Patent CN 118505597 B, Nov. 7, 2025. 

[9] M. R. Jahanshahi and W. Tang, “Active damage detection system and method for detecting cracks in a surface,” U.S. Patent Application Publication US 2025/0378545 A1, Dec. 11, 2025. 

---

<div align="center">

**CrackScan — Equipo 06**

</div>
