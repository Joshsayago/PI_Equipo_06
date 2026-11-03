# PARTE III. TRL 4 – VALIDACIÓN TECNOLÓGICA EN ENTORNO DE LABORATORIO

## 15. Introducción y alcance del TRL 4

El TRL 4 corresponde a la validación tecnológica en un entorno de laboratorio mediante un prototipo de baja fidelidad. En esta etapa se busca integrar componentes básicos para comprobar que pueden funcionar conjuntamente bajo condiciones controladas.

Para CrackScan, esta fase considera la integración progresiva de la estructura física, el sistema de captura de imágenes, el procesamiento visual, la georreferenciación y la consulta de información geoespacial.

El objetivo no es demostrar todavía el funcionamiento definitivo del dispositivo en viviendas reales, sino comprobar que la arquitectura básica puede ejecutar una secuencia de inspección simulada y producir registros coherentes.

## 16. Objetivo e hipótesis de validación

**Objetivo del TRL 4.**

Integrar los componentes básicos de CrackScan en un prototipo de baja fidelidad y evaluar su funcionamiento conjunto mediante pruebas controladas en un entorno de laboratorio.

**Hipótesis de validación.**

La integración de los módulos de captura, procesamiento visual, georreferenciación y consulta geoespacial permitirá ejecutar una secuencia básica de inspección simulada, generando registros que relacionen las características visuales de una superficie con su ubicación geográfica.

## 17. Arquitectura del prototipo integrado

### 17.1. Integración física

La estructura tridimensional desarrollada durante la etapa de diseño constituye la base para organizar los componentes del dispositivo.

En esta fase se deberá comprobar la correspondencia entre el diseño y los materiales adquiridos, considerando:

- Espacios disponibles para los componentes electrónicos.
- Ubicación y orientación de la cámara.
- Acceso a los controles y conexiones.
- Distribución de la alimentación eléctrica.
- Protección y estabilidad de los módulos.
- Facilidad de manipulación del dispositivo.
  
### 17.2. Integración electrónica

La integración electrónica deberá permitir la comunicación entre el microcontrolador y los módulos correspondientes.

Se propone verificar progresivamente:

1. Alimentación eléctrica del sistema.
2. Encendido y funcionamiento del microcontrolador.
3. Comunicación con la cámara o módulo de captura.
4. Lectura de información del módulo GPS.
5. Comunicación con los dispositivos de salida, cuando corresponda.
6. Estabilidad del sistema durante una secuencia de operación.

La integración definitiva dependerá de las características técnicas y compatibilidad de los componentes seleccionados.

<p align="center">
 <img width="1135" height="706" alt="image" src="https://github.com/user-attachments/assets/b336a009-0eef-4a61-a20a-20c3843ccf0c" />
  <br>
  <em>Figura 4. Esquema electrónico de las conexiones entre los componentes del sistema CrackScan.</em>
</p>

 
### 17.3. Integración del procesamiento de imágenes

El módulo de procesamiento deberá recibir las fotografías capturadas y ejecutar el procedimiento de análisis visual seleccionado.

La integración considerará:

- Recepción de la imagen.
- Preparación y procesamiento digital.
- Identificación de posibles grietas.
- Obtención de una región o máscara de la grieta, cuando se utilice segmentación.
- Extracción de características visuales.
- Almacenamiento de los resultados.

Si el procesamiento requiere más capacidad computacional que la disponible en el microcontrolador, podrá ejecutarse en una computadora o plataforma externa durante las primeras pruebas de laboratorio.

Esta alternativa permitirá evaluar la funcionalidad del sistema sin asumir que el modelo de inteligencia artificial puede ejecutarse directamente en cualquier placa electrónica.

### 17.4. Integración geoespacial

La información obtenida mediante GPS deberá asociarse al registro de inspección. Posteriormente, las coordenadas podrán utilizarse para consultar la información territorial disponible.

La integración deberá conservar la correspondencia entre:

- Identificador de inspección.
- Fotografía capturada.
- Características visuales obtenidas.
- Coordenadas geográficas.
- Fuente cartográfica consultada.
- Información territorial recuperada.

La asociación de estos datos permitirá mantener la trazabilidad de cada inspección.

## 18. Pruebas de baja fidelidad

### 18.1. Prueba de secuencia de operación

**Objetivo:** comprobar que los módulos básicos pueden ejecutar una secuencia de inspección simulada.

**Procedimiento propuesto:**

1. Encender el prototipo.
2. Iniciar una inspección de prueba.
3. Capturar una fotografía de una superficie de concreto.
4. Ejecutar el procesamiento visual disponible.
5. Obtener o incorporar una coordenada geográfica de prueba.
6. Consultar la información territorial correspondiente.
7. Generar un registro con los resultados.
8. Verificar que la información permanezca asociada al mismo identificador de inspección.

**Indicadores:**

| Indicador | Criterio de evaluación |
|---|---|
| Captura | La imagen se obtiene y almacena correctamente. |
| Procesamiento | El módulo recibe la imagen y genera una salida. |
| Georreferenciación | Se registra una coordenada válida o una coordenada de prueba identificada como tal. |
| Consulta geoespacial | Se obtiene información de la fuente cartográfica seleccionada o se registra su indisponibilidad. |
| Integración | Los resultados se asocian a un mismo registro de inspección. |

### 18.2. Prueba de repetibilidad

**Objetivo:** evaluar si el sistema genera registros consistentes cuando se repite una inspección bajo condiciones similares.

**Procedimiento propuesto:**

1. Seleccionar una superficie de concreto con una grieta visible.
2. Capturar varias fotografías manteniendo condiciones de distancia e iluminación similares.
3. Procesar las imágenes mediante el mismo procedimiento.
4. Comparar las características visuales obtenidas.
5. Registrar las variaciones observadas.
6. Repetir el procedimiento con una superficie sin grietas.

La prueba permitirá identificar si los cambios en la iluminación, orientación o distancia afectan el resultado del análisis visual.

### 18.3. Prueba de trazabilidad

**Objetivo:** verificar que cada registro conserve la correspondencia entre imagen, características visuales y ubicación geográfica.

**Procedimiento propuesto:**

1. Generar un identificador único para cada inspección.
2. Asociar una fotografía al identificador.
3. Incorporar las características visuales obtenidas.
4. Registrar las coordenadas geográficas.
5. Incorporar la información territorial consultada.
6. Recuperar el registro y comprobar que los datos correspondan a la misma inspección.

### 18.4. Prueba de funcionamiento en entorno simulado

Se propone utilizar superficies de concreto, fotografías de referencia y ubicaciones geográficas de prueba para reproducir las condiciones básicas de una inspección.

Esta prueba permitirá evaluar el funcionamiento del sistema sin requerir todavía una aplicación en viviendas reales.
 
## 19. Matriz de validación del prototipo

| Componente | Prueba | Evidencia requerida | Estado |
|---|---|---|---|
| Estructura física | Revisión del ensamble y distribución de componentes. | Fotografías y dimensiones del prototipo. | Pendiente de verificación. |
| Cámara | Captura de imágenes de prueba. | Fotografías almacenadas. | Pendiente de ejecución. |
| Procesamiento visual | Análisis de imágenes con y sin grietas. | Predicciones y métricas de evaluación. | Pendiente de ejecución. |
| GPS | Obtención de coordenadas. | Registro de latitud y longitud. | Pendiente de ejecución. |
| Información geoespacial | Consulta de coordenadas en una capa territorial. | Capturas y registro de atributos. | Pendiente de ejecución. |
| Integración | Ejecución de una secuencia de inspección. | Registro completo de una prueba. | Pendiente de ejecución. |
| Trazabilidad | Recuperación de los datos asociados a una inspección. | Registro con identificador único. | Pendiente de ejecución. |

Los estados deberán actualizarse únicamente después de realizar y documentar las pruebas correspondientes.

## 20. Criterios de aceptación preliminares

Para considerar satisfactoria la validación de baja fidelidad, se proponen los siguientes criterios:

| Criterio | Condición esperada |
|---|---|
| Captura de imágenes | Obtener y almacenar fotografías sin errores. |
| Procesamiento | Recibir imágenes y generar resultados verificables. |
| Georreferenciación | Registrar coordenadas válidas o identificar claramente datos de prueba. |
| Consulta geoespacial | Recuperar información cuando la fuente y la capa estén disponibles. |
| Integración | Ejecutar la secuencia básica sin perder la correspondencia entre módulos. |
| Trazabilidad | Conservar los datos asociados a cada inspección. |

Los valores cuantitativos de desempeño deberán establecerse después de obtener resultados experimentales iniciales. No se asignarán porcentajes de precisión ni tolerancias sin mediciones que los respalden.

## 21. Limitaciones y aspectos pendientes

Durante la validación de baja fidelidad deberán considerarse las siguientes limitaciones:

1. **Variabilidad de las superficies:** las manchas, sombras, juntas y rugosidad pueden confundirse con grietas.
2. **Calibración de medidas:** la estimación de ancho y longitud requiere una referencia física de escala.
3. **Condiciones de captura:** la distancia, iluminación y orientación de la cámara pueden afectar el análisis.
4. **Disponibilidad GPS:** la recepción de señal puede variar según el entorno.
5. **Disponibilidad geoespacial:** la consulta depende de las capas, atributos y servicios disponibles.
6. **Capacidad computacional:** el modelo de procesamiento podría requerir una plataforma externa.
7. **Alcance de la evaluación:** la información obtenida no sustituye una inspección estructural profesional.

## 22. Conclusiones del TRL 4

1. Se definió una propuesta de integración de los componentes físicos, electrónicos, computacionales y geoespaciales de CrackScan.
2. Se establecieron pruebas de baja fidelidad para evaluar el funcionamiento conjunto de los módulos en un entorno de laboratorio.
3. La validación deberá comprobar la continuidad de la secuencia de inspección y la correspondencia entre imágenes, características visuales y coordenadas.
4. La evaluación del procesamiento visual deberá considerar métricas específicas y conjuntos de prueba independientes.
5. La integración funcional del prototipo y sus resultados deberán documentarse mediante evidencias experimentales antes de afirmar que se ha alcanzado la validación tecnológica correspondiente.

---

# 23. Proyección de desarrollo tecnológico

La evolución de CrackScan se plantea de manera progresiva, de acuerdo con los resultados que se obtengan en cada etapa.

| Nivel | Resultado esperado | Evidencia principal |
|---|---|---|
| TRL 2 | Concepto tecnológico formulado. | Arquitectura funcional, diseño 3D, antecedentes científicos y análisis de patentes. |
| TRL 3 | Viabilidad experimental de componentes principales. | Datos de ensayos y demostraciones individuales. |
| TRL 4 | Integración básica y validación en laboratorio. | Prototipo funcional de baja fidelidad y resultados de pruebas controladas. |

El desarrollo posterior deberá considerar la optimización del procesamiento visual, la mejora de la calibración geométrica, la estabilidad de la georreferenciación y la evaluación del sistema bajo condiciones de captura más cercanas a las de una inspección real.

---

# 24. Referencias bibliográficas

[1] S. Dorafshan, R. J. Thomas, and M. Maguire, “SDNET2018: An annotated image dataset for non-contact concrete crack detection using deep convolutional neural networks,” *Data in Brief*, vol. 21, pp. 1664–1668, 2018. https://doi.org/10.1016/j.dib.2018.11.015

[2] American Concrete Institute, *ACI PRC-228.4-23: Visual Condition Survey of Concrete—Guide*. ACI Committee 228, 2023. https://www.concrete.org/publications/internationalconcreteabstractsportal.aspx?id=51740314

[3] Y. Liu, J. Yao, X. Lu, R. Xie, and L. Li, “DeepCrack: A deep hierarchical feature learning architecture for crack segmentation,” *Neurocomputing*, vol. 338, pp. 139–153, 2019. https://doi.org/10.1016/j.neucom.2019.01.036

[4] “Concrete structure crack inspection device and crack inspection method,” European Patent EP1813934A1, 2007. https://patents.google.com/patent/EP1813934A1/en

[5] “Image-based crack detection,” U.S. Patent US8873837B2, 2014. https://patents.google.com/patent/US8873837B2/en

[6] “Electrical methods and systems for concrete testing,” Canadian Patent Application CA3122674A1, 2021. https://patents.google.com/patent/CA3122674A1/en

[7] Centro Nacional de Estimación, Prevención y Reducción del Riesgo de Desastres (CENEPRED), Sistema de Información para la Gestión del Riesgo de Desastres (SIGRID). https://sigrid.cenepred.gob.pe/

