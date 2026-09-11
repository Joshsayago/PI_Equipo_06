
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

El material seleccionado para la carcasa fue **PLA (ácido poliláctico)**, debido a que es un material comúnmente utilizado en la fabricación de piezas mediante impresión 3D.

También se definieron **condiciones de soporte o enlace** para representar la sujeción de la carcasa durante el análisis.

---

### 🌎 Configuración de la gravedad

La gravedad se configuró con una magnitud de:

$$
g = 9.81\;m/s^2
$$

y una dirección:

$$
e_x = 0,\qquad e_y = 0,\qquad e_z = -1
$$

Esto representa la acción de la gravedad en dirección vertical hacia abajo sobre el modelo.

<p align="center">
  <img
    src="https://github.com/user-attachments/assets/1f9d815d-a40e-4bc8-9fe6-cc08c922c40f"
    width="820"
    alt="Configuración de gravedad en SimScale"
  />
  <br>
  <em>Figura X. Configuración de la gravedad del modelo en SimScale.</em>
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

### ⬇️ Aplicación de la fuerza

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
    src="https://github.com/user-attachments/assets/ca10ce8e-51a1-4a6e-96f0-894562d1273d"
    width="820"
    alt="Fuerza vertical de 5 N aplicada en SimScale"
  />
  <br>
  <em>Figura X. Aplicación de una fuerza vertical de 5 N sobre la carcasa.</em>
</p>

---

### ✋ Fuerzas de agarre

Además de la carga asociada al peso de la cámara, se aplicaron **tres fuerzas de compresión de referencia de 5 N** en las partes:

- superior,
- inferior,
- posterior de la carcasa.

Estas cargas representan de manera aproximada la presión ejercida por la mano del usuario al sujetar el dispositivo.

Debido a que no se contó con un valor experimental específico de fuerza de agarre, se utilizó **5 N como carga de referencia**, tomando como orden de magnitud el peso aproximado de la cámara.

---

### 🔩 Condiciones de soporte

Se establecieron condiciones de enlace o soporte en zonas específicas del modelo para representar la sujeción de la carcasa durante la simulación.

Estas restricciones permiten evaluar la distribución de esfuerzos y deformaciones producidas por las cargas aplicadas.

---

### 🎯 Objetivo de la simulación

La simulación estructural se realizó con el propósito de:

- evaluar la respuesta de la carcasa frente a cargas externas;
- analizar el comportamiento del PLA;
- representar el peso de la cámara;
- simular de manera aproximada las fuerzas de agarre;
- identificar posibles zonas críticas antes de fabricar el prototipo.

> 🧱 **La simulación permite evaluar preliminarmente el comportamiento de la carcasa antes de su fabricación y verificar su respuesta frente al peso de la cámara y las fuerzas externas consideradas.**

---

