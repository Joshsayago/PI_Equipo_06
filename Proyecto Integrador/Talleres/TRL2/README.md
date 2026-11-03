# CrackScan: TRL 2
<div align="center">

**Equipo:** Equipo 06  
**Proyecto:** CrackScan  
**Universidad:** Universidad Peruana Cayetano Heredia   

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Computer Vision](https://img.shields.io/badge/Computer_Vision-000000?style=for-the-badge&logo=opencv&logoColor=white)
![GIS](https://img.shields.io/badge/GIS-5C8A3C?style=for-the-badge&logo=qgis&logoColor=white)
![Hardware](https://img.shields.io/badge/Hardware-555555?style=for-the-badge&logo=arduino&logoColor=white)
![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)

</div>

---

# PARTE I. TRL 2 – FORMULACIÓN DEL CONCEPTO O APLICACIÓN DE LA PROPUESTA TECNOLÓGICA

## 1. Introducción y alcance del TRL 2

CrackScan es una propuesta de sistema inteligente portátil orientado al apoyo de la inspección preliminar de grietas en viviendas de Lima Metropolitana. Surge ante la necesidad de contar con herramientas que faciliten el registro y la caracterización visual de daños superficiales en elementos de concreto, incorporando información geográfica del entorno donde se realiza la inspección.

En esta etapa se formula la aplicación práctica de los principios científicos y tecnológicos que sustentan la propuesta. Se establece cómo podrían integrarse la captura de imágenes, el procesamiento digital, la georreferenciación y la información geoespacial para generar un registro preliminar de las características observadas.

El resultado de este nivel es la definición del concepto tecnológico, su arquitectura funcional, los requerimientos iniciales y la identificación de antecedentes científicos y tecnológicos relacionados.

### 1.1. Problema y aplicación propuesta

La inspección visual de grietas en superficies de concreto permite reconocer manifestaciones físicas como aberturas, fisuras, ramificaciones y variaciones geométricas. Sin embargo, su documentación puede depender de la observación y el registro manual, lo que dificulta estandarizar la información recopilada durante distintas inspecciones.

CrackScan propone desarrollar un dispositivo portátil que permita capturar fotografías de grietas, procesarlas mediante herramientas de visión artificial y asociar los resultados con una ubicación geográfica.

La propuesta considera dos grupos de información:

- **Caracterización visual:** identificación de la presencia de grietas y estimación de características observables, como ancho, longitud, orientación y patrón.
- **Contexto geográfico:** registro de coordenadas mediante GPS y consulta de información geoespacial relacionada con el nivel de riesgo o daño sísmico de la zona.

La combinación de ambas fuentes busca proporcionar información preliminar que permita organizar y priorizar inspecciones técnicas posteriores. El sistema no pretende determinar por sí solo la seguridad estructural de una vivienda ni predecir su colapso.

## 2. Concepto tecnológico y arquitectura funcional

### 2.1. Frontera del sistema

El sistema recibe como entradas una superficie de concreto que será inspeccionada, energía eléctrica para su funcionamiento y la interacción del usuario mediante los controles disponibles.

La cámara obtiene una imagen de la superficie. El procesamiento digital permite analizar sus características visuales y reconocer posibles grietas. Paralelamente, el módulo GPS permite registrar la ubicación geográfica de la inspección.

La información visual y geográfica se organiza para generar un registro que incluya las características identificadas y el contexto territorial consultado.

Las salidas previstas son:

- Imagen de la superficie inspeccionada.
- Identificación de presencia o ausencia de grietas.
- Caracterización geométrica visual.
- Coordenadas geográficas del registro.
- Información geoespacial asociada a la zona.
- Resultado preliminar de apoyo a la priorización de inspecciones.

<p align="center">
 <img width="1133" height="607" alt="image" src="https://github.com/user-attachments/assets/6ea693ad-95d3-4eaf-97e5-d32a33d91b5c" />
  <br>
  <em>Figura 1. Diagrama de caja negra del sistema inteligente portátil para el apoyo a la inspección de grietas.</em>
</p>

 
### 2.2. Secuencia de operación propuesta

| Etapa | Funcionamiento previsto |
|---|---|
| 1. Inicio del sistema | El usuario enciende el dispositivo y verifica la disponibilidad de sus componentes. |
| 2. Captura de imagen | La cámara obtiene una fotografía de la superficie de concreto que será evaluada. |
| 3. Procesamiento visual | El sistema analiza la imagen para identificar posibles grietas y extraer sus características visuales. |
| 4. Georreferenciación | El módulo GPS obtiene las coordenadas geográficas correspondientes al lugar de inspección. |
| 5. Consulta geoespacial | Las coordenadas se utilizan para consultar la información territorial disponible sobre el riesgo o daño sísmico de la zona. |
| 6. Integración de información | Se relacionan las características visuales con el contexto geográfico, conservando ambos datos como fuentes diferenciadas. |
| 7. Generación del registro | Se presenta la información obtenida para apoyar la identificación y priorización de inspecciones técnicas. |

La secuencia representa el funcionamiento conceptual del sistema. La disponibilidad y precisión de cada etapa deberán comprobarse experimentalmente.

### 2.3. Relación entre los módulos

La arquitectura funcional de CrackScan considera cinco módulos principales:

| Módulo | Función | Resultado esperado |
|---|---|---|
| Captura de imágenes | Obtener fotografías de superficies de concreto. | Imagen digital de inspección. |
| Procesamiento de imágenes | Identificar grietas y caracterizar sus propiedades visuales. | Información visual de la grieta. |
| Geolocalización | Obtener coordenadas mediante GPS. | Registro de latitud y longitud. |
| Información geoespacial | Consultar información territorial asociada a la ubicación. | Contexto de riesgo sísmico de la zona. |
| Control y visualización | Coordinar las operaciones y presentar los resultados. | Registro integrado de inspección. |

<p align="center">
 <img width="1115" height="617" alt="image" src="https://github.com/user-attachments/assets/46b4d3f2-b75f-4520-b4e5-1a23b3cfd531" />
  <br>
  <em>Figura 2. Esquema de funciones que representa las principales operaciones del sistema CrackScan.</em>
</p>

 
### 2.4. Fundamentos tecnológicos

**a) Visión artificial y procesamiento digital de imágenes**

La visión artificial permite analizar imágenes digitales mediante algoritmos capaces de reconocer patrones y características visuales. En CrackScan, este fundamento se utilizaría para identificar regiones que presenten características compatibles con grietas en superficies de concreto.

El análisis podría incluir técnicas de clasificación y segmentación. La clasificación permitiría distinguir imágenes con y sin grietas, mientras que la segmentación permitiría delimitar los píxeles correspondientes a la grieta.

**b) Caracterización geométrica**

La caracterización visual considera parámetros como ancho, longitud, orientación y patrón. Para convertir dimensiones expresadas en píxeles a unidades físicas, como milímetros, será necesario incorporar una referencia de escala o un procedimiento de calibración.

Por ello, la identificación visual de una grieta no equivale automáticamente a una medición física exacta.

**c) Sistema de posicionamiento global (GPS)**

El GPS permite obtener coordenadas geográficas mediante señales de satélites. En CrackScan, su función será asociar cada registro de inspección con una ubicación, permitiendo relacionar posteriormente la observación con información territorial.

**d) Sistemas de información geográfica (SIG)**

Los SIG permiten almacenar, analizar y representar información asociada a ubicaciones geográficas. Su aplicación en CrackScan permitirá consultar información territorial disponible mediante coordenadas, considerando las capas relacionadas con el riesgo o daño sísmico de la zona.

**e) Integración de información**

La integración propuesta relaciona la caracterización visual de la grieta con el contexto geográfico de la inspección. Ambas fuentes aportan información complementaria, pero no representan una relación causal directa ni sustituyen una evaluación estructural especializada.

## 3. Objetivo e hipótesis de trabajo

**Objetivo del TRL 2.**

Formular el concepto tecnológico de un sistema portátil que integre el análisis visual de grietas en superficies de concreto con información geográfica del entorno, para apoyar el registro y la priorización preliminar de inspecciones técnicas en viviendas de Lima Metropolitana.

**Hipótesis de trabajo.**

La integración de herramientas de procesamiento de imágenes, georreferenciación e información geoespacial permitiría organizar información visual y territorial de una inspección en un único registro, facilitando la identificación de viviendas que podrían requerir una evaluación técnica posterior.

**Pregunta de investigación.**

¿En qué medida la integración del análisis visual de grietas y la información geográfica del entorno puede contribuir a generar registros preliminares útiles para priorizar inspecciones técnicas en viviendas?

## 4. Estado del arte aplicado a CrackScan

La propuesta se sustenta en investigaciones relacionadas con la inspección visual de concreto, la detección automatizada de grietas y el análisis de imágenes digitales.

| Referencia | Trabajo | Aporte principal | Relación con CrackScan |
|---|---|---|---|
| [1] | Dorafshan et al. (2018). SDNET2018. | Presenta un conjunto de más de 56 000 imágenes de concreto con y sin grietas, incluyendo superficies de muros, pavimentos y tableros de puentes. | Proporciona un antecedente para desarrollar y evaluar modelos de detección de grietas mediante imágenes. |
| [2] | ACI PRC-228.4-23 (2023). Visual Condition Survey of Concrete. | Desarrolla criterios para planificar, ejecutar y documentar inspecciones visuales de estructuras de concreto. | Sustenta la identificación y documentación de características visibles, incluyendo grietas y sus dimensiones geométricas. |
| [3] | Zhu et al. (2021). DeepCrack. | Presenta un conjunto de datos y un enfoque de aprendizaje profundo para la segmentación de grietas. | Constituye un antecedente para estudiar la delimitación de grietas a nivel de píxel. |

### 4.1. Análisis de los antecedentes

SDNET2018 constituye una referencia importante porque reúne imágenes de superficies de concreto con diferentes condiciones visuales. Incluye grietas de distintas dimensiones y obstáculos como sombras, rugosidad, bordes y manchas. Esto permite reconocer que un sistema de detección debe evaluarse frente a variaciones que pueden dificultar el reconocimiento automático [1].
<p align="center">
  <img width="393" height="345" alt="image" src="https://github.com/user-attachments/assets/62d7197f-b1bc-4db7-b13b-94961fdcc52c" />

  <br>
  <em>Figura 5. Ejemplos de imágenes del conjunto de datos SDNET2018 que muestran: (a) grietas finas, (b) grietas gruesas, (c) sombras, (d) manchas, (e) superficies rugosas, (f) inclusiones y vacíos, (g) bordes, (h) juntas y descascaramiento superficial, e (i) obstrucciones en el fondo.</em>
</p>


Por otro lado, la guía ACI PRC-228.4-23 establece criterios para realizar inspecciones visuales y documentar características físicas observables. Su contenido permite orientar los parámetros que CrackScan pretende registrar, sin asumir que la observación visual determina por sí sola la condición estructural completa [2].

Finalmente, DeepCrack aporta antecedentes para la segmentación de grietas, una tarea que permitiría delimitar su forma y extensión en una imagen [3].

### 4.2. Brecha de aplicación identificada

Los antecedentes revisados desarrollan herramientas para reconocer, segmentar o documentar grietas en superficies de concreto. Sin embargo, la propuesta de CrackScan busca integrar estas funciones con el registro geográfico y la consulta de información territorial relacionada con el contexto sísmico.

La oportunidad de aplicación identificada consiste en evaluar la integración de:

1. Captura portátil de imágenes de superficies de concreto.
2. Caracterización visual de grietas.
3. Registro de coordenadas geográficas.
4. Consulta de información geoespacial.
5. Organización conjunta de información visual y territorial.

Esta integración deberá validarse mediante pruebas específicas. No se afirma que represente una tecnología inédita a nivel mundial.

## 5. Análisis preliminar de patentabilidad y protección

### 5.1. Antecedentes tecnológicos

La búsqueda de antecedentes permite reconocer soluciones previamente desarrolladas para la inspección de grietas mediante imágenes y sistemas portátiles.

| Documento | Tecnología descrita | Relación y diferencia con CrackScan |
|---|---|---|
| EP1813934A1. Concrete structure crack inspection device and crack inspection method. | Describe la captura de imágenes de estructuras de concreto, procesamiento de datos y representación de grietas mediante información vectorial. | Comparte el análisis de imágenes y la caracterización geométrica. CrackScan plantea incorporar además el registro geográfico y la consulta de información territorial. |
| US8873837B2. Image-based crack detection. | Describe métodos de detección y cuantificación de grietas mediante procesamiento de imágenes y reconocimiento de patrones. | Es un antecedente directo de análisis visual automatizado. No demuestra la integración específica propuesta por CrackScan. |
| CA3122674A1. Electrical methods and systems for concrete testing. | Describe sistemas portátiles de inspección de concreto que incorporan procesamiento de imágenes para detectar y caracterizar daños. | Se relaciona con la inspección portátil y el procesamiento de imágenes. La propuesta de CrackScan incorpora como elemento adicional el contexto geoespacial de la ubicación. |

### 5.2. Análisis preliminar

La revisión evidencia que la captura y el procesamiento de imágenes para detectar grietas cuentan con antecedentes tecnológicos. Por ello, la utilización de una cámara o un algoritmo de detección no constituye, por sí sola, una característica novedosa.

El aspecto que merece mayor análisis es la integración funcional entre la caracterización visual de grietas, la georreferenciación y la consulta de información geoespacial dentro de un sistema portátil de apoyo a la inspección.

| Criterio | Evaluación preliminar |
|---|---|
| Novedad | Requiere comparar la combinación funcional propuesta con los documentos y soluciones existentes. |
| Nivel inventivo | Debe determinarse si la integración propuesta presenta una solución técnica que no resulte evidente a partir de los antecedentes. |
| Aplicación industrial | Se plantea una aplicación en el registro y apoyo a la inspección preliminar de viviendas. |
| Descripción suficiente | Se cuenta con el concepto funcional, el diseño 3D y los esquemas del sistema. Los parámetros de funcionamiento y la integración deberán precisarse. |

Esta evaluación es exploratoria y no constituye una opinión legal de patentabilidad. La protección de una eventual invención requerirá una búsqueda más exhaustiva de documentos y reivindicaciones.

## 6. Diseño conceptual y requisitos de ingeniería

### 6.1. Diseño tridimensional

El equipo cuenta con un diseño tridimensional del dispositivo CrackScan. Este diseño constituye un avance en la definición de la configuración física del sistema y permite visualizar la disposición prevista de sus componentes.

La correspondencia entre el diseño 3D y la distribución electrónica definitiva deberá comprobarse mediante la revisión de las dimensiones, soportes, espacios internos y conexiones.

 <p align="center">
<img width="323" height="287" alt="image" src="https://github.com/user-attachments/assets/e062f56e-724a-4190-8af6-7a2f2332fcc2" />
<img width="607" height="393" alt="image" src="https://github.com/user-attachments/assets/76e9bb0b-73e6-4691-bafe-9408965163b8" />
<img width="372" height="270" alt="image" src="https://github.com/user-attachments/assets/3659d7c5-5718-4e87-b39a-14631d6a6089" />

  <br>
  <em>Figura 3. Diseño tridimensional de la estructura del prototipo portátil CrackScan.</em>
</p>
 
### 6.2. Requisitos de diseño

| Requisito | Implementación prevista | Verificación posterior |
|---|---|---|
| Portabilidad | Estructura compacta que permita el traslado y uso durante inspecciones. | Evaluar dimensiones, peso y facilidad de manipulación. |
| Captura de imágenes | Cámara integrada al dispositivo. | Comprobar calidad y estabilidad de las fotografías. |
| Procesamiento visual | Algoritmo de detección y caracterización de grietas. | Evaluar resultados con imágenes de referencia. |
| Georreferenciación | Módulo GPS. | Comparar coordenadas con una ubicación de referencia. |
| Consulta geoespacial | Acceso a información territorial mediante coordenadas. | Verificar correspondencia entre ubicación y capa consultada. |
| Alimentación | Sistema de alimentación eléctrica para los componentes. | Comprobar autonomía y estabilidad de funcionamiento. |
| Visualización | Interfaz para presentar la información de inspección. | Verificar que los datos se presenten correctamente. |

### 6.3. Selección de componentes

Los materiales y componentes principales del proyecto han sido adquiridos por el equipo. Su selección responde a los requerimientos de captura, procesamiento, posicionamiento y alimentación del dispositivo.

 
| N.° | Material o componente | Especificaciones |
|:---:|---|---|
| 1 |XIAO ESP32S3 Sense | Microcontrolador con conectividad Wi-Fi y Bluetooth, cámara integrada y micrófono digital, utilizado como unidad de procesamiento y control del sistema. |
| 2 | Pantalla OLED | 2.4 pulgadas, resolución 128 × 64, color blanco, interfaz I2C, controlador SSD1309 y alimentación de 3.3 V. |
| 3 | Módulo MT3608 | Módulo elevador de tensión DC-DC (Boost). |
| 4 | Portapilas para batería 18650 | Portapilas para soldar, compatible con batería de litio de 3.7 V. |
| 5 | Switch de encendido | Interruptor de 2 pines, color rojo, de presión y sin tornillos. |
| 6 | Botón pulsador | Redondo, de 1 a 2 cm, con cuerpo roscado y tuerca de ajuste. |
| 7 | Anillo de LEDs RGB | Tipo 5050 WS2812, de 16 LEDs o configuración similar en cadena. |
| 8 | Extensión USB tipo C | Conector macho a hembra. |
| 9 | Cables de conexión (jumpers) | Configuraciones hembra-macho, macho-macho y hembra-hembra. |
| 10 | Tiras de pines soldables | Juegos de pines macho y hembra. |
| 11 | Conectores para PCB | Bloques terminales de tornillo, de color verde o azul. |
| 12 | Tornillos M3 × 20 mm | 10 unidades. |
| 13 | Tornillos M3 × 10 mm | 4 unidades. |
| 14 | Tornillos M3 × 5 mm | 4 unidades. |

La adquisición de materiales representa un avance en la preparación de la implementación física. Sin embargo, la disponibilidad de los componentes no demuestra todavía su integración ni su funcionamiento conjunto.

## 7. Perfil del proyecto

**Usuarios y aplicación.** CrackScan está orientado a apoyar el registro preliminar de grietas en superficies de concreto de viviendas de Lima Metropolitana. Su información podría resultar útil para organizar inspecciones y reconocer ubicaciones que requieran una evaluación técnica posterior.

**Alcance.** El sistema busca identificar y caracterizar visualmente grietas, asociar los registros con coordenadas geográficas y consultar información territorial relacionada con el contexto sísmico.

**Limitaciones.** El resultado no representa un diagnóstico estructural ni una certificación de seguridad de la vivienda. La interpretación de los daños y la determinación de la condición estructural corresponden a profesionales competentes.

**Entregables del TRL 2.**

- Concepto tecnológico formulado.
- Caja negra y esquema de funciones.
- Secuencia de operación.
- Diseño tridimensional.
- Requerimientos iniciales de ingeniería.
- Revisión de antecedentes científicos.
- Análisis preliminar de propiedad intelectual.

## 8. Conclusiones del TRL 2

1. Se formuló el concepto tecnológico de CrackScan como un sistema portátil que integra caracterización visual de grietas y contexto geográfico.
2. Se identificaron los fundamentos de visión artificial, procesamiento digital de imágenes, GPS y sistemas de información geográfica.
3. La revisión científica permitió identificar antecedentes para la detección, segmentación y documentación de grietas en superficies de concreto.
4. La revisión de patentes evidenció que existen antecedentes de inspección mediante imágenes, por lo que la integración funcional propuesta debe evaluarse frente a las soluciones existentes.
5. El diseño tridimensional, la adquisición de materiales y los esquemas funcionales constituyen avances de diseño para preparar la construcción y validación experimental del sistema.

---
 
# 24. Referencias bibliográficas

[1] S. Dorafshan, R. J. Thomas, and M. Maguire, “SDNET2018: An annotated image dataset for non-contact concrete crack detection using deep convolutional neural networks,” *Data in Brief*, vol. 21, pp. 1664–1668, 2018. https://doi.org/10.1016/j.dib.2018.11.015

[2] American Concrete Institute, *ACI PRC-228.4-23: Visual Condition Survey of Concrete—Guide*. ACI Committee 228, 2023. https://www.concrete.org/publications/internationalconcreteabstractsportal.aspx?id=51740314

[3] Y. Liu, J. Yao, X. Lu, R. Xie, and L. Li, “DeepCrack: A deep hierarchical feature learning architecture for crack segmentation,” *Neurocomputing*, vol. 338, pp. 139–153, 2019. https://doi.org/10.1016/j.neucom.2019.01.036



