## 📡 Ejercicio: Mejora de Lectura Analógica (Promediado y Conversión a Voltaje)

En este ejercicio se ha optimizado la lectura de un sensor analógico (como un potenciómetro) conectado a nuestro microcontrolador. En el contexto del Internet de las Cosas (IoT), es vital asegurar que los datos que enviamos a la nube o procesamos localmente sean precisos y estables. Para lograr esto, implementamos dos técnicas clave: **el promediado de datos** y la **conversión a voltaje real**.
<p align="center">
<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/ab7c88d0-cd43-4abc-bd76-9487f597e6ff" />
<p>
  
### 1. Promediado de Datos (Reducción de Ruido Eléctrico)

En el mundo físico, los sensores están expuestos a interferencias electromagnéticas y pequeñas fluctuaciones de corriente conocidas como **"ruido eléctrico"**. Si nuestro código tomara una sola lectura instantánea, correríamos el riesgo de capturar un "pico" falso, enviando un dato erróneo.

**¿Cómo lo solucionamos en el código?**
En lugar de tomar un solo valor, el programa realiza un muestreo de **15 lecturas** consecutivas con un pequeño intervalo de tiempo (delay(100)). 
* Acumulamos estos valores en la variable suma.
* Una vez que llegamos a la lectura número 15, dividimos el total entre 15 (suma / 15) para obtener el promedioDigital.

**Beneficio:** Este método actúa como un filtro digital de paso bajo muy sencillo. Al promediar, los picos altos y bajos repentinos se cancelan entre sí, entregándonos una lectura mucho más estable, suave y confiable.

### 2. Conversión de Valores ADC a Voltaje

Los microcontroladores no entienden de "voltios" en el mundo analógico; ellos ven el mundo a través de su **Convertidor Analógico-Digital (ADC)**, el cual traduce un voltaje físico en un número digital que el procesador puede manejar.

En este caso (trabajando con una placa de 3.3V y una resolución de 12 bits):
* El ADC tiene una resolución de **12 bits**, lo que significa que puede dividir el voltaje de entrada en $2^{12}$ pasos, es decir, **4096 niveles** (que van del `0` al 4095).
* `0` equivale a 0 Voltios (GND).
* `4095` equivale al voltaje máximo de referencia, que es **3.3 Voltios**.

Para devolver el dato a un valor que los humanos y los sistemas externos entiendan (Voltios), aplicamos una regla de tres simple plasmada en la siguiente fórmula:

```cpp
float voltaje = (promedioDigital * 3.3) / 4095; Multiplicamos nuestra lectura promedio por el voltaje máximo del sistema y lo dividimos entre la resolución máxima del ADC
```
int potPin = 34;
int contador = 0;
float suma = 0;

void setup() {
  Serial.begin(115200);
}

void loop() {
  if (contador < 15) {
    // Leemos el valor crudo del ADC
    int valorDigital = analogRead(potPin);

    // Acumulamos las lecturas
    suma += valorDigital;
    contador++;

    delay(100);
  }
  else if (contador == 15) {
    // 1. Calculamos el promedio para eliminar el ruido
    float promedioDigital = suma / 15;

    // 2. Convertimos el valor digital promedio a Voltaje real (0 - 3.3V)
    float voltaje = (promedioDigital * 3.3) / 4095;

    // Imprimimos los resultados en el Monitor Serie
    Serial.println("\n--- RESULTADOS ---");
    Serial.print("Promedio Digital: ");
    Serial.println(promedioDigital, 2);
    Serial.print("Voltaje Equivalente: ");
    Serial.print(voltaje, 3);
    Serial.println(" V");
    Serial.println("-------------------\n");

    // Reiniciamos variables para el siguiente ciclo de muestreo
    suma = 0;
    contador = 0;
  }
}
<p align="center">
<img width="800" height="458" alt="image" src="https://github.com/user-attachments/assets/4a4922ba-8a73-47f1-9a97-446730992be6" />
</p>
