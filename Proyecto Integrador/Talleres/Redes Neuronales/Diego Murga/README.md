# Selección de Red Neuronal Convolucional (CNN)

## Introducción

Dentro de los temas estudiados en redes neuronales, se analizaron tres conceptos principales: Perceptrón, Keras y Red Neuronal Convolucional (CNN). Luego de revisar sus características y aplicaciones, se seleccionó la CNN como el tema más importante para profundizar debido a su relevancia actual dentro del campo del Deep Learning y el procesamiento de imágenes.

Las CNN constituyen una de las arquitecturas más utilizadas en aplicaciones modernas de visión computacional, reconocimiento de objetos, análisis de imágenes médicas, vehículos autónomos y sistemas de inspección automatizada.

---

## ¿Qué es una CNN?

Una Red Neuronal Convolucional (Convolutional Neural Network, CNN) es un tipo de red neuronal diseñada específicamente para procesar imágenes.

Su principal ventaja es la capacidad de aprender automáticamente características visuales relevantes sin necesidad de definir manualmente reglas o patrones.

A medida que la información avanza por la red, las CNN identifican características simples, como bordes y líneas, para posteriormente reconocer patrones más complejos.

<p align="center">
  <img width="902" height="511" alt="image" src="https://github.com/user-attachments/assets/932d2b33-4335-4e57-a3a5-559ee8a39fad" />
</p>


---

## Funciones principales de una CNN

### 1. Convolución

La convolución es la operación más importante dentro de una CNN.

Consiste en aplicar filtros sobre la imagen con el objetivo de detectar características relevantes como:

- Bordes.
- Líneas.
- Texturas.
- Formas.

Cada filtro permite extraer información específica de la imagen y generar mapas de características que serán utilizados en las siguientes etapas de procesamiento.

### Importancia

La convolución permite que la red identifique automáticamente patrones visuales sin necesidad de programar reglas específicas para cada caso.

---

### 2. Función de Activación ReLU

La función ReLU (Rectified Linear Unit) introduce no linealidad dentro de la red neuronal.

Matemáticamente se define como:

$$
ReLU(x)=\max(0,x)
$$

Esta función transforma todos los valores negativos en cero y mantiene los valores positivos.

### Importancia

La función ReLU permite que la red aprenda relaciones complejas entre los datos y acelera significativamente el proceso de entrenamiento.

---

### 3. Pooling

El Pooling es una técnica utilizada para reducir el tamaño de los mapas de características generados por la convolución.

La variante más utilizada es Max Pooling, que conserva únicamente el valor más representativo de cada región analizada.

### Importancia

El Pooling reduce la cantidad de información que debe procesar la red, disminuye el costo computacional y mejora la capacidad de generalización del modelo.

---

### 4. Capas Densas

Las capas densas reciben la información procesada por las etapas anteriores y generan la clasificación final.

Estas capas son responsables de transformar las características extraídas en una predicción concreta.

### Importancia

Permiten convertir la información visual aprendida por la CNN en una respuesta útil para el usuario.

---

## Gráfica de pérdida

<p align=center>
  <img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/30062344-e307-4618-a128-7d336a960c80" />
</p>

Esta gráfica permite ver si la CNN está aprendiendo. Si el *Loss* va disminuyendo conforme avanzan las épocas, significa que el modelo está reduciendo su error en el entrenamiento.

## Gráfica de Accuracy y ROC-AUC

<p align=center>
  <img width="863" height="395" alt="image" src="https://github.com/user-attachments/assets/e6ee35df-cc7e-4bb5-a748-be7b07051153" />
</p>

Esta graficas muestra que tan bien funciona el modelo con los datos de validacion.

- Accuracy: Que proporción de predicciones fueron correctas.
- ROC-AUC: Mide qué tan bien el modelo distingue entre las clases.

## Matriz de confusión

<p align=center>
  <img width="364" height="346" alt="image" src="https://github.com/user-attachments/assets/93a898f7-27e2-4ebf-ad52-b251343d1ccf" />
</p>

Esta gráfica te permite ver cuántas imágenes clasificó correctamente la CNN y cuántas clasificó incorrectamente, separando los resultados entre las dos clases.

## Grad-CAM

<p align=center>
  <img width="990" height="356" alt="image" src="https://github.com/user-attachments/assets/68ac3025-5fbe-401c-aab0-667a3dc20b25" />
</p>

El código produce algo parecido a:
Imagen original → Grad-CAM → Superposición
Y permite responder:
¿En qué parte de la imagen se fijó principalmente la ResNet para hacer su predicción?

Es útil porque no solo sabes qué clase predijo el modelo, sino también qué zonas de la imagen influyeron en esa predicción.
