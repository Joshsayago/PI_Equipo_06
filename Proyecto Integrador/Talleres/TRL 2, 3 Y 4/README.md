# TRL 2, TRL 3 y TRL 4: Desarrollo tecnológico de CrackScan

<div align="center">

**Proyecto:** Sistema inteligente portátil para apoyo a la inspección de grietas en viviendas de Lima Metropolitana.  
**Tecnología emergente:** Aprendizaje autosupervisado y modelos de visión fundacionales para detectar y segmentar grietas en concreto.  
**Equipo:** Equipo 06  

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Computer Vision](https://img.shields.io/badge/Computer_Vision-000000?style=for-the-badge&logo=opencv&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)

</div>

---

## 1. TRL 2: Formulación del concepto tecnológico

### 1.1. Objetivo
Formular el concepto tecnológico de un sistema de análisis visual de grietas en superficies de concreto mediante inteligencia artificial, tomando como base el aprendizaje autosupervisado y los modelos de visión fundacionales estudiados en el TRL 1.  
En esta etapa se establece la arquitectura conceptual de la tecnología, se definen sus componentes, entradas, procesos y salidas, y se identifican los recursos necesarios para desarrollar una prueba de concepto experimental. [1] [2]

### 1.2. Concepto tecnológico propuesto
CrackScan propone desarrollar un sistema de análisis visual capaz de identificar y caracterizar grietas presentes en superficies de concreto mediante fotografías digitales.  
La tecnología se fundamentará en el aprovechamiento de representaciones visuales obtenidas mediante modelos preentrenados, particularmente DINOv2, y su adaptación a tareas específicas de reconocimiento y segmentación de grietas.  
El concepto considera que el análisis se desarrollará en diferentes etapas:
1. Captura de una fotografía de la superficie de concreto.
2. Preprocesamiento de la imagen para adecuarla a los requerimientos del modelo.
3. Extracción de características visuales mediante un modelo de visión.
4. Identificación y segmentación de las regiones correspondientes a las grietas.
5. Procesamiento geométrico de la región segmentada.
6. Obtención de parámetros visuales y geométricos.
7. Registro de los resultados y asociación de metadatos geográficos, cuando se disponga de GPS.  

El sistema estará orientado a proporcionar información preliminar para apoyar la inspección técnica, sin sustituir una evaluación estructural profesional.

### 1.3. Arquitectura tecnológica propuesta
Se plantea una arquitectura modular compuesta por los siguientes elementos:

*   **A. Módulo de adquisición de imágenes:** Recibe fotografías de superficies de concreto mediante una cámara digital o dispositivo móvil. Las imágenes deberán mostrar la superficie de interés con suficiente resolución y condiciones de captura que permitan distinguir las características de las grietas.
*   **B. Módulo de preprocesamiento:** Realiza las operaciones necesarias para preparar las fotografías antes de introducirlas al modelo de inteligencia artificial. Entre las operaciones consideradas se encuentran: redimensionamiento, normalización de valores de píxeles, conversión de formatos, ajustes de contraste y organización de los datos de entrada.
*   **C. Módulo de inteligencia artificial:** Constituye el núcleo tecnológico de CrackScan. Se propone investigar DINOv2 como extractor de características visuales, debido a su capacidad de generar representaciones reutilizables mediante preentrenamiento autosupervisado. Para obtener una segmentación específica de grietas, las características extraídas deberán conectarse con un módulo de segmentación o una cabeza de predicción a nivel de píxel.
*   **D. Módulo de procesamiento geométrico:** Utiliza la máscara de segmentación generada por el modelo para obtener características cuantificables de la grieta:
    *   *Ancho:* abertura transversal de la grieta.
    *   *Longitud:* extensión del recorrido de la grieta.
    *   *Orientación:* dirección predominante respecto de una referencia definida.
    *   *Patrón visual:* configuración de la grieta y sus ramificaciones.  
    *La conversión de píxeles a unidades físicas requerirá una referencia de escala o procedimiento de calibración.*
*   **E. Módulo de georreferenciación y registro:** Permite asociar los resultados del análisis visual con información complementaria (fotografía original, fecha, hora, coordenadas GPS, parámetros geométricos y resultado del análisis visual). La información geográfica se utilizará como metadato y podrá relacionarse con información territorial sobre el nivel de riesgo o daño sísmico.

### 1.4. Entradas, procesos y salidas

| Entradas | Procesamiento | Salidas |
| :--- | :--- | :--- |
| Fotografía digital | Preprocesamiento | Imagen preparada |
| Imagen preparada | Extracción de características | Representación visual |
| Representación visual | Reconocimiento | Identificación de grieta |
| Imagen y características | Segmentación | Máscara de grieta |
| Máscara segmentada | Análisis geométrico | Ancho, longitud y orientación |
| Referencia de escala | Calibración | Dimensiones físicas estimadas |
| Coordenadas GPS | Georreferenciación | Registro de ubicación |

### 1.5. Selección preliminar de herramientas

| Herramienta | Aplicación |
| :--- | :--- |
| **Python** | Lenguaje de programación principal |
| **PyTorch** | Implementación y adaptación de modelos de inteligencia artificial |
| **DINOv2** | Extracción de características visuales |
| **OpenCV** | Preprocesamiento y procesamiento geométrico |
| **NumPy** | Operaciones numéricas y análisis de matrices |
| **Matplotlib** | Visualización de resultados experimentales |
| **Conjunto de datos de grietas** | Entrenamiento, adaptación y evaluación del modelo |

*La disponibilidad de recursos computacionales determinará si el procesamiento se realizará en una computadora durante las primeras pruebas o si posteriormente podrá trasladarse a una plataforma portátil.*

### 1.6. Requerimientos tecnológicos
1. Disponer de fotografías de superficies de concreto con y sin grietas.
2. Contar con imágenes que presenten diferentes características geométricas y condiciones de captura.
3. Disponer de máscaras de referencia para evaluar la segmentación.
4. Implementar un modelo capaz de reconocer o segmentar grietas.
5. Incorporar un procedimiento de calibración para realizar mediciones físicas.
6. Establecer métricas para evaluar el rendimiento del modelo.
7. Garantizar que los registros experimentales puedan asociarse con sus imágenes originales.

### 1.7. Plan preliminar de experimentación
Se propone realizar pruebas iniciales con imágenes digitales de grietas en concreto. Las fotografías deberán incluir variaciones de iluminación, textura, distancia, orientación y abertura de grieta. También se incluirán superficies sin grietas que presenten irregularidades, manchas, juntas o sombras. Se plantea comparar una alternativa convencional de segmentación con una arquitectura que aproveche las características visuales de DINOv2.

### 1.8. Entregables del TRL 2
*   Arquitectura conceptual del sistema.
*   Diagrama de bloques del funcionamiento.
*   Definición de entradas, procesos y salidas.
*   Selección preliminar de herramientas.
*   Identificación de requerimientos tecnológicos.
*   Protocolo inicial de experimentación.
*   Justificación de la arquitectura seleccionada.

### 1.9. Resultado esperado
Al finalizar el TRL 2 se espera disponer de un concepto tecnológico estructurado y técnicamente fundamentado que permita iniciar la implementación experimental del módulo de análisis visual de CrackScan.

---

## 2. TRL 3: Prueba de concepto experimental

### 2.1. Objetivo
Desarrollar una primera implementación experimental del módulo de inteligencia artificial de CrackScan para demostrar que los principios tecnológicos identificados pueden aplicarse al reconocimiento y segmentación de grietas en fotografías de superficies de concreto. [3] [5] [6]

### 2.2. Desarrollo del conjunto de datos
Se recopilarán fotografías de superficies de concreto considerando superficies con grietas longitudinales, transversales, diagonales, ramificadas, sin grietas, y con manchas, sombras y juntas. Para clasificación se asignarán etiquetas de presencia/ausencia; para segmentación se usarán máscaras de referencia. [1]

### 2.3. Implementación del modelo de inteligencia artificial
*   **Experimento 1 (Reconocimiento mediante DINOv2):** Usa un modelo DINOv2 preentrenado para extraer características visuales conectadas a una cabeza de clasificación.
*   **Experimento 2 (Segmentación de grietas):** Implementa una arquitectura que utiliza características visuales de DINOv2 junto con un módulo de segmentación a nivel de píxel.

### 2.4. Procesamiento geométrico preliminar
Una vez obtenida la máscara, se estudia el cálculo de ancho (abertura transversal), longitud (extensión del recorrido), orientación (dirección predominante) y patrón visual (continuidad y ramificaciones).

### 2.5. Diseño experimental
Se divide el conjunto de datos en tres subconjuntos (**entrenamiento, validación y prueba**). Las imágenes de una misma grieta, superficie o vivienda permanecerán en una sola partición para evitar filtraciones de datos.

### 2.6. Evaluación del desempeño

| Componente | Indicador | Finalidad |
| :--- | :--- | :--- |
| Clasificación | Precisión | Evaluar la proporción de predicciones positivas correctas |
| Clasificación | Sensibilidad | Evaluar la capacidad de identificar grietas existentes |
| Clasificación | F1-score | Equilibrar precisión y sensibilidad |
| Segmentación | IoU | Medir la superposición entre la máscara predicha y la real |
| Segmentación | Dice | Evaluar la similitud entre ambas máscaras |
| Medición | Error absoluto medio | Comparar las mediciones con valores de referencia |
| Procesamiento | Tiempo de inferencia | Evaluar el tiempo requerido por imagen |

### 2.7. Comparación de alternativas tecnológicas
Se comparará el enfoque basado en DINOv2 con una alternativa de referencia especializada en segmentación de grietas en términos de calidad, cantidad de datos requeridos, tiempo de procesamiento, consumo de memoria y generalización.

### 2.8. Entregables del TRL 3
*   Conjunto de imágenes organizado y documentado.
*   Código de implementación del modelo.
*   Modelo experimental de clasificación y segmentación.
*   Resultados de las pruebas computacionales y máscaras generadas.
*   Comparación con alternativa de referencia e informe de evaluación.

### 2.9. Resultado esperado
Contar con una prueba de concepto funcional que demuestre experimentalmente la capacidad de un modelo de IA para reconocer y/o segmentar grietas.

---

## 3. TRL 4: Validación tecnológica en laboratorio

### 3.1. Objetivo
Validar experimentalmente el funcionamiento del módulo de análisis visual de CrackScan mediante la integración de sus principales componentes en un entorno controlado de laboratorio. [8] [9]

### 3.2. Desarrollo del prototipo experimental

| Componente | Función |
| :--- | :--- |
| Cámara digital o dispositivo móvil | Captura de imágenes |
| Computadora de procesamiento | Ejecución del modelo de inteligencia artificial |
| Modelo de segmentación | Identificación de los píxeles de la grieta |
| Software de procesamiento | Cálculo de características geométricas |
| Referencia de escala | Calibración de dimensiones |
| Sistema de almacenamiento | Registro de imágenes y resultados |

### 3.3. Preparación de muestras de concreto
Se utilizarán probetas, placas o superficies de concreto con grietas de diferentes características. Las dimensiones reales se obtendrán mediante instrumentos de precisión (microscopios de medición o comparadores de fisuras).

### 3.4. Procedimiento de captura experimental
1. Identificar y registrar la muestra.
2. Realizar medición de referencia.
3. Capturar fotografía con referencia de escala.
4. Procesar mediante el modelo de IA.
5. Obtener máscara, calcular características y comparar con referencias.

### 3.5. Validación de la segmentación
Se compararán las máscaras generadas con referencias manuales usando **IoU** y **Dice**, analizando errores de omisión, falsos positivos por sombras o confusión con juntas. [7]

### 3.6. Validación de las mediciones geométricas
*   **A. Medición del ancho:** Abertura transversal comparada con instrumentos de referencia.
*   **B. Medición de la longitud:** Recorrido o esqueleto geométrico.
*   **C. Medición de la orientación:** Dirección predominante en grados.
*   **D. Caracterización del patrón:** Continuidad y ramificaciones.

### 3.7. Escenarios de validación
*   **Escenario A:** Superficies con grietas finas.
*   **Escenario B:** Superficies con grietas pronunciadas o ramificadas.
*   **Escenario C:** Superficies sin grietas o con irregularidades superficiales.

### 3.8. Integración del registro geográfico
Verificación de la asociación de coordenadas GPS y metadatos. La consulta a bases como SIGRID/CENEPRED se mantendrá diferenciada de los resultados del análisis visual.

### 3.9. Evaluación del funcionamiento integral
Se evaluarán métricas de captura, segmentación (IoU/Dice), mediciones geométricas (error absoluto en mm y grados), tiempo de inferencia, repetibilidad e integridad de datos.

### 3.10. Entregables del TRL 4
*   Prototipo experimental de laboratorio integrado.
*   Registro de muestras, fotografías y máscaras generadas.
*   Comparación con instrumentos de referencia y evaluación de repetibilidad.
*   Informe de validación tecnológica.

### 3.11. Resultado esperado
Contar con un prototipo experimental validado en condiciones controladas de laboratorio, capaz de procesar fotografías, segmentar grietas y estimar características geométricas.

---

## 4. Comparación de las etapas de desarrollo

| Aspecto | TRL 2 | TRL 3 | TRL 4 |
| :--- | :--- | :--- | :--- |
| **Enfoque** | Diseño conceptual | Prueba de concepto | Validación en laboratorio |
| **Inteligencia artificial** | Selección y arquitectura | Implementación experimental | Integración y validación |
| **Datos** | Definición de requerimientos | Conjunto de imágenes | Muestras controladas de concreto |
| **Segmentación** | Diseño del procedimiento | Prueba computacional | Validación experimental |
| **Mediciones** | Definición de métodos | Pruebas preliminares | Comparación con referencias físicas |
| **Hardware** | Identificación de recursos | Computadora de desarrollo | Configuración experimental integrada |
| **Evidencia** | Diagramas y especificaciones | Código y resultados experimentales | Prototipo y resultados de laboratorio |

---

## 5. Continuidad tecnológica de CrackScan
El desarrollo progresivo TRL 2, 3 y 4 permite pasar de la investigación documental a la implementación experimental y validación controlada.  
> **Consideración:** El avance de cada nivel deberá sustentarse en los entregables y resultados efectivamente obtenidos. La formulación de una actividad o protocolo experimental no constituye por sí misma evidencia de que el nivel TRL correspondiente haya sido alcanzado.

---
## 6. Referencias

[1] K. Zhang, Y. Zhang, and H. D. Cheng, “Self-supervised structure learning for crack detection based on cycle-consistent generative adversarial networks,” *Journal of Computing in Civil Engineering*, vol. 34, no. 3, Art. no. 04020004, 2020, doi: 10.1061/(ASCE)CP.1943-5487.0000883.

[2] M. Oquab et al., “DINOv2: Learning robust visual features without supervision,” arXiv preprint arXiv:2304.07193, 2023, doi: 10.48550/arXiv.2304.07193.

[3] M. Sohaib, M. J. Hasan, M. A. Shah, and Z. Zheng, “A robust self-supervised approach for fine-grained crack detection in concrete structures,” *Scientific Reports*, vol. 14, no. 1, Art. no. 12646, 2024, doi: 10.1038/s41598-024-63575-x.

[4] S. Shim, “Self-supervised domain adaptive approach for extrapolated crack segmentation with fine-tuned inpainting generative model,” *Computer-Aided Civil and Infrastructure Engineering*, vol. 40, no. 21, pp. 3333–3358, 2025, doi: 10.1111/mice.13517.

[5] T. Zhu et al., “Autonomous detection of concrete cracks using self-supervised DinoV2,” *Machine Intelligence Research*, vol. 23, no. 1, pp. 168–184, 2026, doi: 10.1007/s11633-025-1553-5.

[6] B. A. Kyem, J. K. Asamoah, E. Denteh, A. Danyo, and A. Aboah, “Self-supervised multi-scale transformer with Attention-Guided Fusion for efficient crack detection,” *Automation in Construction*, vol. 181, Art. no. 106591, 2026.

[7] J. Cheng, Y. Sun, W. Xiong, W. Chen, Y. Li, and Y. Quan, “Defect detection in image space,” U.S. Patent 12,260,538 B2, Mar. 25, 2025.

[8] Tianjin Research Institute for Water Transport Engineering, MOT, assignee, “Concrete member crack detection method based on deep learning algorithm,” Chinese Patent CN118505597B, Nov. 7, 2025.

[9] M. R. Jahanshahi and W. Tang, “Active damage detection system and method for detecting cracks in a surface,” U.S. Patent Application Publication US20250378545A1, Dec. 11, 2025.

<div align="center">

**CrackScan — Equipo 06**

</div>
