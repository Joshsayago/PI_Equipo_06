````markdown
# Actividad 01 — Adquisición de datos con un potenciómetro

## Objetivo

Realizar la adquisición de una señal analógica mediante un potenciómetro conectado al ESP32. Además, se buscó mejorar la estabilidad de las mediciones mediante el promedio de varias lecturas y convertir el valor obtenido por el ADC a voltaje.

## Conexión del circuito

El potenciómetro fue conectado al ESP32 de la siguiente manera:

| Potenciómetro | ESP32 |
|---|---|
| Terminal lateral | 3.3 V |
| Terminal lateral | GND |
| Terminal central | GPIO 34 |

El terminal central del potenciómetro proporciona un voltaje variable dependiendo de su posición. Esta señal es adquirida mediante el ADC del ESP32.

## Procesamiento de la señal

El ESP32 utiliza un ADC de 12 bits, por lo que las lecturas pueden tomar valores entre 0 y 4095.

Para obtener una medición más estable se realizaron varias lecturas consecutivas y se calculó su promedio.

```cpp
long suma = 0;

for (int i = 0; i < 10; i++) {
  suma += analogRead(potPin);
  delay(10);
}

float promedioADC = suma / 10.0;
````

Posteriormente, el valor ADC promedio se convirtió a voltaje utilizando:

$$
V = \frac{ADC}{4095}\times 3.3
$$

En el código:

```cpp
float voltaje = promedioADC * 3.3 / 4095.0;
```

## Resultados

Los resultados de las mediciones se observaron durante la ejecución del programa. Al variar la posición del potenciómetro, el valor obtenido por el ADC y el voltaje calculado también cambiaron.

![Resultados de la actividad 01](<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/1cdbd964-9c94-479e-a5c3-3cb4209aecb2" />
)
)

La imagen muestra los valores de voltaje obtenidos durante la ejecución del programa y permite verificar la variación de la señal generada por el potenciómetro.

---

# Actividad 02 — Conexión del ESP32 a una red Wi-Fi

## Objetivo

Establecer una conexión inalámbrica entre el ESP32 y una red Wi-Fi para permitir posteriormente la transmisión de datos hacia plataformas IoT.

## Conexión Wi-Fi

Para establecer la conexión se utilizó la biblioteca:

```cpp
#include <WiFi.h>
```

El ESP32 fue configurado con el nombre y contraseña de la red Wi-Fi.

El programa verifica continuamente el estado de la conexión hasta que el dispositivo logra conectarse correctamente.

```cpp
WiFi.begin(ssid, password);

while (WiFi.status() != WL_CONNECTED) {
  delay(500);
  Serial.print(".");
}
```

Una vez establecida la conexión, se puede obtener la dirección IP asignada al ESP32 mediante:

```cpp
Serial.println(WiFi.localIP());
```

## Resultados

La ejecución del programa permitió comprobar la conexión del ESP32 a la red Wi-Fi y obtener los datos generados durante la prueba.

![Resultados de la actividad 02](<img width="1600" height="906" alt="image" src="https://github.com/user-attachments/assets/41f81562-e8b8-4449-9d54-b43c3ecdd38c" />
)

La captura muestra los resultados obtenidos durante la ejecución del programa y confirma el funcionamiento de la conexión utilizada para las actividades posteriores de envío de datos a plataformas IoT.

```

 

