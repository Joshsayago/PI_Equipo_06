<div align="center">
  <h2>⚙️ Simulación estructural de la carcasa</h2>
  <p><b>Evaluación de esfuerzos en los puntos de fijación mediante SimScale</b></p>
</div>

### 📌 Justificación de la simulación

Se realizó una simulación estructural estática en **SimScale** para evaluar el comportamiento de la carcasa fabricada en **PLA**. El análisis se concentró en los cuatro puntos destinados a los tornillos, debido a que estas zonas permiten mantener unidas las partes del dispositivo y pueden presentar concentración de esfuerzos.

<div align="center">

<h3>📊 Parámetros de la simulación</h3>

<table>
  <thead>
    <tr>
      <th align="center">Parámetro</th>
      <th align="center">Configuración</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><b>Tipo de análisis</b></td>
      <td align="center">Estático estructural</td>
    </tr>
    <tr>
      <td><b>Material de la carcasa</b></td>
      <td align="center">PLA</td>
    </tr>
    <tr>
      <td><b>Carga total aplicada</b></td>
      <td align="center">5 N</td>
    </tr>
    <tr>
      <td><b>Número de puntos de fijación</b></td>
      <td align="center">4</td>
    </tr>
    <tr>
      <td><b>Fuerza aplicada por punto</b></td>
      <td align="center">1,25 N</td>
    </tr>
    <tr>
      <td><b>Dirección de las fuerzas</b></td>
      <td align="center">Eje Z negativo</td>
    </tr>
    <tr>
      <td><b>Gravedad</b></td>
      <td align="center">9,81 m/s²</td>
    </tr>
    <tr>
      <td><b>Dirección de la gravedad</b></td>
      <td align="center">(0, 0, −1)</td>
    </tr>
    <tr>
      <td><b>Tipo de malla</b></td>
      <td align="center">Estándar</td>
    </tr>
    <tr>
      <td><b>Nivel de finura</b></td>
      <td align="center">4</td>
    </tr>
    <tr>
      <td><b>Resultado evaluado</b></td>
      <td align="center">Esfuerzo de Von Mises</td>
    </tr>
    <tr>
      <td><b>Esfuerzo máximo</b></td>
      <td align="center">17,28 kPa</td>
    </tr>
  </tbody>
</table>

</div>

### 🧱 Material seleccionado

La carcasa fue configurada con **PLA**, debido a que este material será empleado para fabricar el prototipo mediante impresión 3D. El material se asignó a toda la geometría de la carcasa antes de ejecutar la simulación.

### 🌎 Gravedad y dirección

Se configuró una aceleración gravitacional de **9,81 m/s²** en dirección negativa del eje **Z**. Esta condición representa la acción del peso propio de la carcasa de PLA.

<div align="center">
  <p><b>Magnitud de la gravedad: 9,81 m/s²</b></p>
  <p><b>Dirección: (0, 0, −1), correspondiente al eje Z negativo</b></p>
</div>

### 🧮 Justificación de la fuerza aplicada

Se consideró una carga total de **5 N**, correspondiente al peso estimado de los componentes internos del dispositivo. Esta fuerza equivale aproximadamente al peso generado por una masa de **0,51 kg**.

<div align="center">
  <p><b>Masa estimada = 5 N ÷ 9,81 m/s² = 0,51 kg</b></p>
</div>

Para simplificar el análisis, se asumió que esta carga se distribuye uniformemente entre los cuatro puntos de fijación:

<div align="center">
  <h3>F<sub>tornillo</sub> = F<sub>total</sub> ÷ número de fijaciones</h3>
  <h3>F<sub>tornillo</sub> = 5 N ÷ 4 = 1,25 N</h3>
</div>

Por ello, se aplicó una fuerza de **1,25 N en dirección Z negativa** sobre cada uno de los cuatro puntos de fijación. Esto permitió evaluar la distribución de los esfuerzos alrededor de las uniones y detectar posibles zonas críticas antes de fabricar el prototipo.

> **Nota:** La distribución uniforme representa una condición simplificada en la que los cuatro tornillos soportan la carga de los componentes internos de manera equivalente.

<div align="center">

<h3>📷 Evidencia de la configuración</h3>

<table>
  <tr>
    <td align="center" width="50%">
      <img width="520" alt="Configuración de la gravedad en SimScale" src="https://github.com/user-attachments/assets/5f58e946-a1f8-44b4-9ef1-1fa7cd210e8b">
      <br>
      <b>Figura 1. Configuración de la gravedad</b>
      <br>
      <sub>Magnitud de 9,81 m/s² en dirección Z negativa.</sub>
    </td>
    <td align="center" width="50%">
      <img width="520" alt="Configuración de la fuerza en SimScale" src="https://github.com/user-attachments/assets/49e414aa-a56e-447b-8ba3-b8a4b3efa51e">
      <br>
      <b>Figura 2. Configuración de la fuerza</b>
      <br>
      <sub>Fuerza de 1,25 N aplicada en dirección Z negativa.</sub>
    </td>
  </tr>
</table>

</div>

### 🕸️ Configuración del mallado

Para el análisis se utilizó una **malla estándar con nivel de finura 4**. Esta configuración permitió representar adecuadamente la distribución de los esfuerzos sin incrementar excesivamente el costo computacional de la simulación.

### 🖥️ Resultado de la simulación

<p align="center">
  <img width="900" alt="Distribución del esfuerzo de Von Mises en la carcasa de PLA" src="https://github.com/user-attachments/assets/f5feb575-7787-461a-ab25-1dcff4d52c7a">
</p>

<p align="center">
  <i>Figura 3. Distribución del esfuerzo de Von Mises en la carcasa de PLA.</i>
</p>

### 🔍 Interpretación de los resultados

La simulación mostró un esfuerzo máximo de Von Mises de **17,28 kPa**, equivalente a **0,01728 MPa**.

La mayor parte de la carcasa presenta tonalidades azules, asociadas con los niveles más bajos de esfuerzo de la escala. Los valores aumentan alrededor de los cuatro puntos de fijación, donde se observan tonalidades celestes y verdes.

La concentración más notoria se presenta cerca del punto de fijación inferior izquierdo. Este comportamiento se relaciona con la presencia de los orificios, los cambios en la geometría y la aplicación localizada de las cargas.

No se observa una concentración elevada extendida sobre toda la carcasa. Por lo tanto, bajo las condiciones establecidas en la simulación, la carga total de **5 N** produce esfuerzos principalmente localizados alrededor de las uniones.

> ⚠️ **Alcance de la simulación:** Los resultados corresponden únicamente al material, las cargas, la gravedad, las condiciones de fijación y el mallado definidos en el modelo. Esta simulación constituye una evaluación preliminar y no reemplaza las pruebas mecánicas realizadas sobre el prototipo físico.

<div align="center">
  <h3>🔗 Acceso a la simulación</h3>

  <a href="https://www.simscale.com/workbench/?pid=7146214850117818288&mi=spec:72e2d9ef-0303-4a14-8f8f-3f46c65aeeb1%2Cservice:SIMULATION%2Cstrategy:1">
    <b>🌐 Ver simulación completa en SimScale</b>
  </a>
</div>
