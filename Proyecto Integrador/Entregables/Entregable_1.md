# **1\. Lista de Exigencias** 

**Tabla 1: Lista de Exigencias**

| LISTA DE EXIGENCIAS |  |  | Páginas: 4 |
| ----- | :---: | ----- | ----- |
|  |  |  | **Edición: Rev. 2** |
| **PROYECTO:** |  | **Sistema inteligente portátil para monitoreo y clasificación del riesgo asociado a grietas en viviendas de concreto** | **Fecha: 23/08/2026** |
|  |  |  | **Revisado:** |
| **CLIENTE:**  |  | **UNIVERSIDAD PERUANA CAYETANO HEREDIA** | **Elaborado: D.M, P.M, B.B, M.H, J.S** |
| Fecha (cambios) | Deseo o Exigencia | **Descripción** | **Responsable** |
| **21/08/26** | E | **Función Principal:**  Detectar y registrar grietas en estructuras de concreto mediante análisis de imágenes  , incorporando información de ubicación geográfica  para generar una evaluación preliminar y facilitar la priorización de inspecciones técnicas **\[1\]**.  | D.M ,  J.S |
| **23/08/26** | E | **Geometría:** El dispositivo deberá contar con dimensiones reducidas que permitan su transporte y utilización durante inspecciones de viviendas. La estructura deberá permitir incorporar sensores, cámara, sistema de procesamiento y elementos de visualización sin dificultar su manipulación.  | M.H |
| **23/08/26** | E | **Cinemática:** El sistema deberá permitir el posicionamiento y desplazamiento de la cámara sobre diferentes zonas de la superficie de concreto. Durante la captura de imágenes se deberá mantener una posición estable para evitar movimientos que generen imágenes borrosas o alteren los resultados del análisis.  | J.S |
| **23/08/26** | E | **Fuerzas**: El dispositivo no deberá ejercer fuerzas significativas sobre la superficie inspeccionada que puedan modificar o ampliar las grietas. Los elementos de contacto deberán utilizarse únicamente para posicionamiento o referencia de medición.   | J.S |
| **23/08/26** | E | **Energía:** El sistema deberá utilizar una fuente de alimentación portátil y de baja tensión adecuada para el funcionamiento del ESP32, sensores, cámara y demás componentes electrónicos. . Se priorizará un bajo consumo energético para permitir varias inspecciones antes de recargar el dispositivo   | D.M, P.M |
| **23/08/26** | E | **Materia:** No se requiere flujo de materia durante la operación del sistema, debido a que la inspección se realiza de manera no destructiva sobre la superficie de concreto.     | M.H |
| **23/08/26** | E | **Señales (Información):** El sistema deberá disponer de señales de entrada y salida necesarias para la adquisición, procesamiento, evaluación y comunicación de información durante la inspección. Señales de entrada: activación e inicio de la inspección, imagen de la grieta, datos provenientes de los sensores, coordenadas geográficas y selección o confirmación del punto de evaluación. Señales de salida: características de la grieta, información geográfica relevante, resultado de la evaluación preliminar, recomendación o priorización de inspección y, cuando corresponda, señal de alerta.  | D.M, P.M |
| **23/08/26** | E | **Control:** El sistema deberá controlar la adquisición periódica de datos, procesamiento de las imágenes y señales, la integración de la información obtenida y la generación del resultado de la evaluación preliminar.    | D.M, P.M |
| **23/08/26** | E | **Electrónico (hardware):** Se utilizará un controlador adecuado para la adquisición y procesamiento de información. El sistema integrará una cámara para registrar y analizar las grietas, un módulo GPS para obtener la ubicación de la inspección y los sensores o elementos de medición necesarios para obtener características físicas complementarias de la grieta, de acuerdo con la solución técnica seleccionada.  | D.M, P.M |
| **23/08/26** | E | **Software:** El software deberá permitir el procesamiento y análisis de las imágenes de las grietas, la integración de las coordenadas geográficas, la consulta de información geográfica proveniente de fuentes oficiales sobre las características del suelo y/o condiciones de peligro o susceptibilidad del entorno, y la generación de una evaluación preliminar. También, deberá permitir la visualización de los resultados mediante una interfaz adecuada y admitir futuras modificaciones o ampliaciones.  | D.M, P.M |
| **23/08/26** | E | **Comunicaciones:** La unidad de procesamiento deberá comunicarse con la cámara y los demás componentes mediante conexión inalámbrica. Asimismo, deberá permitir transmitir los resultados hacia la plataforma de almacenamiento o visualización.       | D.M, p.M |
| **23/08/26** | E | **Seguridad:** El sistema deberá garantizar una operación segura para el usuario y proteger sus componentes eléctricos y electrónicos. Durante el diseño se tomará como referencia la ISO 12100 para identificar peligros, estimar y evaluar los riesgos, y establecer medidas para eliminarlos o reducirlos **\[2\]**. Asimismo, se considerará la IEC 60529 para seleccionar la protección de la carcasa frente al ingreso de polvo y agua **\[3\]** y la Ley N.° 29783 de Seguridad y Salud en el Trabajo **\[4\]**. | B.B |
| **23/08/26** | E | **Ergonomía**: El dispositivo deberá ser portátil, ligero y sencillo de manipular. Los elementos de captura y control deberán ubicarse de manera que permitan realizar una inspección sin adoptar posiciones incómodas durante períodos prolongados que comprometan la salud y en conformidad con la norma ISO 7250 (Basic human body measurements for technological design)**\[5\].**   | M.H |
| **23/08/26** | E | **Fabricación:** El sistema deberá fabricarse con materiales disponibles en el mercado nacional, permitiendo el fácil reemplazo de componentes electrónicos. Se considerarán componentes nacionales o importados con tiempos de adquisición de 5 a 15 días. La carcasa y soporte deberán ser resistentes y proteger los componentes frente al polvo y humedad, tomando como referencia la IEC 60529\. Asimismo, las piezas deberán presentar un acabado superficial adecuado según la  ISO 21920-1 **\[6\].**  | B.B |
| **23/08/26** | E | **Control de calidad:** El diseño y fabricación del sistema deberá cumplir con las exigencias establecidas, considerando dimensiones, materiales, seguridad y funcionamiento. La detección y medición de grietas se validará mediante comparación con mediciones de referencia, evaluando la precisión, error y repetibilidad del sistema.  | J.S |
| **23/08/26** | E | **Montaje:** El sistema tendrá un diseño portátil y de fácil montaje, permitiendo posicionar temporalmente frente a la superficie de concreto. Sus componentes deberán mantenerse firmes durante la inspección y permitir un rápido ensamblaje y desmontaje para facilitar su transporte y mantenimiento.  | M.H |
| **23/08/26** | D | **Transporte:** El sistema deberá ser portátil y permitir su traslado manual. Como meta de diseño, el equipo completo deberá mantenerse por debajo de aproximadamente 3 kg y sus componentes deberán permanecer protegidos mediante una carcasa durante su transporte.  | P.M |
| **23/08/26** | D | **Uso:** El sistema estará diseñado inicialmente para trabajar principalmente en superficies de concreto accesibles y bajo condiciones controladas o semicontroladas de iluminación. La iluminación deberá mantenerse lo más uniforme posible durante la captura para reducir sombras, reflejos y cambios de contraste que puedan ser interpretados erróneamente como grietas. El sistema será una herramienta de apoyo a la inspección y no reemplazará la evaluación realizada por un profesional especializado.  | M.H |
| **23/08/26** | E | **Mantenimiento: Componentes mecánicos:** Deberán permitir un fácil acceso para su inspección, limpieza, ajuste, reparación o reemplazo. **Componentes electrónicos:** La cámara, controlador y demás componentes deberán permitir su calibración, inspección y reemplazo individual en caso de falla.  | J.S |
| **23/08/26** | D | **Costos:** Se priorizará el uso de materiales y componentes de bajo costo y fácil adquisición. Se estima que el costo de materiales del prototipo no deberá superar los S/ 400, considerando la cámara, controlador, sistema de alimentación, carcasa, soporte y componentes electrónicos necesarios.  | B.B |
| **23/08/26** | E | **Plazos:**  El proyecto empezará el martes 18 de agosto y espera su finalización el martes 1 de diciembre.  | D.M, P.M  |

| N°Sem. | Unidad | Contenido/Actividad | FECHAS (mar / jue) | SEMANAS 2026-I |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | HORAS SEM. |
| :---: | :---: | :---: | :---: | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | :---: |
|  |  |  |  | AGO |  | SEP |  |  |  |  | OCT |  |  |  | NOV |  |  |  | DIC |  |  |
|  |  |  |  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 |  |
| 1 | U1 | Lista de exigencias | 19 y 24 ago. | X |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 2 | U1 | Diseño del sistema — módulo mecánico | 24 y 26 ago. |  | X |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 3 | U1 | Diseño del sistema — módulo electrónico | 1 y 3 sep. |  |  | X |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 4 | U1 | Diseño del sistema — Software | 8 y 10 sep. |  |  |  | X |  |  |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 5 | U2 | Introducción a la inteligencia artificial — IA en Python | 15 y 17 sep. |  |  |  |  | X |  |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 6 | U2 | Introducción a Internet de las cosas (IoT) | 22 y 24 sep. |  |  |  |  |  | X |  |  |  |  |  |  |  |  |  |  |  | 8 |
| 7 | U2 | Introducción a las redes neuronales — Redes neuronales en Python | 29 sep. y 1 oct. |  |  |  |  |  |  | X |  |  |  |  |  |  |  |  |  |  | 8 |
| 8 | U2 | **EXAMEN / Presentación de avance del proyecto (documentación)** | 6 y 8 oct. |  |  |  |  |  |  |  | X |  |  |  |  |  |  |  |  |  | 8 |
| 9 | U2 | Tiny Machine Learning con Edge Impulse | 13 y 15 oct. |  |  |  |  |  |  |  |  | X |  |  |  |  |  |  |  |  | 8 |
| 10 | U3 | TRL 1: Definición e indicadores — Integración de módulos e identificación del TRL | 20 y 22 oct. |  |  |  |  |  |  |  |  |  | X |  |  |  |  |  |  |  | 8 |
| 11 | U3 | TRL 2, 3 y 4: Definición e indicadores — Integración de los módulos del sistema | 27 y 29 oct. |  |  |  |  |  |  |  |  |  |  | X |  |  |  |  |  |  | 8 |
| 12 | U3 | TRL 5 al 7: Definición e indicadores — Prueba y validación del proyecto | 3 y 5 nov. |  |  |  |  |  |  |  |  |  |  |  | X |  |  |  |  |  | 8 |
| 13 | U3 | TRL 8 y 9: Definición e indicadores — Prueba y validación documentada | 10 y 12 nov. |  |  |  |  |  |  |  |  |  |  |  |  | X |  |  |  |  | 8 |
| 14 | U4 | Propiedad intelectual: Estado de la técnica — Redacción de solicitud de patente | 17 y 19 nov. |  |  |  |  |  |  |  |  |  |  |  |  |  | X |  |  |  | 8 |
| 15 | U4 | Propiedad intelectual: Registro de software — Manual de usuario y memoria descriptiva | 24 y 26 nov. |  |  |  |  |  |  |  |  |  |  |  |  |  |  | X |  |  | 8 |
| 16 | U4 | **Revisión de documentos técnicos / PRESENTACIÓN FINAL DEL PROYECTO** | 1 dic. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | X |  | 8 |
| 17 | U4 | Cierre de curso — publicación de notas finales | hasta 11 dic. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | X | 0 |
| TOTAL DE HORAS PROGRAMADAS (asistencia G2, sesiones sincrónicas) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 128 |

**BIBLIOGRAFÍA**

**\[1\]  M. A.-M. Khan, S.-H. Kee, A.-S. K. Pathan, and A.-A. Nahid, “Image processing techniques for concrete crack detection: A scientometrics literature review,” *Remote Sensing*, vol. 15, no. 9, p. 2400, 2023\. \[En línea\]. Disponible en: [https://doi.org/10.3390/rs15092400](https://doi.org/10.3390/rs15092400)**

**\[2\] International Organization for Standardization, “ISO 12100:2010. Safety of machinery — General principles for design — Risk assessment and risk reduction,” ISO, 2010\. \[En línea\]. Disponible en: [https://www.normsplash.com/Samples/ISO/186791471/ISO-12100-2010-en.pdf](https://www.normsplash.com/Samples/ISO/186791471/ISO-12100-2010-en.pdf)**

**\[3\] International Electrotechnical Commission, “IEC 60529:1989. Degrees of protection provided by enclosures (IP Code),” IEC, 1989\. \[En línea\]. Disponible en: [https://cdn.standards.iteh.ai/samples/3993/1c9316a803404d25ae2abe512833463b/IEC-60529-1989.pdf](https://cdn.standards.iteh.ai/samples/3993/1c9316a803404d25ae2abe512833463b/IEC-60529-1989.pdf)**

**\[4\] Congreso de la República del Perú, “Ley N.° 29783, Ley de Seguridad y Salud en el Trabajo,” 2011\. \[En línea\]. Disponible en: [https://cdn.www.gob.pe/uploads/document/file/571762/Ley\_N\_\_29783.pdf](https://cdn.www.gob.pe/uploads/document/file/571762/Ley_N__29783.pdf)**

**\[5\] International Organization for Standardization, “ISO 7250-1:2017. Basic human body measurements for technological design — Part 1: Body measurement definitions and landmarks,” ISO, 2017\. \[En línea\]. Disponible en: [ISO 7250-1:2017 — ISO](https://www.iso.org/standard/65246.html?utm_source=chatgpt.com)**

**\[6\] International Organization for Standardization, “ISO 21920-1:2021. Geometrical product specifications (GPS) — Surface texture: Profile — Part 1: Indication of surface texture,” ISO, 2021\. \[En línea\]. Disponible en: [ISO 21920-1:2021 — ISO](https://www.iso.org/standard/72196.html?utm_source=chatgpt.com)**
