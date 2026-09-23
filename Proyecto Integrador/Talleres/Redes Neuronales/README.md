# Informe: Uso de CNN en el proyecto Crack Scan

## 1. Introducción

El proyecto **Crack Scan** tiene como objetivo desarrollar un sistema capaz de identificar grietas en superficies a partir de imágenes. Para realizar esta tarea se utilizará una **Red Neuronal Convolucional (CNN)**, debido a que este tipo de modelo está diseñado especialmente para trabajar con imágenes y aprender automáticamente características visuales.

El sistema recibirá una imagen de una superficie, procesará sus características y determinará si presenta una grieta. Dependiendo del alcance final del proyecto, también podría localizar la zona donde se encuentra la grieta.

---

## 2. ¿Qué CNN utilizaría?

Para Crack Scan utilizaría **transfer learning con MobileNetV2 o EfficientNetB0**, en lugar de construir una CNN completamente desde cero.

Para un proyecto académico, una opción práctica sería **MobileNetV2**.

### ¿Por qué MobileNetV2?

MobileNetV2 es una arquitectura CNN relativamente ligera que permite obtener buenos resultados sin requerir un modelo excesivamente pesado.

Sus principales ventajas para Crack Scan serían:

- Tiene un tamaño relativamente reducido.
- Requiere menos recursos computacionales que modelos más grandes.
- Permite utilizar **transfer learning**.
- Puede adaptarse a un problema de clasificación de imágenes.
- Es adecuada si posteriormente se quisiera llevar el sistema a una aplicación web o dispositivo con recursos limitados.

La arquitectura se utilizaría inicialmente con los pesos obtenidos mediante entrenamiento previo y posteriormente se adaptaría al problema específico de detección de grietas.

---

# 3. ¿Por qué utilizar una CNN?

Las imágenes contienen una gran cantidad de información: píxeles, bordes, texturas, formas, contrastes, etc.

Una CNN permite aprender automáticamente cuáles de estas características son importantes para identificar una grieta.

Por ejemplo, durante el entrenamiento la red puede aprender progresivamente:

```text
Imagen
   ↓
Bordes
   ↓
Líneas y patrones
   ↓
Texturas
   ↓
Patrones similares a grietas
   ↓
Clasificación
   ↓
Grieta / No grieta
```

Esto evita tener que programar manualmente reglas como:

> "Si existe una línea oscura con determinada longitud, entonces existe una grieta".

La CNN aprende estos patrones a partir de los ejemplos proporcionados durante el entrenamiento.

---

# 4. Funcionamiento propuesto de Crack Scan

El flujo general del sistema sería:

```text
                  CRACK SCAN

              Imagen de entrada
                     ↓
             Preprocesamiento
                     ↓
              MobileNetV2
           (modelo preentrenado)
                     ↓
             Extracción de
               características
                     ↓
              Capa clasificadora
                     ↓
             ┌───────────────┐
             │               │
          GRIETA          NO GRIETA
```

Por ejemplo:

**Entrada:**

```text
Fotografía de una pared
```

**Salida:**

```text
Predicción: GRIETA
Probabilidad: 94.7 %
```

---

# 5. Funciones principales que utilizaría

El proyecto puede dividirse en varias funciones para mantener organizado el código.

## 5.1. Carga de imágenes

Esta función tendría como objetivo cargar las imágenes del conjunto de datos.

```python
def cargar_datos():
    ...
```

Su función sería:

- Leer las imágenes.
- Identificar sus etiquetas.
- Separarlas en entrenamiento, validación y prueba.

Por ejemplo:

```text
Dataset
   │
   ├── train
   ├── validation
   └── test
```

---

## 5.2. Preprocesamiento

Las imágenes deben tener un formato adecuado para ingresar a la CNN.

```python
def preprocesar_imagen(imagen):
    ...
```

Esta función podría realizar:

- Redimensionamiento.
- Normalización de valores de píxeles.
- Conversión al formato esperado por MobileNetV2.

Por ejemplo, si las imágenes originales tienen diferentes tamaños, podrían convertirse a:

```text
224 × 224 píxeles
```

para utilizarse como entrada del modelo.

---

# 6. Aumento de datos

Una función importante sería utilizar **Data Augmentation**.

```python
def aumentar_datos():
    ...
```

Esto permite generar variaciones de las imágenes de entrenamiento mediante transformaciones como:

- Rotación.
- Volteo horizontal.
- Zoom.
- Desplazamiento.
- Variación de contraste.

Por ejemplo:

```text
Imagen original
      ↓
 ┌────┼────┐
 ↓    ↓    ↓
rotada zoom volteada
```

Esto ayuda a que el modelo no dependa de una posición o apariencia demasiado específica de la grieta.

---

# 7. Construcción del modelo

Se utilizaría MobileNetV2 como extractor de características.

Conceptualmente:

```python
base_model = MobileNetV2(
    weights="imagenet",
    include_top=False
)
```

Luego se agregaría una parte específica para Crack Scan:

```text
MobileNetV2
     ↓
Global Average Pooling
     ↓
Dropout
     ↓
Dense
     ↓
Salida
```

Para un problema binario:

```text
0 → No grieta
1 → Grieta
```

La última capa podría utilizar una activación **sigmoid**, que produciría un valor entre 0 y 1.

Ejemplo:

```text
0.03 → No grieta
0.94 → Grieta
```

---

# 8. Entrenamiento

El modelo se entrenaría utilizando las imágenes etiquetadas.

```python
history = model.fit(
    train_data,
    validation_data=val_data,
    epochs=...
)
```

Durante cada época, el modelo intenta reducir su error.

Se pueden almacenar métricas como:

- `loss`
- `accuracy`
- `val_loss`
- `val_accuracy`
- `AUC`

Esto permite observar cómo evoluciona el aprendizaje.

---

# 9. Evaluación del modelo

Una vez terminado el entrenamiento, el modelo debe evaluarse utilizando imágenes que **no haya utilizado durante el entrenamiento**.

Esto es importante porque no interesa solamente que la CNN memorice las imágenes, sino que pueda reconocer grietas en imágenes nuevas.

Las principales métricas serían:

### Accuracy

Indica qué proporción de las predicciones fueron correctas.

```text
Accuracy = predicciones correctas / predicciones totales
```

---

### Precision

Permite analizar qué proporción de las imágenes clasificadas como grieta realmente eran grietas.

Es especialmente útil para conocer la cantidad de **falsos positivos**.

---

### Recall

Indica qué proporción de las grietas existentes fueron detectadas por el modelo.

Para Crack Scan esta métrica es especialmente importante, porque un sistema que no detecta una grieta existente genera un **falso negativo**.

---

### F1-Score

Combina precision y recall en una sola métrica.

---

### ROC-AUC

Permite evaluar la capacidad del modelo para diferenciar entre:

```text
Grieta
vs.
No grieta
```

sin depender de un único umbral de clasificación.

---

# 10. Matriz de confusión

También utilizaría una **matriz de confusión**.

Tendría una estructura como:

| | Predicción: No grieta | Predicción: Grieta |
|---|---:|---:|
| **Real: No grieta** | Verdadero negativo | Falso positivo |
| **Real: Grieta** | Falso negativo | Verdadero positivo |

Esta matriz permitirá identificar exactamente qué tipo de errores está cometiendo Crack Scan.

Por ejemplo, si existen muchos falsos negativos, significa que el sistema está dejando pasar imágenes que realmente contienen grietas.

---

# 11. Resultados esperados

Los resultados esperados del proyecto serían:

### 11.1. Clasificación correcta

El sistema debería ser capaz de recibir una imagen nueva y determinar si contiene una grieta.

Por ejemplo:

```text
Imagen
   ↓
Crack Scan
   ↓
Grieta detectada
Probabilidad: 95 %
```

o:

```text
Imagen
   ↓
Crack Scan
   ↓
No se detectó grieta
Probabilidad de grieta: 4 %
```

---

### 11.2. Buen desempeño en imágenes nuevas

Se espera que el modelo tenga un desempeño consistente tanto en las imágenes de entrenamiento como en imágenes que no haya visto anteriormente.

Un resultado problemático sería:

```text
Training Accuracy:   99 %
Validation Accuracy: 70 %
```

porque podría indicar **sobreajuste (overfitting)**.

Un comportamiento más deseable sería que ambas métricas sean relativamente cercanas.

---

### 11.3. Alto recall para las grietas

Uno de los objetivos importantes de Crack Scan sería minimizar los casos en los que existe una grieta pero el sistema indica que no existe.

Por ello, además de Accuracy, se debe prestar especial atención a:

```text
Recall
F1-Score
ROC-AUC
Matriz de confusión
```

---

# 12. CNN desde cero vs. Transfer Learning

Como parte del proyecto también sería útil realizar una comparación experimental.

| Característica | CNN desde cero | MobileNetV2 + Transfer Learning |
|---|---|---|
| Arquitectura | Construida manualmente | Preentrenada |
| Entrenamiento | Desde cero | Aprovecha pesos existentes |
| Cantidad de datos necesaria | Generalmente mayor | Generalmente menor |
| Tiempo de entrenamiento | Mayor | Menor |
| Complejidad | Mayor | Menor |
| Uso recomendado | Experimentación | Modelo principal |

Por eso, para **Crack Scan utilizaría MobileNetV2 con transfer learning como modelo principal**, mientras que una CNN desde cero puede utilizarse como **modelo de comparación**.

Esto además permite demostrar experimentalmente si aprovechar características previamente aprendidas mejora el desempeño en el problema de detección de grietas.

---

# 13. Resultado final esperado del proyecto

El producto final sería un sistema que siga este proceso:

```text
┌──────────────────────┐
│   Usuario carga      │
│      una imagen      │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│   Preprocesamiento   │
│   de la imagen       │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│      MobileNetV2     │
│   CNN preentrenada   │
└──────────┬───────────┘
           ↓
┌──────────────────────┐
│ Clasificación de la  │
│       imagen         │
└──────────┬───────────┘
           ↓
      ┌────┴────┐
      ↓         ↓
   GRIETA    NO GRIETA
      ↓         ↓
  Probabilidad  Probabilidad
```

## Conclusión

Para **Crack Scan**, se propone utilizar una **CNN mediante transfer learning, tomando MobileNetV2 como modelo base**, debido a que permite aprovechar características visuales aprendidas previamente y adaptarlas al problema específico de identificación de grietas.

El sistema deberá realizar el **preprocesamiento de imágenes, aumento de datos, entrenamiento, validación y evaluación**, utilizando métricas como Accuracy, Precision, Recall, F1-Score y ROC-AUC.

El resultado esperado es un modelo capaz de analizar imágenes nuevas y clasificarlas como **"grieta" o "no grieta"**, proporcionando además una probabilidad de predicción. La evaluación mediante una matriz de confusión permitirá determinar los errores del sistema y, especialmente, analizar qué tan bien detecta las grietas existentes.
