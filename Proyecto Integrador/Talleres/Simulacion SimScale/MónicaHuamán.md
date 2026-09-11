---

## 🧩 Simulación estructural en SimScale

Para evaluar preliminarmente el comportamiento mecánico de la carcasa del dispositivo se realizó una **simulación estructural en SimScale**, considerando el material de fabricación, las condiciones de soporte, la gravedad y las cargas externas que podrían actuar durante el uso del equipo.

<p align="center">
  <a href="https://www.simscale.com/workbench/?pid=8284097056428431416&rru=e442d6d6-7ada-4613-bd25-728ddf262d95&ci=87e7812c-239f-4a9a-83b0-3c45a5200b03&mt=SIMULATION_RESULT&ct=SOLUTION_FIELD">
    <img src="https://img.shields.io/badge/ABRIR_SIMULACIÓN_EN_SIMSCALE-D8D2C8?style=for-the-badge&logoColor=4A4A4A">
  </a>
</p>

### ⚙️ Configuración general

| Parámetro | Valor |
|---|---|
| **Tipo de análisis** | Estático lineal |
| **Material** | PLA |
| **Gravedad** | 9.81 m/s² |
| **Carga de referencia** | 5 N |
| **Dirección principal** | Eje Z negativo |

El material seleccionado para la carcasa fue **PLA (ácido poliláctico)**, debido a que es un material comúnmente utilizado en piezas fabricadas mediante impresión 3D.

También se definieron **condiciones de soporte o enlace** para representar la sujeción de la carcasa y evitar el movimiento libre del modelo durante la simulación.

---

### 🌎 Gravedad aplicada

La gravedad se configuró con una magnitud de:

$$
g = 9.81\;m/s^2
$$

y una dirección:

$$
e_x = 0,\qquad e_y = 0,\qquad e_z = -1
$$

Esto representa la acción de la gravedad en dirección vertical hacia abajo.

<p align="center">
  <img
    src="Recursos/Imágenes/SimScale_Gravedad.png"
    width="760"
    alt="Configuración de gravedad en SimScale"
  />
  <br>
  <em>Figura X. Configuración de la gravedad utilizada en el modelo.</em>
</p>

---

### 📐 Cálculo de la carga por peso de la cámara

La fuerza correspondiente al peso de la cámara se calculó mediante:

$$
F_g = m\cdot g
$$

Considerando una masa aproximada de:

$$
m = 0.51\;kg
$$

se obtiene:

$$
F_g = 0.51(9.81)
$$

$$
\boxed{F_g \approx 5\;N}
$$

Por lo tanto, se consideró una **fuerza aproximada de 5 N en dirección vertical hacia abajo**, representando el peso de la cámara sobre la carcasa.

---

### ⬇️ Fuerza aplicada en SimScale

La fuerza principal se configuró con los siguientes componentes:

$$
F_x = 0\;N
$$

$$
F_y = 0\;N
$$

$$
F_z = -5\;N
$$

El signo negativo indica que la fuerza actúa en dirección descendente sobre el eje Z.

<p align="center">
  <img
    src="Recursos/Imágenes/SimScale_Fuerza_5N.png"
    width="760"
    alt="Fuerza vertical de 5 N aplicada en SimScale"
  />
  <br>
  <em>Figura X. Configuración de la fuerza vertical de 5 N sobre la carcasa.</em>
</p>

---

### ✋ Fuerzas de agarre

Además del peso de la cámara, se aplicaron **tres fuerzas de compresión de referencia de 5 N** en las partes:

- superior,
- inferior,
- posterior de la carcasa.

Estas cargas representan de manera aproximada la presión ejercida por la mano del usuario al sujetar el dispositivo.

Debido a que no se contó con un valor experimental específico de fuerza de agarre, se utilizó **5 N como carga de referencia**, tomando como orden de magnitud el peso aproximado de la cámara.

---

### 🔩 Condiciones de soporte

Se establecieron condiciones de enlace o soporte en zonas específicas del modelo para representar la sujeción de la carcasa durante el análisis.

Estas restricciones permiten evaluar la distribución de esfuerzos y deformaciones generadas por las cargas aplicadas.

---

### 🎯 Objetivo de la simulación

La simulación estructural se realizó con el propósito de:

- evaluar la respuesta de la carcasa frente a cargas externas;
- analizar el comportamiento del PLA;
- representar el peso de la cámara;
- simular de manera aproximada las fuerzas de agarre;
- identificar posibles zonas críticas antes de fabricar el prototipo.

---

### 🖥️ Resultado de la simulación

<p align="center">
  <img
    src="https://github.com/user-attachments/assets/7b723053-41df-443c-b288-24d381e5daf1"
    width="900"
    alt="Resultado de la simulación estructural en SimScale"
  />
  <br>
  <em>Figura X. Resultado del análisis estructural realizado en SimScale.</em>
</p>

> 🧱 **La simulación permite evaluar preliminarmente el comportamiento de la carcasa antes de su fabricación y verificar su respuesta frente al peso de la cámara y las fuerzas externas consideradas.**

---ibución de la tensión de Von Mises, la cual permite identificar las zonas donde se concentran los mayores esfuerzos mecánicos. De acuerdo con los resultados obtenidos, la mayor parte del case presenta tonalidades azules, lo que indica una menor concentración de esfuerzos, mientras que las zonas con colores de mayor intensidad representan regiones donde el esfuerzo es relativamente más elevado. Este análisis permite identificar posibles puntos críticos del diseño y evaluar si la carcasa de PLA presenta un comportamiento estructural adecuado frente a las cargas aplicadas.
