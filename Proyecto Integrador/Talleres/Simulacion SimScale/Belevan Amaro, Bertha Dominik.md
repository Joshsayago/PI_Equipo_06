<div align="center">
  <h2>⚙️ Simulación estructural de la carcasa</h2>
  <p><b>Evaluación de los esfuerzos generados en los puntos de fijación mediante SimScale</b></p>
</div>

### 📌 Justificación de la simulación

Se realizó una simulación estructural estática en **SimScale** para evaluar el comportamiento de la carcasa fabricada en **PLA**. El análisis se concentró en los cuatro puntos de fijación destinados a los tornillos, debido a que estas zonas mantienen unidas las partes del dispositivo y pueden presentar concentración de esfuerzos.

<div align="center">

### 📊 Parámetros de la simulación

<table>
  <thead>
    <tr>
      <th align="center">Parámetro</th>
      <th align="center">Configuración</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><b>Tipo de análisis</b></td><td align="center">Estático estructural</td></tr>
    <tr><td><b>Material de la carcasa</b></td><td align="center">PLA</td></tr>
    <tr><td><b>Carga total aplicada</b></td><td align="center">5 N</td></tr>
    <tr><td><b>Puntos de fijación</b></td><td align="center">4</td></tr>
    <tr><td><b>Fuerza por punto</b></td><td align="center">1,25 N</td></tr>
    <tr><td><b>Dirección de la fuerza</b></td><td align="center">Eje Z negativo</td></tr>
    <tr><td><b>Gravedad</b></td><td align="center">9,81 m/s²</td></tr>
    <tr><td><b>Dirección de la gravedad</b></td><td align="center">Eje Z negativo</td></tr>
    <tr><td><b>Tipo de malla</b></td><td align="center">Estándar</td></tr>
    <tr><td><b>Nivel de finura</b></td><td align="center">4</td></tr>
    <tr><td><b>Resultado evaluado</b></td><td align="center">Esfuerzo de Von Mises</td></tr>
    <tr><td><b>Esfuerzo máximo</b></td><td align="center">17,28 kPa</td></tr>
  </tbody>
</table>

</div>

### 🧱 Material seleccionado

La carcasa fue configurada con **PLA**, debido a que este material será empleado para fabricar el prototipo mediante impresión 3D. El material se asignó a toda la geometría de la carcasa antes de ejecutar la simulación.

### 🌎 Gravedad y dirección

Se consideró una aceleración gravitacional de **9,81 m/s²**, aplicada en la dirección negativa del eje **Z**. Esta configuración representa la acción del peso propio de la carcasa de PLA.

<div align="center">
  <p><b>Vector de gravedad: (0, 0, −9,81) m/s²</b></p>
</div>

Además, las fuerzas correspondientes a la carga de los componentes internos se aplicaron en la misma dirección, es decir, hacia el eje **Z negativo**.

### 🧮 Justificación de la fuerza aplicada

Se consideró una carga total de **5 N**, correspondiente al peso estimado de los componentes internos del dispositivo. Esta fuerza equivale aproximadamente al peso generado por una masa de **0,51 kg**.

<div align="center">
  <p><b>Masa estimada = 5 N ÷ 9,81 m/s² = 0,51 kg</b></p>
</div>

Para simplificar el análisis, se asumió que la carga total se distribuye uniformemente entre los cuatro puntos de fijación:

<div align="center">
  <h3>F<sub>tornillo</sub> = F<sub>total</sub> ÷ número de fijaciones</h3>
  <h3>F<sub>tornillo</sub> = 5 N ÷ 4 = 1,25 N</h3>
</div>

Por ello, se aplicó una fuerza de **1,25 N en dirección Z negativa** sobre cada uno de los cuatro puntos de fijación. Esto permitió analizar la distribución de los esfuerzos alrededor de los tornillos y detectar posibles zonas críticas antes de fabricar el prototipo.

> **Nota:** La distribución uniforme representa una condición simplificada en la que los cuatro tornillos soportan la carga de los componentes internos de manera equivalente.

### 🕸️ Configuración del mallado

Para el análisis se utilizó una **malla estándar con nivel de finura 4**. Esta configuración permitió representar la distribución de los esfuerzos en la carcasa sin incrementar excesivamente el costo computacional de la simulación.

### 🖥️ Resultado de la simulación

<p align="center">
  <img width="900" alt="Distribución del esfuerzo de Von Mises en la carcasa de PLA" src="https://github.com/user-attachments/assets/ad2d2dd1-c7f3-4213-a9d4-4e2ad5225659">
</p>

<p align="center">
  <i>Figura 1. Distribución del esfuerzo de Von Mises en la carcasa de PLA.</i>
</p>
<div align="center">

### 🔗 Acceso a la simulación

<a href="https://www.simscale.com/workbench/?pid=7146214850117818288&mi=spec:72e2d9ef-0303-4a14-8f8f-3f46c65aeeb1%2Cservice:SIMULATION%2Cstrategy:1">
  <b>🌐 Ver simulación completa en SimScale</b>
</a>

</div>

### 🔍 Interpretación de los resultados

La simulación mostró un esfuerzo máximo de Von Mises de aproximadamente **17,28 kPa**, equivalente a **0,01728 MPa**.

La mayor parte de la carcasa presenta tonalidades azules, las cuales representan niveles bajos de esfuerzo. Los incrementos se concentran principalmente alrededor de los puntos de fijación y sus zonas cercanas, debido a que allí se aplicaron las cargas y restricciones del modelo.

Bajo las condiciones simuladas, no se observa una zona crítica evidente frente a la carga total de **5 N**. Por lo tanto, el diseño presenta un comportamiento adecuado para esta condición preliminar de carga.

> ⚠️ **Alcance de la simulación:** Los resultados corresponden únicamente al material, las cargas, la dirección de la gravedad, las condiciones de fijación y el mallado establecidos en el modelo. Esta simulación preliminar no reemplaza las pruebas mecánicas realizadas sobre el prototipo físico.
