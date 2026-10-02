## Ejercicio 01: Mejora de Lectura Analógica (Promediado y Conversión a Voltaje)

En este ejercicio se ha optimizado la lectura de un sensor analógico (potenciómetro) conectado a un ESP32 (microcontrolador). En el contexto del Internet de las Cosas (IoT), se debe asegurar que los datos que se envían a la nube o se procesan localmente sean precisos y estables. Para lograr esto, se aplicaron 2 cosas: **el promediado de datos** y la **conversión a voltaje real**.
<p align="center">
<img width="500" height="450" alt="image" src="https://github.com/user-attachments/assets/ab7c88d0-cd43-4abc-bd76-9487f597e6ff" />
<p>
  
### 1. Promediado de Datos (Reducción de Ruido Eléctrico)

En el mundo físico, los sensores están expuestos a interferencias electromagnéticas y pequeñas fluctuaciones de corriente conocidas como **"ruido eléctrico"**. Si código tomara una sola lectura instantánea, correríamos el riesgo de capturar un "pico" falso, enviando un dato erróneo.

**¿Cómo lo solucionamos en el código?**
En lugar de tomar un solo valor, el programa realiza un muestreo de **15 lecturas** consecutivas con un pequeño intervalo de tiempo (delay(100)). 
* Se acumulan estos valores en la variable suma.
* Una vez que llegamos a la lectura número 15, dividimos el total entre 15 (suma / 15) para obtener el promedioDigital.

**Beneficio:** Este método actúa como un filtro digital de paso bajo muy sencillo. Al promediar, los picos altos y bajos repentinos se cancelan entre sí, entregándonos una lectura mucho más estable, suave y confiable.

### Conversión de Valores ADC a Voltaje

Los microcontroladores no entienden de "voltios" en el mundo analógico; ellos ven el mundo a través de su **Convertidor Analógico-Digital (ADC)**, el cual traduce un voltaje físico en un número digital que el procesador puede manejar.

En este caso (trabajando con una placa de 3.3V y una resolución de 12 bits):
* El ADC tiene una resolución de **12 bits**, lo que significa que puede dividir el voltaje de entrada en $2^{12}$ pasos, es decir, **4096 niveles** (que van del `0` al 4095).
* 0 equivale a 0 Voltios (GND).
* 4095 equivale al voltaje máximo de referencia, que es **3.3 Voltios**.

Para devolver el dato a un valor que los humanos y los sistemas externos entiendan (Voltios), aplicamos una regla de tres simple plasmada en la siguiente fórmula:
float voltaje = (promedioDigital * 3.3) / 4095; Multiplicamos nuestra lectura promedio por el voltaje máximo del sistema y lo dividimos entre la resolución máxima del ADC.

**Código mejorado:**
```cpp
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
```
<p align="center">
<img width="800" height="458" alt="image" src="https://github.com/user-attachments/assets/4a4922ba-8a73-47f1-9a97-446730992be6" />
</p>


## Ejercicio 05: Control de LED vía Interfaz Web (ESP32)

En este ejercicio, hemos dado un paso crucial en el mundo del IoT: la interacción remota. Configuramos el ESP32 no solo para conectarse a una red WiFi, sino para actuar como un **Servidor Web** capaz de alojar una página web y recibir comandos desde un navegador para encender o apagar un componente físico (un LED).

###¿Qué se necesitó para llevarlo a cabo?

Para replicar este ejercicio, se utilizaron los siguientes elementos:
* **Hardware:**
  * Placa de desarrollo ESP32.
  * Un LED (cualquier color).
  * Una resistencia de 220Ω o 330Ω (para proteger el LED limitando la corriente).
  * Cables puente (jumpers) y una protoboard.
  * *(Nota: El ESP32 cuenta con un LED interno conectado al pin 2, por lo que el código funcionará de forma nativa incluso sin componentes externos, encendiendo el LED de la propia placa).*
* **Software:**
  * Entorno de desarrollo Arduino IDE con la tarjeta ESP32 configurada.
  * Red WiFi local activa (con nombre de red y contraseña).
  * Un dispositivo (celular o computadora) conectado a la **misma red WiFi** para acceder a la plataforma.

### Explicación de las Conexiones

El circuito físico diseñado es bastante directo:
1. **Ánodo del LED (pata larga, positivo):** Se conecta a un extremo de la **resistencia**. El otro extremo de la resistencia va conectado al **Pin Digital 2** del ESP32.
2. **Cátodo del LED (pata corta, negativo):** Se conecta directamente a cualquiera de los pines **GND (Tierra)** del ESP32.

*Dinámica:* Cuando enviamos una señal de nivel alto (`HIGH`) desde el Pin 2, la corriente fluye a través de la resistencia hacia el LED, emitiendo luz y cerrando el circuito en GND. Al enviar un nivel bajo (`LOW`), la corriente se detiene y el LED se apaga.

<div align="center">
  <img width="720" height="980" alt="image" src="https://github.com/user-attachments/assets/b0ee43ec-cc23-43c5-8ecd-c7998b8779f2" />
</div>

### ¿Cómo se trabajó el código?

El programa transforma al ESP32 en un pequeño dispositivo inteligente con su propia interfaz gráfica. La lógica se divide en tres fases principales:

1. **Conexión a la red WiFi:** 
   Mediante la librería `<WiFi.h>`, ingresamos nuestras credenciales (SSID y Password). El ESP32 se conecta al router y este le asigna una **Dirección IP local**. Esta IP es nuestra "llave de entrada"; al escribirla en un navegador web, accedemos directamente a nuestro ESP32.
2. **Creación del Servidor Web:**
   Instanciamos un servidor en el **puerto 80** (`WiFiServer server(80);`), que es el puerto estándar para el tráfico web (HTTP). En la función `loop()`, el ESP32 se queda "escuchando" constantemente, esperando a que un cliente (nuestro navegador) se conecte a él.
3. **Interfaz Gráfica e Interacción (Peticiones HTTP):**
   Cuando el navegador se conecta a la IP del ESP32, este le responde enviando código HTML y CSS en texto plano. Esto renderiza una página web sencilla con dos botones: "ENCENDER LED" y "APAGAR LED". 
   * Si presionas el botón verde de encendido, el navegador envía la petición `GET /ON` en la URL. El ESP32 detecta esta cadena de texto y ejecuta `digitalWrite(ledPin, HIGH)`.
   * Si presionas el botón rojo, el navegador envía `GET /OFF`, y el ESP32 procede a apagar el componente con `digitalWrite(ledPin, LOW)`.

### Código que se usó

```cpp
#include <WiFi.h>

// Reemplaza con tus credenciales de red
const char* ssid = "iPhoneDomi";
const char* password = "12341234";

// Configura el servidor web en el puerto 80 (HTTP estándar)
WiFiServer server(80);

// Asignamos el pin digital para el LED
const int ledPin = 2; 

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);
  digitalWrite(ledPin, LOW); // Iniciamos con el LED apagado por defecto

  // Iniciar conexión WiFi
  Serial.print("Conectando a la red ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);

  // Bucle de espera hasta que la conexión sea exitosa
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("");
  Serial.println("¡WiFi conectado!");
  Serial.print("Dirección IP para controlar el LED: ");
  // Imprime la IP que debes poner en el navegador web
  Serial.println(WiFi.localIP()); 

  // Iniciar el servidor
  server.begin();
}

void loop() {
  WiFiClient client = server.available(); // Escucha a los clientes entrantes

  if (client) {
    String currentLine = ""; 
    while (client.connected()) {
      if (client.available()) {
        char c = client.read();
        
        // Si la petición HTTP termina (salto de línea), enviamos la respuesta HTML
        if (c == '\n') {
          if (currentLine.length() == 0) {
            // 1. Cabeceras HTTP estándar
            client.println("HTTP/1.1 200 OK");
            client.println("Content-type:text/html");
            client.println();
            
            // 2. Interfaz Web en HTML y CSS
            client.print("<html><head><meta name=\"viewport\" content=\"width=device-width, initial-scale=1\">");
            client.print("<style>body{font-family: Arial; text-align: center; margin-top: 50px;}");
            client.print(".btn{background-color: #4CAF50; color: white; padding: 15px 32px; font-size: 20px; text-decoration: none; border-radius: 8px;} ");
            client.print(".btn-off{background-color: #f44336;}</style></head>");
            client.print("<body><h1>Control de LED - ESP32</h1>");
            client.print("<p><a href=\"/ON\"><button class=\"btn\">ENCENDER LED</button></a></p>");
            client.print("<p><a href=\"/OFF\"><button class=\"btn btn-off\">APAGAR LED</button></a></p>");
            client.print("</body></html>");
            client.println();
            break;
          } else {
            currentLine = "";
          }
        } else if (c != '\r') {
          currentLine += c; // Construye la línea de la petición
        }

        // 3. Revisa qué botón se presionó en la plataforma web y acciona el hardware
        if (currentLine.endsWith("GET /ON")) {
          digitalWrite(ledPin, HIGH); // Enciende el LED
        }
        if (currentLine.endsWith("GET /OFF")) {
          digitalWrite(ledPin, LOW);  // Apaga el LED
        }
      }
    }
    client.stop(); // Cierra la conexión con el cliente para liberar recursos
  }
}
```
<p align="center">
<img width="1600" height="402" alt="image" src="https://github.com/user-attachments/assets/5dbfeed9-4412-4a83-a1d8-5ded4e2db3df" />
<p>
