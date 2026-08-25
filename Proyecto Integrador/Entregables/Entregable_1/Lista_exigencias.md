# LISTA DE EXIGENCIAS

**PROYECTO:** Sistema inteligente portátil para monitoreo y clasificación del riesgo asociado a grietas en viviendas de concreto  
**Fecha:** 23/08/2026  

**Revisado:**  

**CLIENTE:** UNIVERSIDAD PERUANA CAYETANO HEREDIA  
**Elaborado:** D.M, P.M, B.B, M.H, J.S  

| N.° | Fecha | E/D | Exigencia / Deseo | Responsable |
|---:|---|:---:|---|---|
| 1 | 21/08/26 | **E** | **Función principal:** Detectar y registrar grietas en estructuras de concreto, identificando características con el propósito de facilitar la priorización de inspecciones técnicas[1].  | D.M, P.M, B.B, M.H, J.S |
| 2 | 23/08/26 | **E** | **Geometría:** El dispositivo deberá contar con dimensiones reducidas que permitan su transporte y utilización durante inspecciones de viviendas. La estructura deberá permitir incorporar sensores, cámara, sistema de procesamiento y elementos de visualización sin dificultar su manipulación. | M.H |
| 3 | 23/08/26 | **E** | **Cinemática:** El sistema deberá permitir el posicionamiento y desplazamiento de la cámara sobre diferentes zonas de la superficie de concreto. Durante la captura de imágenes se deberá mantener una posición estable para evitar movimientos que generen imágenes borrosas o alteren los resultados del análisis. | J.S |
| 4 | 23/08/26 | **E** | **Fuerzas:** El dispositivo no deberá ejercer fuerzas significativas sobre la superficie inspeccionada que puedan modificar o ampliar las grietas. Los elementos de contacto deberán utilizarse únicamente para posicionamiento o referencia de medición. | J.S |
| 5 | 23/08/26 | **E** | **Energía:** El sistema deberá utilizar una fuente de alimentación portátil y de baja tensión adecuada para el funcionamiento del ESP32, sensores, cámara y demás componentes electrónicos. Se priorizará un bajo consumo energético para permitir varias inspecciones antes de recargar el dispositivo. | D.M, P.M |
| 6 | 23/08/26 | **E** | **Materia:** La materia de entrada estará constituida por superficies de concreto endurecido con presencia o ausencia de grietas visibles [2]. | M.H |
| 7 | 23/08/26 | **E** | **Señales (Información):** Deberá contar con señales de entrada y salida necesarias para el monitoreo y control del sistema.<br><br>**Señales de entrada:** activación del sistema, inicio de inspección, captura de imagen, lectura de sensores y selección del punto de evaluación.<br><br>**Señales de salida:** dimensiones/características de la grieta, condición detectada, nivel de riesgo, alerta y resultado de la inspección. | D.M, P.M |
| 8 | 23/08/26 | **E** | **Control:** El sistema deberá controlar la adquisición periódica de datos, procesamiento de las imágenes y/o señales, almacenamiento de resultados y generación de alertas. | D.M, P.M |
| 9 | 23/08/26 | **E** | **Electrónico (hardware):** Se utilizará un controlador adecuado para la adquisición y procesamiento de información. Se integrará una cámara para registrar las grietas, sensores de movimiento/vibración o aceleración y sensores ambientales según los requerimientos definidos durante el desarrollo. | D.M, P.M |
| 10 | 23/08/26 | **E** | **Software:** El software deberá permitir procesar los datos de sensores y actuadores, integrar información pública sobre los tipos de suelo del Perú, visualizar los resultados mediante una aplicación o plataforma web, operar de forma automática o manual, presentar información comprensible y permitir futuras modificaciones o ampliaciones. | D.M, P.M |
| 11 | 23/08/26 | **E** | **Comunicaciones:** La unidad de procesamiento deberá comunicarse con la cámara y los demás componentes mediante conexión inalámbrica. Asimismo, deberá permitir transmitir los resultados hacia la plataforma de almacenamiento o visualización. | D.M, P.M |
| 12 | 23/08/26 | **E** | **Seguridad:** El sistema deberá garantizar una operación segura para el usuario y proteger sus componentes eléctricos y electrónicos. Durante el diseño se tomará como referencia la ISO 12100 para identificar peligros, estimar y evaluar los riesgos, y establecer medidas para eliminarlos o reducirlos [3]. Asimismo, se considerará la IEC 60529 para seleccionar la protección de la carcasa frente al ingreso de polvo y agua [4] y la Ley N.° 29783 de Seguridad y Salud en el Trabajo [5]. | B.B |
| 13 | 23/08/26 | **E** | **Ergonomía:** El dispositivo deberá ser portátil, ligero y sencillo de manipular. Los elementos de captura y control deberán ubicarse de manera que permitan realizar una inspección sin adoptar posiciones incómodas durante periodos prolongados que comprometan la salud y en conformidad con la norma ISO 7250 (Basic human body measurements for technological design) [6]. | M.H |
| 14 | 23/08/26 | **E** | **Fabricación:** El sistema deberá fabricarse con materiales disponibles en el mercado nacional, permitiendo el fácil reemplazo de componentes electrónicos. Se considerarán componentes nacionales o importados con tiempos de adquisición de 5 a 15 días. La carcasa y soporte deberán ser resistentes y proteger los componentes frente al polvo y humedad, tomando como referencia la IEC 60529. Asimismo, las piezas deberán presentar un acabado superficial adecuado según la ISO 21920-1 [7]. | B.B |
| 15 | 23/08/26 | **E** | **Control de calidad:** El diseño y fabricación del sistema deberá cumplir con las exigencias establecidas, considerando dimensiones, materiales, seguridad y funcionamiento. La detección y medición de grietas se validará mediante comparación con mediciones de referencia, evaluando la precisión, error y repetibilidad del sistema. | J.S |
| 16 | 23/08/26 | **E** | **Montaje:** El sistema tendrá un diseño portátil y de fácil montaje, permitiendo posicionar temporalmente frente a la superficie de concreto. Sus componentes deberán mantenerse firmes durante la inspección y permitir un rápido ensamblaje y desmontaje para facilitar su transporte y mantenimiento. | M.H |
| 17 | 23/08/26 | **D** | **Transporte:** El sistema deberá ser portátil y permitir su traslado manual. Como meta de diseño, el equipo completo deberá mantenerse por debajo de aproximadamente **3 kg** y sus componentes deberán permanecer protegidos mediante una carcasa durante su transporte. | P.M |
| 18 | 23/08/26 | **D** | **Uso:** El sistema estará diseñado inicialmente para trabajar principalmente en superficies de concreto accesibles y bajo condiciones controladas o semicontroladas de iluminación.<br><br>Como rango de diseño preliminar para los componentes electrónicos se considerarán temperaturas ambientales aproximadas de **5 °C a 40 °C** y humedad relativa de hasta **85 % sin condensación**.<br><br>La iluminación deberá mantenerse lo más uniforme posible durante la captura para reducir sombras, reflejos y cambios de contraste que puedan ser interpretados erróneamente como grietas.<br><br>El sistema será una herramienta de apoyo a la inspección y no reemplazará la evaluación realizada por un profesional especializado. | M.H |
| 19 | 23/08/26 | **E** | **Mantenimiento:** **Componentes mecánicos:** deberán permitir un fácil acceso para su inspección, limpieza, ajuste, reparación o reemplazo.<br><br>**Componentes electrónicos:** la cámara, controlador y demás componentes deberán permitir su calibración, inspección y reemplazo individual en caso de falla. | J.S |
| 20 | 23/08/26 | **D** | **Costos:** Se priorizará el uso de materiales y componentes de bajo costo y fácil adquisición. Se estima que el costo de materiales del prototipo no deberá superar los **S/ 400**, considerando la cámara, controlador, sistema de alimentación, carcasa, soporte y componentes electrónicos necesarios. | B.B |
| 21 | 23/08/26 | **E** | **Plazos:** El proyecto empezará el martes **18 de agosto de 2026** y espera su finalización el martes **1 de diciembre de 2026**. | D.M, P.M, B.B, M.H, J.S |

---

# PLAN DE TRABAJO

| N.° Sem. | Unidad | Contenido / Actividad | Fechas (mar / jue) | Horas sem. |
|---:|:---:|---|---|---:|
| 1 | U1 | Lista de exigencias | 19 y 24 ago. | 8 |
| 2 | U1 | Diseño del sistema — módulo mecánico | 24 y 26 ago. | 8 |
| 3 | U1 | Diseño del sistema — módulo electrónico | 1 y 3 sep. | 8 |
| 4 | U1 | Diseño del sistema — Software | 8 y 10 sep. | 8 |
| 5 | U2 | Introducción a la inteligencia artificial — IA en Python | 15 y 17 sep. | 8 |
| 6 | U2 | Introducción a Internet de las cosas (IoT) | 22 y 24 sep. | 8 |
| 7 | U2 | Introducción a las redes neuronales — Redes neuronales en Python | 29 sep. y 1 oct. | 8 |
| 8 | U2 | **EXAMEN / Presentación de avance del proyecto (documentación)** | 6 y 8 oct. | 8 |
| 9 | U2 | Tiny Machine Learning con Edge Impulse | 13 y 15 oct. | 8 |
| 10 | U3 | TRL 1: Definición e indicadores — Integración de módulos e identificación del TRL | 20 y 22 oct. | 8 |
| 11 | U3 | TRL 2, 3 y 4: Definición e indicadores — Integración de los módulos del sistema | 27 y 29 oct. | 8 |
| 12 | U3 | TRL 5 al 7: Definición e indicadores — Prueba y validación del proyecto | 3 y 5 nov. | 8 |
| 13 | U3 | TRL 8 y 9: Definición e indicadores — Prueba y validación documentada | 10 y 12 nov. | 8 |
| 14 | U4 | Propiedad intelectual: Estado de la técnica — Redacción de solicitud de patente | 17 y 19 nov. | 8 |
| 15 | U4 | Propiedad intelectual: Registro de software — Manual de usuario y memoria descriptiva | 24 y 26 nov. | 8 |
| 16 | U4 | **Revisión de documentos técnicos / PRESENTACIÓN FINAL DEL PROYECTO** | 1 y 3 dic. | 8 |
| 17 | U4 | Cierre de curso — publicación de notas finales | hasta 11 dic. | 0 |

**TOTAL DE HORAS PROGRAMADAS (asistencia G2, sesiones sincrónicas): 128 horas**

---

## BIBLIOGRAFÍA

**[1]** M. A.-M. Khan, S.-H. Kee, A.-S. K. Pathan, and A.-A. Nahid, “Image processing techniques for concrete crack detection: A scientometrics literature review,” *Remote Sensing*, vol. 15, no. 9, p. 2400, 2023. [En línea]. Disponible en:  
https://doi.org/10.3390/rs15092400

**[2]** International Organization for Standardization, “ISO 12100:2010. Safety of machinery — General principles for design — Risk assessment and risk reduction,” ISO, 2010. [En línea]. Disponible en:  
https://www.normsplash.com/Samples/ISO/186791471/ISO-12100-2010-en.pdf

**[3]** International Electrotechnical Commission, “IEC 60529:1989. Degrees of protection provided by enclosures (IP Code),” IEC, 1989. [En línea]. Disponible en:  
https://cdn.standards.iteh.ai/samples/3993/1c9316a803404d25ae2abe512833463b/IEC-60529-1989.pdf

**[4]** Congreso de la República del Perú, “Ley N.° 29783, Ley de Seguridad y Salud en el Trabajo,” 2011. [En línea]. Disponible en:  
https://cdn.www.gob.pe/uploads/document/file/571762/Ley_N__29783.pdf

**[5]** American Concrete Institute, “ACI 224R-01: Control of cracking in concrete structures,” ACI Committee 224, 2001. [En línea]. Disponible en:  
https://www.concrete.org/frequentlyaskedquestions.aspx?faqid=855

**[6]** International Organization for Standardization, “ISO 7250-1:2017. Basic human body measurements for technological design — Part 1: Body measurement definitions and landmarks,” ISO, 2017. [En línea]. Disponible en:  
https://www.iso.org/standard/65246.html

**[7]** International Organization for Standardization, “ISO 21920-1:2021. Geometrical product specifications (GPS) — Surface texture: Profile — Part 1: Indication of surface texture,” ISO, 2021. [En línea]. Disponible en:  
https://www.iso.org/standard/72196.html
