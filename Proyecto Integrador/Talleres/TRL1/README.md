 
# CRACKSCAN

### Principios básicos reportados de la tecnología propuesta · TRL 1

<div align="center">

**Equipo:** Equipo 06  
**Proyecto:** CrackScan  

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Computer Vision](https://img.shields.io/badge/Computer_Vision-000000?style=for-the-badge&logo=opencv&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)

</div>

## Ficha del proyecto

| Campo | Información |
|---|---|
| Proyecto | CrackScan — Sistema inteligente portátil para apoyo a la inspección de grietas en viviendas de Lima Metropolitana |
| Tecnología emergente | Aprendizaje autosupervisado y modelos de visión fundacionales aplicados al análisis visual de grietas en concreto |
| Institución | Universidad Peruana Cayetano Heredia |
| Curso | Proyecto Integrador |
| Equipo | Equipo 06 |
| Nivel documentado | TRL 1 — Principios básicos reportados de la tecnología propuesta |
| Alcance | Revisión bibliográfica, identificación de antecedentes tecnológicos y fundamento científico, sin validación experimental del sistema |

## Contenido

1. [Presentación del proyecto](#presentación-del-proyecto)
2. [Artículos científicos y principios tecnológicos](#1-artículos-científicos-y-principios-tecnológicos)
3. [Estado del arte](#2-estado-del-arte)
4. [Patentes y solicitudes relacionadas](#3-patentes-y-solicitudes-relacionadas)
5. [Bases de datos y fuentes de información científica](#4-bases-de-datos-y-fuentes-de-información-científica)
6. [Brecha identificada y propuesta de investigación](#5-brecha-identificada-y-propuesta-de-investigación)
7. [Posibles aplicaciones y evolución tecnológica](#6-posibles-aplicaciones-y-evolución-tecnológica)
8. [Conclusiones](#7-conclusiones)
9. [Referencias bibliográficas](#referencias-bibliográficas)

---

## Presentación del proyecto

CrackScan es un proyecto orientado al desarrollo de un sistema inteligente portátil para apoyar la inspección preliminar de grietas en superficies de concreto de viviendas de Lima Metropolitana. La propuesta considera el análisis de fotografías digitales mediante técnicas de visión por computadora e inteligencia artificial, con el propósito de identificar y caracterizar visualmente las grietas presentes en dichas superficies.

La tecnología emergente considerada corresponde al **aprendizaje autosupervisado (*self-supervised learning*) y los modelos de visión fundacionales (*foundation vision models*)**. Estos enfoques permiten obtener representaciones visuales a partir de grandes colecciones de imágenes y aprovecharlas posteriormente en tareas específicas de reconocimiento y análisis de imágenes.

Un modelo representativo de esta tecnología es **DINOv2**, desarrollado mediante aprendizaje autosupervisado. Sus representaciones visuales pueden reutilizarse y adaptarse a diferentes tareas de visión por computadora, entre ellas clasificación y análisis a nivel de píxel. Esto permite estudiar su posible aplicación en la identificación y segmentación de grietas en superficies de concreto.

En CrackScan, el análisis visual considera características como el ancho aproximado, la longitud, la orientación y el patrón de las grietas. Para obtener dimensiones físicas, como el ancho expresado en milímetros, será necesario incorporar una referencia de escala o un procedimiento de calibración. Asimismo, se contempla el registro de información geográfica mediante GPS como metadato asociado a la inspección.

De manera complementaria, la propuesta considera información geográfica relacionada con el contexto de riesgo o daño sísmico de la zona, procedente de fuentes como SIGRID/CENEPRED. Esta información permitiría contextualizar el registro de la inspección, sin establecer una relación causal directa entre el valor cartográfico y las características individuales de una grieta.

En esta etapa TRL 1 se documentan los principios científicos y antecedentes tecnológicos que sustentan la propuesta. **No se afirma que el modelo de inteligencia artificial haya sido entrenado, que la segmentación de grietas haya sido validada o que el sistema determine la seguridad estructural de una vivienda.**

**Pregunta de investigación:** ¿Cómo pueden el aprendizaje autosupervisado y los modelos de visión fundacionales contribuir a la identificación y segmentación de grietas en superficies de concreto, reduciendo la dependencia de anotaciones manuales y permitiendo obtener características visuales útiles para apoyar una inspección preliminar?

### Enfoque metodológico de CONCYTEC

La metodología de niveles de madurez tecnológica (TRL) permite identificar el grado de desarrollo de una tecnología mediante evidencias correspondientes a diferentes etapas de investigación y desarrollo.

En el nivel **TRL 1 — Principios básicos reportados de la nueva tecnología propuesta**, se identifican y documentan los fundamentos científicos que podrían sustentar una aplicación tecnológica. Entre las evidencias consideradas para esta etapa se encuentran los artículos científicos, el estado del arte, las bases de datos, los libros y las tesis relacionadas con la tecnología estudiada.

Por ello, el presente documento se concentra en revisar investigaciones sobre aprendizaje autosupervisado, modelos de visión fundacionales y métodos de detección y segmentación de grietas. También se identifican antecedentes de propiedad industrial y posibles aplicaciones de estos enfoques en el proyecto CrackScan.

**Alcance de la revisión:** el análisis se limita a los fundamentos y antecedentes publicados. La selección definitiva de una arquitectura, la adaptación de modelos, la construcción de conjuntos de imágenes y la evaluación de su desempeño corresponden a etapas posteriores del desarrollo tecnológico.

---

## 1. Artículos científicos y principios tecnológicos

### 1.1. Aprendizaje autosupervisado (*Self-Supervised Learning*)

El aprendizaje autosupervisado es un enfoque de aprendizaje automático que permite entrenar modelos utilizando información generada a partir de los propios datos, sin requerir necesariamente etiquetas manuales para todas las imágenes durante el preentrenamiento.

A diferencia del aprendizaje supervisado convencional, donde el modelo aprende a partir de ejemplos previamente etiquetados, el aprendizaje autosupervisado plantea tareas de entrenamiento que permiten identificar patrones y relaciones dentro de los datos disponibles.

En el análisis de grietas, este enfoque resulta de interés porque la elaboración manual de anotaciones puede requerir tiempo y trabajo especializado. Por ejemplo, delimitar los píxeles correspondientes a una grieta en una fotografía constituye una tarea de anotación que puede ser laboriosa, especialmente cuando se trabaja con numerosas imágenes.

Zhang y colaboradores (2020) estudiaron un enfoque de aprendizaje estructural basado en redes generativas adversarias y consistencia cíclica para la detección de grietas. Su propuesta permite aprender estructuras visuales sin depender de los pares de imágenes y máscaras de referencia utilizados habitualmente en métodos supervisados [1].

Este antecedente demuestra que existen estrategias de aprendizaje que pueden reducir la dependencia de anotaciones convencionales. Sin embargo, el aprendizaje autosupervisado no significa que todas las etapas posteriores puedan prescindir de datos etiquetados, ya que la adaptación y evaluación de una aplicación específica pueden requerir anotaciones de referencia.

En CrackScan, este principio podría aprovecharse para estudiar representaciones visuales de superficies de concreto y facilitar la adaptación de modelos a tareas de reconocimiento o segmentación de grietas.

### 1.2. Modelos de visión fundacionales (*Foundation Vision Models*)

Los modelos de visión fundacionales son modelos entrenados previamente con grandes colecciones de imágenes, con el objetivo de aprender características visuales generales que puedan reutilizarse en diferentes aplicaciones.

En lugar de desarrollar un modelo desde cero para cada problema, estas representaciones pueden servir como punto de partida para tareas específicas mediante procedimientos de adaptación o ajuste.

Un ejemplo representativo es **DINOv2**, presentado por Oquab y colaboradores (2023). Este modelo utiliza aprendizaje autosupervisado para obtener representaciones visuales que pueden transferirse a diferentes tareas de visión por computadora [2].

Las características extraídas por DINOv2 pueden utilizarse como información de entrada para otros componentes del sistema, como clasificadores o módulos de segmentación. De esta manera, el modelo puede funcionar como extractor de características visuales sin que necesariamente sea, por sí solo, un detector especializado de grietas.

En CrackScan, DINOv2 se considera una alternativa tecnológica para investigar la identificación de patrones visuales asociados a grietas en superficies de concreto.

Es importante diferenciar las funciones que pueden desarrollarse a partir de estas representaciones:

- **Clasificación:** permite determinar si una imagen o región contiene una grieta.
- **Detección:** permite identificar la presencia de grietas y localizar regiones aproximadas dentro de una imagen.
- **Segmentación:** permite delimitar los píxeles que corresponden a una grieta, proporcionando información espacial más detallada.

La segmentación es especialmente relevante para CrackScan, debido a que podría servir como base para procedimientos posteriores de medición geométrica. Sin embargo, una máscara de píxeles no proporciona directamente dimensiones físicas: para estimar el ancho o la longitud en milímetros se requiere una referencia de escala o calibración.

### 1.3. Detección y segmentación de grietas mediante inteligencia artificial

La detección de grietas en concreto constituye una aplicación de la visión por computadora que busca reconocer discontinuidades visibles en superficies estructurales.

Las fotografías pueden presentar diferentes condiciones que dificultan el reconocimiento, como variaciones de iluminación, sombras, manchas, juntas, texturas irregulares, superficies rugosas y obstrucciones.

Sohaib y colaboradores (2024) presentaron SS-YOLO, un enfoque orientado a la detección de grietas finas en concreto que incorpora mecanismos de atención y pseudoetiquetado [3].

El pseudoetiquetado consiste en utilizar predicciones generadas por un modelo para construir etiquetas provisionales que posteriormente pueden incorporarse a procesos de entrenamiento. Su utilidad depende de la calidad de dichas predicciones, debido a que los errores pueden propagarse durante el aprendizaje.

Por otro lado, Kyem y colaboradores (2026) presentaron Crack-Segmenter, un enfoque basado en un transformador multiescala y mecanismos de fusión guiados por atención para la segmentación de grietas [6].

Estos antecedentes permiten reconocer que existen diferentes estrategias para abordar el análisis de grietas mediante inteligencia artificial. No obstante, los resultados obtenidos en conjuntos de datos y superficies específicas no garantizan el mismo desempeño en fotografías de viviendas de Lima Metropolitana.

Para CrackScan, la identificación de grietas deberá considerar tanto la capacidad de reconocimiento como la delimitación de sus regiones, debido a que esta última puede proporcionar información necesaria para caracterizar sus dimensiones y geometría.

### 1.4. Adaptación de dominio y variabilidad de las imágenes

La adaptación de dominio es un enfoque que busca mejorar la transferencia de modelos cuando las características de los datos de aplicación difieren de aquellas presentes en los datos utilizados durante el entrenamiento.

En el análisis de grietas, las diferencias pueden presentarse por cambios en la iluminación, distancia de captura, textura del concreto, resolución de las fotografías, condiciones ambientales o características de las superficies inspeccionadas.

Shim (2025) estudió un enfoque de adaptación de dominio para la segmentación de grietas mediante un modelo generativo de *inpainting* ajustado con DreamBooth [4].

El estudio resulta relevante porque aborda la dificultad de trasladar modelos entre diferentes entornos visuales. La generación de imágenes sintéticas puede contribuir a ampliar los datos disponibles, aunque es necesario comprobar que estas imágenes representen adecuadamente las condiciones reales de aplicación.

En CrackScan, este principio resulta importante debido a que las fotografías podrían obtenerse en viviendas con superficies de concreto de diferentes características. Por ello, un modelo entrenado con imágenes de otros entornos deberá evaluarse antes de utilizarse en las condiciones previstas por el proyecto.

### 1.5. Caracterización geométrica de grietas mediante procesamiento de imágenes

La identificación de una grieta no constituye por sí sola una medición de sus dimensiones. Para obtener características geométricas es necesario procesar la región identificada y establecer una relación entre los píxeles de la imagen y las dimensiones reales de la superficie.

Entre los parámetros visuales considerados por CrackScan se encuentran:

- **Ancho:** abertura transversal de la grieta.
- **Longitud:** extensión del recorrido de la grieta.
- **Orientación:** dirección predominante respecto de una referencia definida.
- **Patrón o tipo:** configuración visual de la grieta y sus ramificaciones.

El procesamiento de imágenes puede utilizarse para analizar contornos, regiones, distancias y orientaciones. Sin embargo, las dimensiones expresadas en píxeles no equivalen automáticamente a milímetros o centímetros.

Para realizar mediciones físicas se necesita incorporar una referencia de escala, conocer las condiciones de captura o aplicar procedimientos de calibración. Sreedhara y colaboradores (2023) estudiaron la aplicación del procesamiento digital de imágenes para medir anchos de grietas de concreto en estudios de campo [13].

En consecuencia, la segmentación constituye una etapa previa para el análisis geométrico, mientras que la calibración permite relacionar las mediciones digitales con dimensiones físicas.

### 1.6. Registro geográfico y contextualización de la inspección

La georreferenciación permite asociar información espacial a los registros obtenidos durante una inspección. En CrackScan, el GPS se contempla como un medio para registrar las coordenadas geográficas correspondientes al lugar donde se captura la fotografía.

Estas coordenadas pueden utilizarse como metadatos para organizar los registros y consultar información geográfica relacionada con el contexto de la zona.

El proyecto considera la posible incorporación de información cartográfica de SIGRID/CENEPRED relacionada con el nivel de riesgo o daño sísmico de la zona.

Esta información tendría una función complementaria: permitiría contextualizar la caracterización visual de una grieta con información geográfica disponible para el área de inspección.

Es importante precisar que el valor cartográfico de una zona no representa una medición directa de la grieta ni determina por sí mismo la condición estructural de una vivienda. La información visual y geográfica corresponde a fuentes diferentes y deberá interpretarse de manera complementaria.

La integración de estos datos constituye una característica de aplicación del proyecto, mientras que la tecnología emergente central de esta revisión corresponde al aprendizaje autosupervisado y los modelos de visión fundacionales.

---

## 2. Estado del arte

La investigación sobre detección y segmentación de grietas mediante inteligencia artificial ha evolucionado desde métodos de procesamiento de imágenes y aprendizaje supervisado hacia enfoques que buscan aprovechar datos sin anotaciones manuales, representaciones visuales preentrenadas y técnicas de adaptación de dominio.

Los trabajos revisados presentan diferentes estrategias para identificar discontinuidades en superficies de concreto y mejorar la capacidad de generalización de los modelos.

### 2.1. Investigaciones relacionadas

| Referencia | Año | Investigación | Aporte principal | Relación con CrackScan y limitaciones |
|---|---:|---|---|---|
| Zhang et al. [1] | 2020 | Aprendizaje estructural mediante redes generativas adversarias y consistencia cíclica. | Propone aprender estructuras de grietas sin requerir pares convencionales de imágenes y máscaras de referencia. | Constituye un antecedente de aprendizaje con menor dependencia de anotaciones manuales. Su arquitectura es diferente de DINOv2. |
| Oquab et al. [2] | 2023 | DINOv2: aprendizaje de características visuales robustas sin supervisión. | Presenta representaciones visuales generales obtenidas mediante preentrenamiento autosupervisado. | Proporciona una base reutilizable para adaptar modelos al análisis de grietas. No es un detector especializado de grietas. |
| Sohaib et al. [3] | 2024 | SS-YOLO para detección de grietas finas en concreto. | Combina mecanismos de atención y pseudoetiquetado para el análisis de grietas. | Presenta una aplicación especializada en concreto. Sus resultados requieren validación en imágenes del entorno de CrackScan. |
| Shim [4] | 2025 | Adaptación de dominio para segmentación de grietas mediante un modelo generativo. | Estudia la generación y adaptación de imágenes para mejorar la transferencia entre dominios. | Es relevante ante diferencias de textura, iluminación y condiciones de captura. |
| Zhu et al. [5] | 2026 | Detección de grietas mediante DINOv2. | Estudia el uso de DINOv2 como extractor de características visuales acompañado de una cabeza de clasificación lineal. | Vincula los modelos fundacionales con la detección de grietas. La clasificación no equivale a segmentación ni a medición física. |
| Kyem et al. [6] | 2026 | Crack-Segmenter: transformador multiescala con fusión guiada por atención. | Presenta un enfoque para segmentar grietas con menor dependencia de anotaciones manuales durante el entrenamiento. | Es un antecedente de segmentación a nivel de píxel. Su aplicación a superficies de viviendas requiere evaluación. |

### 2.2. Evolución de los enfoques tecnológicos

Los trabajos revisados muestran diferentes aproximaciones al análisis automatizado de grietas.

En primer lugar, Zhang y colaboradores (2020) estudiaron el aprendizaje de estructuras visuales mediante redes generativas adversarias y consistencia cíclica, planteando una alternativa para reducir la dependencia de anotaciones convencionales [1].

Posteriormente, Oquab y colaboradores (2023) presentaron DINOv2, que amplía las posibilidades de reutilización de representaciones visuales mediante preentrenamiento autosupervisado [2].

En 2024, Sohaib y colaboradores desarrollaron SS-YOLO, una estrategia especializada en grietas finas de concreto que incorpora mecanismos de atención y pseudoetiquetado [3].

Por su parte, Shim (2025) abordó el problema de adaptación de dominio mediante modelos generativos, considerando las diferencias entre los entornos de entrenamiento y aplicación [4].

Finalmente, los trabajos de Zhu y colaboradores (2026) y Kyem y colaboradores (2026) muestran dos líneas complementarias: el aprovechamiento de características fundacionales para la detección y el desarrollo de arquitecturas especializadas para segmentación [5], [6].

### 2.3. Análisis crítico del estado del arte

A partir de la comparación de las investigaciones se identifican las siguientes consideraciones para CrackScan:

1. **Diferenciar las tareas de visión por computadora.** La clasificación, detección y segmentación producen resultados diferentes. Para caracterizar geométricamente una grieta, la segmentación puede proporcionar información espacial más detallada.

2. **Considerar la variabilidad de las superficies.** Las sombras, manchas, juntas, texturas y obstrucciones pueden dificultar la identificación de grietas.

3. **Validar con imágenes representativas.** Los resultados publicados en otros conjuntos de datos no garantizan el mismo desempeño en viviendas de Lima Metropolitana.

4. **Evaluar la necesidad de anotaciones.** El aprendizaje autosupervisado puede reducir la dependencia de etiquetas durante el preentrenamiento, pero la evaluación de resultados requiere referencias confiables.

5. **Considerar las limitaciones de medición.** Una máscara de segmentación no proporciona directamente dimensiones físicas. Para medir ancho y longitud se necesita escala o calibración.

6. **Evaluar la viabilidad computacional.** Los modelos de visión fundacionales pueden requerir recursos de procesamiento y memoria que deben considerarse al definir su implementación en un sistema portátil.

Estas consideraciones permiten identificar los principales aspectos que deberán estudiarse en las siguientes etapas de desarrollo.

### 2.4. Síntesis del estado del arte

Las investigaciones revisadas muestran que el aprendizaje autosupervisado y los modelos de visión fundacionales constituyen alternativas relevantes para desarrollar sistemas de análisis visual con menor dependencia de anotaciones manuales.

Asimismo, los antecedentes especializados en grietas demuestran la existencia de métodos de detección y segmentación aplicados a superficies de concreto.

Sin embargo, no se ha demostrado mediante los trabajos revisados que una combinación específica de estas tecnologías pueda caracterizar de manera confiable las grietas presentes en viviendas de Lima Metropolitana bajo las condiciones previstas por CrackScan.

Por ello, la adaptación de los modelos, la construcción de datos representativos y la validación experimental constituyen actividades necesarias para determinar su utilidad en el proyecto.

---

## 3. Patentes y solicitudes relacionadas

La revisión de documentos de propiedad industrial permite identificar antecedentes tecnológicos relacionados con el procesamiento de imágenes, la detección automatizada de defectos y la inspección de superficies.

Los documentos identificados constituyen referencias de tecnologías cercanas al campo de aplicación de CrackScan. No corresponden necesariamente a la combinación específica de aprendizaje autosupervisado, modelos fundacionales y registro geográfico planteada por el proyecto.

| Referencia | Documento y fecha | Tipo de documento | Tecnología descrita | Relación con CrackScan |
|---|---|---|---|---|
| [7] | US12260538B2, 25 de marzo de 2025. *Defect detection in image space*. | Patente concedida de Estados Unidos. | Describe el procesamiento de imágenes y el entrenamiento de redes para resaltar características de defectos, incluidas grietas. | Se relaciona con la identificación visual de defectos y la diferenciación entre grietas y fondo. |
| [8] | CN118505597B, 7 de noviembre de 2025. *Concrete member crack detection method based on deep learning algorithm*. | Patente concedida de China. | Describe un método de detección de grietas en elementos de concreto mediante aprendizaje profundo. | Constituye un antecedente de detección automatizada de grietas en concreto. |
| [9] | US20250378545A1, 11 de diciembre de 2025. *Active damage detection system and method for detecting cracks in a surface*. | Solicitud de patente publicada en Estados Unidos. | Describe un sistema de inspección activa mediante una plataforma robótica y una cámara. | Se relaciona con la captura y el análisis visual de superficies, aunque utiliza una configuración diferente a la de un dispositivo portátil. |

### 3.1. Análisis de los antecedentes patentados

Los documentos revisados permiten identificar tres líneas de desarrollo tecnológico:

- **Procesamiento de imágenes:** utilización de algoritmos para distinguir defectos y grietas de las características del fondo [7].
- **Detección automatizada en concreto:** aplicación de técnicas de aprendizaje profundo para reconocer grietas en elementos de concreto [8].
- **Inspección visual activa:** utilización de cámaras y plataformas de inspección para obtener información desde diferentes puntos de vista [9].

Estos antecedentes permiten reconocer tecnologías existentes y establecer diferencias con la propuesta de CrackScan.

La revisión de patentes no constituye por sí sola un análisis de patentabilidad ni una evaluación de libertad de operación. Para determinar la novedad de una solución específica sería necesario realizar una búsqueda de anterioridad más amplia y un análisis especializado de las reivindicaciones correspondientes.

---

## 4. Bases de datos y fuentes de información científica

La revisión bibliográfica considera fuentes académicas, repositorios de publicaciones científicas y documentos de propiedad industrial que permiten identificar investigaciones relacionadas con la tecnología propuesta.

| Fuente | Tipo de información | Utilidad para CrackScan |
|---|---|---|
| ScienceDirect (Elsevier) | Artículos científicos y publicaciones académicas. | Consulta de investigaciones sobre detección y segmentación de grietas. |
| Springer Nature | Artículos científicos y libros especializados. | Revisión de modelos de visión por computadora y aprendizaje automático. |
| Scientific Reports | Investigaciones científicas multidisciplinarias. | Identificación de antecedentes sobre aprendizaje autosupervisado y análisis de grietas. |
| IEEE Xplore | Publicaciones de ingeniería, electrónica y computación. | Consulta de investigaciones sobre procesamiento digital de imágenes e inteligencia artificial. |
| Scopus | Base de datos de referencias y citas académicas. | Identificación de publicaciones relacionadas y seguimiento de antecedentes científicos. |
| Web of Science | Índice de publicaciones científicas. | Consulta de investigaciones y análisis de producción científica. |
| Google Académico | Buscador de literatura académica. | Localización de artículos, tesis y documentos científicos. |
| Google Patents | Documentos de propiedad industrial. | Identificación de patentes y solicitudes relacionadas con detección de defectos. |

### 4.1. Términos de búsqueda relacionados

Para identificar investigaciones relacionadas con la tecnología propuesta se consideran los siguientes términos:

| Área de investigación | Términos de búsqueda |
|---|---|
| Aprendizaje autosupervisado | `self-supervised learning`, `unsupervised visual representation learning`. |
| Modelos fundacionales | `foundation vision models`, `DINOv2`, `visual feature extraction`. |
| Detección de grietas | `concrete crack detection`, `deep learning crack detection`. |
| Segmentación | `concrete crack segmentation`, `pixel-level crack segmentation`. |
| Adaptación de dominio | `domain adaptation crack detection`, `synthetic data crack segmentation`. |
| Medición geométrica | `concrete crack width measurement`, `crack image processing`. |
| Aplicación portátil | `portable concrete crack inspection`, `mobile crack detection system`. |

### 4.2. Criterios de selección de información

Para la selección de las investigaciones se consideran los siguientes criterios:

- Identificación de autores, año y fuente de publicación.
- Relación directa con el aprendizaje autosupervisado, los modelos fundacionales o la detección de grietas.
- Descripción de los métodos empleados y de sus principales aportes.
- Identificación de las limitaciones de aplicación.
- Posibilidad de consultar el documento original o su registro bibliográfico.

Es importante diferenciar los artículos científicos de las fichas técnicas y los documentos de patentes, debido a que cada fuente proporciona un tipo de evidencia diferente.

---

## 5. Brecha identificada y propuesta de investigación

La revisión de investigaciones permite reconocer que existen diferentes métodos para identificar y segmentar grietas en superficies de concreto mediante inteligencia artificial.

Asimismo, los modelos de visión fundacionales ofrecen representaciones visuales que pueden reutilizarse en tareas específicas, mientras que el aprendizaje autosupervisado permite explorar alternativas para reducir la dependencia de anotaciones manuales durante el preentrenamiento.

Sin embargo, los antecedentes revisados no demuestran directamente el funcionamiento de un sistema portátil que integre el análisis visual de grietas, su caracterización geométrica y el registro de información geográfica en las condiciones de aplicación previstas por CrackScan.

### 5.1. Brecha tecnológica identificada

La brecha de aplicación identificada consiste en estudiar la adaptación de modelos de visión por computadora para analizar grietas en superficies de concreto de viviendas de Lima Metropolitana, considerando las variaciones de textura, iluminación y condiciones de captura.

Además, se requiere investigar cómo complementar la identificación visual con procedimientos de medición geométrica y registro geográfico.

Para abordar esta brecha se consideran los siguientes elementos:

- Identificación visual de grietas en fotografías de superficies de concreto.
- Segmentación de las regiones correspondientes a las grietas.
- Caracterización de ancho, longitud, orientación y patrón visual.
- Incorporación de una referencia de escala o procedimiento de calibración para estimar dimensiones físicas.
- Registro de coordenadas geográficas mediante GPS, cuando corresponda.
- Asociación de información cartográfica relacionada con el contexto de riesgo o daño sísmico de la zona.

Esta brecha representa una oportunidad de investigación y adaptación tecnológica. No constituye una afirmación de novedad mundial ni demuestra que la solución propuesta sea la única existente.

### 5.2. Pregunta de investigación

**¿En qué medida un enfoque de aprendizaje autosupervisado y modelos de visión fundacionales puede contribuir a la identificación y segmentación de grietas en superficies de concreto, reduciendo la necesidad de anotaciones manuales y permitiendo obtener características visuales útiles para apoyar una inspección preliminar?**

### 5.3. Hipótesis de trabajo

El uso de representaciones visuales obtenidas mediante modelos de visión fundacionales preentrenados con aprendizaje autosupervisado podría facilitar la adaptación de modelos de inteligencia artificial para identificar y segmentar grietas en fotografías de superficies de concreto, reduciendo la dependencia de grandes cantidades de imágenes anotadas durante el preentrenamiento.

Esta hipótesis deberá contrastarse mediante pruebas posteriores, comparando los resultados obtenidos con modelos de referencia y conjuntos de imágenes representativos del entorno de aplicación.

### 5.4. Comparación preliminar de alternativas tecnológicas

A partir de los antecedentes revisados se identifican tres alternativas que pueden orientar el desarrollo posterior de CrackScan.

| Alternativa | Ventaja potencial | Limitación principal | Aplicación considerada |
|---|---|---|---|
| DINOv2 como extractor de características y clasificador. | Permite aprovechar representaciones visuales preentrenadas para reconocer imágenes con grietas. | La clasificación no proporciona directamente una máscara para medir la geometría de la grieta. | Reconocimiento inicial de imágenes o regiones con grietas. |
| Modelos especializados como SS-YOLO. | Presentan mecanismos orientados a la detección de grietas finas en concreto. | Su desempeño debe evaluarse con fotografías representativas del proyecto. | Detección de grietas y localización de regiones. |
| Modelos de segmentación como Crack-Segmenter. | Permiten estudiar la delimitación de grietas a nivel de píxel. | Su aplicación a superficies de viviendas requiere adaptación y evaluación. | Obtención de máscaras para el análisis geométrico. |

**Selección tecnológica preliminar:** debido a que CrackScan busca caracterizar las grietas y no únicamente determinar su presencia, se considera importante investigar alternativas que permitan obtener máscaras de segmentación. DINOv2 se mantiene como una alternativa para el aprovechamiento de características visuales preentrenadas, pero no se asume que resuelva por sí solo la segmentación o medición geométrica.

La selección definitiva dependerá de los resultados experimentales, la disponibilidad de datos y los recursos computacionales del sistema.

### 5.5. Propuesta de validación futura

Para comprobar la utilidad de la tecnología se propone evaluar diferentes aspectos del análisis visual y de la caracterización geométrica.

| Componente | Evaluación propuesta | Indicador |
|---|---|---|
| Identificación de grietas | Comparación de predicciones con imágenes clasificadas como grieta o sin grieta. | Precisión, sensibilidad y F1. |
| Segmentación | Comparación de las máscaras predichas con máscaras de referencia. | IoU y coeficiente Dice. |
| Ancho y longitud | Comparación de mediciones del sistema con mediciones de referencia. | Error absoluto medio. |
| Orientación | Comparación de la orientación estimada con una referencia definida. | Error angular en grados. |
| Patrón visual | Comparación de categorías predichas con categorías de referencia. | Matriz de confusión y F1 por categoría. |
| Viabilidad computacional | Evaluación del tiempo de procesamiento y memoria utilizada. | Tiempo por imagen y consumo de memoria. |

Estas evaluaciones permitirán estudiar la capacidad del modelo para reconocer y caracterizar grietas bajo diferentes condiciones de captura.

Los criterios mínimos de aceptación deberán establecerse antes de realizar las pruebas. Los resultados publicados por otros investigadores no se considerarán resultados propios de CrackScan.

---

## 6. Posibles aplicaciones y evolución tecnológica

El aprendizaje autosupervisado y los modelos de visión fundacionales pueden aplicarse a diferentes problemas de inspección visual, particularmente cuando se requiere identificar patrones o discontinuidades en imágenes.

Entre sus posibles campos de aplicación se encuentran:

- **Inspección de infraestructura:** identificación de grietas y defectos superficiales en elementos de concreto.
- **Evaluación de edificaciones:** apoyo al registro y caracterización preliminar de daños visibles.
- **Inspección de puentes y pavimentos:** análisis automatizado de discontinuidades en superficies.
- **Monitoreo de infraestructura:** organización y comparación de registros visuales obtenidos en diferentes momentos.
- **Sistemas portátiles de inspección:** incorporación de modelos de visión por computadora en dispositivos de captura y registro de información.

### 6.1. Evolución propuesta para CrackScan

A partir de los fundamentos estudiados, se plantean las siguientes actividades para las etapas posteriores del proyecto:

1. **Construcción de un conjunto de imágenes:** recopilar fotografías representativas de superficies de concreto con y sin grietas.

2. **Revisión de conjuntos de datos existentes:** identificar bases de imágenes que puedan utilizarse como referencia para el entrenamiento y evaluación inicial.

3. **Selección de un modelo de visión:** estudiar alternativas como DINOv2 y modelos especializados en detección o segmentación de grietas.

4. **Adaptación del modelo:** evaluar su comportamiento con imágenes representativas de las condiciones previstas para CrackScan.

5. **Caracterización geométrica:** desarrollar procedimientos para estimar ancho, longitud y orientación, incorporando referencias de escala o calibración.

6. **Integración de información geográfica:** asociar los registros visuales con coordenadas GPS e información cartográfica disponible para la zona.

7. **Evaluación de la implementación portátil:** estudiar los recursos de procesamiento, memoria y tiempo necesarios para ejecutar el análisis.

Estas actividades corresponden a propuestas de desarrollo y no representan resultados experimentales ya obtenidos.

---

## 7. Conclusiones

1. El aprendizaje autosupervisado constituye un enfoque de inteligencia artificial que permite obtener representaciones visuales mediante tareas de entrenamiento construidas a partir de los propios datos. Su aplicación puede reducir la dependencia de anotaciones manuales durante determinadas etapas del entrenamiento.

2. Los modelos de visión fundacionales, como DINOv2, permiten reutilizar características visuales obtenidas mediante preentrenamiento autosupervisado y adaptarlas a diferentes tareas de visión por computadora.

3. Las investigaciones revisadas presentan diferentes alternativas para la detección y segmentación de grietas, incluyendo redes generativas, pseudoetiquetado, adaptación de dominio y arquitecturas basadas en transformadores.

4. La identificación de una grieta debe diferenciarse de su caracterización geométrica. Para obtener dimensiones físicas se requieren procedimientos adicionales de escala o calibración.

5. Los antecedentes de propiedad industrial muestran soluciones relacionadas con el procesamiento de imágenes, la detección automatizada de grietas y la inspección visual de superficies. Su revisión permite reconocer tecnologías existentes y establecer diferencias con la propuesta de CrackScan.

6. La revisión bibliográfica permite identificar una oportunidad de investigación relacionada con la adaptación de modelos de visión por computadora a las condiciones de captura previstas para viviendas de Lima Metropolitana, complementando el análisis visual con información geográfica.

7. En conjunto, los artículos científicos, antecedentes tecnológicos y documentos de propiedad industrial revisados constituyen una base documental para sustentar los principios básicos de la tecnología propuesta en esta etapa TRL 1.

**El presente documento no demuestra la implementación ni la validación experimental de CrackScan.** La selección definitiva del modelo, la medición geométrica y la integración de los componentes deberán comprobarse mediante actividades de desarrollo y evaluación posteriores.

---

## Referencias bibliográficas

[1] K. Zhang, Y. Zhang y H. D. Cheng, “Self-supervised structure learning for crack detection based on cycle-consistent generative adversarial networks,” *Journal of Computing in Civil Engineering*, vol. 34, n.º 3, art. 04020004, 2020. doi: [10.1061/(ASCE)CP.1943-5487.0000883](https://doi.org/10.1061/(ASCE)CP.1943-5487.0000883).

[2] M. Oquab et al., “DINOv2: Learning robust visual features without supervision,” *arXiv preprint arXiv:2304.07193*, 2023. doi: [10.48550/arXiv.2304.07193](https://doi.org/10.48550/arXiv.2304.07193).

[3] M. Sohaib, M. J. Hasan, M. A. Shah y Z. Zheng, “A robust self-supervised approach for fine-grained crack detection in concrete structures,” *Scientific Reports*, vol. 14, art. 12646, 2024. doi: [10.1038/s41598-024-63575-x](https://doi.org/10.1038/s41598-024-63575-x).

[4] S. Shim, “Self-supervised domain adaptive approach for extrapolated crack segmentation with fine-tuned inpainting generative model,” *Computer-Aided Civil and Infrastructure Engineering*, vol. 40, n.º 21, pp. 3333–3358, 2025. doi: [10.1111/mice.13517](https://doi.org/10.1111/mice.13517).

[5] T. Zhu et al., “Autonomous detection of concrete cracks using self-supervised DINOv2,” *Machine Intelligence Research*, vol. 23, n.º 1, pp. 168–184, 2026. doi: [10.1007/s11633-025-1553-5](https://doi.org/10.1007/s11633-025-1553-5).

[6] B. A. Kyem, J. K. Asamoah, E. Denteh, A. Danyo y A. Aboah, “Self-supervised multi-scale transformer with Attention-Guided Fusion for efficient crack detection,” *Automation in Construction*, vol. 181, art. 106591, 2026. Disponible en: [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0926580525006314).

[7] J. Cheng, Y. Sun, W. Xiong, W. Chen, Y. Li y Y. Quan, “Defect detection in image space,” patente estadounidense US12260538B2, 25 de marzo de 2025. Disponible en: [Google Patents](https://patents.google.com/patent/US12260538B2/en).

[8] Tianjin Research Institute for Water Transport Engineering, MOT, “Concrete member crack detection method based on deep learning algorithm,” patente china CN118505597B, 7 de noviembre de 2025. Disponible en: [Google Patents](https://patents.google.com/patent/CN118505597B/en).

[9] M. R. Jahanshahi y W. Tang, “Active damage detection system and method for detecting cracks in a surface,” solicitud de patente estadounidense US20250378545A1, 11 de diciembre de 2025. Disponible en: [Google Patents](https://patents.google.com/patent/US20250378545A1/en).

[10] Y. Vashpanov, J.-Y. Son, G. Heo, T. Podousova e Y. S. Kim, “Determination of Geometric Parameters of Cracks in Concrete by Image Processing,” *Advances in Civil Engineering*, vol. 2019, art. 2398124, 2019. doi: [10.1155/2019/2398124](https://doi.org/10.1155/2019/2398124).

[11] S. Sreedhara, T. J. Sorensen, A. Poursaee y B. E. Ross, “Practical Application of Digital Image Processing in Measuring Concrete Crack Widths in Field Studies,” *Practice Periodical on Structural Design and Construction*, vol. 28, n.º 1, 2023. doi: [10.1061/(ASCE)SC.1943-5576.0000735](https://doi.org/10.1061/(ASCE)SC.1943-5576.0000735).

[12] OpenCV, “Camera Calibration,” *OpenCV Documentation*. Disponible en: [OpenCV Documentation](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html).

---

<div align="center">

*CRACKSCAN · TRL 1 · Proyecto Integrador · 2026*

</div>

<div align="center">

**CrackScan — Equipo 06**

</div>
