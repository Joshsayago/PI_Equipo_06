## Ejercicio 01: Mejora de Lectura Analógica (Promediado y Conversión a Voltaje)

En este ejercicio se ha optimizado la lectura de un sensor analógico (potenciómetro) conectado a un ESP32 (microcontrolador). En el contexto del Internet de las Cosas (IoT), se debe asegurar que los datos que se envían a la nube o se procesan localmente sean precisos y estables. Para lograr esto, se aplicaron 2 cosas: **el promediado de datos** y la **conversión a voltaje real**.
<p align="center">
<img width="500" height="450" alt="image" src="https://github.com/user-attachments/assets/ab7c88d0-cd43-4abc-bd76-9487f597e6ff" />
<p>
  
### Promediado de Datos (Reducción de Ruido Eléctrico)

En el mundo físico, los sensores están expuestos a interferencias electromagnéticas y pequeñas fluctuaciones de corriente conocidas como **"ruido eléctrico"**. Si código tomara una sola lectura instantánea, correríamos el riesgo de capturar un "pico" falso, enviando un dato erróneo.

** ¿Cómo lo solucionamos en el código? **
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

## Ejercicio 02: Conexión a Red WiFi (Smartphone Hotspot)

Para que un dispositivo sea considerado parte del "Internet de las Cosas", necesita, por definición, estar conectado a una red. Se configura el ESP32 para que se conecte a un punto de acceso inalámbrico (un Hotspot de un Smartphone) y verifique su conexión obteniendo una **Dirección IP local**.

### ¿Qué se necesitó?
* **Hardware:**
  * ESP32.
  * Cable USB para programación y alimentación.
* **Software / Conectividad:**
  * Entorno de desarrollo Arduino IDE.
  * Un Smartphone con la función de **"Compartir Internet"**, "Hotspot" o "Zona Wi-Fi" activada.

### Configuración del Hotspot

1. Activar la opción de compartir internet en el Smartphone.
2. Definir un **Nombre de Red (SSID)** reconocible (ej. *"iPhone de Diego"*).
3. Establecer una **Contraseña** de seguridad (ej. *"diego1234567"*).
Además, las credenciales en el código tienen que coincidir exactamente con las del teléfono, respetando mayúsculas, minúsculas y espacios.

### ¿Cómo se trabajó el código?

El código utiliza la librería estándar <WiFi.h> del ESP32, la cual facilita enormemente la gestión de redes.

1. **Modo Estación (Station Mode):**
   Se usó la instrucción WiFi.mode(WIFI_STA);. Esto le dice al ESP32 que actúe como un "cliente" o "estación" que se va a conectar a un router existente (el celular), en lugar de crear su propia red (Modo Access Point).
2. **Proceso de Conexión:**
   Con WiFi.begin(ssid, password); iniciamos el intento de conexión. Como este proceso no es instantáneo, utilizamos un bucle while que verifica constantemente el estado de la conexión (WiFi.status()). Mientras no esté conectado, el monitor serie imprime puntos creando un efecto de "cargando".
3. **Asignación de IP:**
   Una vez que el teléfono acepta la conexión del ESP32, le asigna una dirección IP. Con el WiFi.localIP() para leer esta dirección e imprimirla en el Monitor Serie, confirmando el éxito de la red.
4. **Resiliencia (Reconexión automática):**
   Una característica destacada de este código es que dentro del loop() se monitorea constantemente el estado del WiFi. Si el celular se apaga, se aleja o la señal cae, el ESP32 lo detecta e intenta reconectarse automáticamente de forma indefinida, garantizando que el dispositivo no se quede "congelado" sin red.

Monitor Serie

<div align="center">
 <img width="800" height="499" alt="image" src="https://github.com/user-attachments/assets/43a289e7-ffd4-4dc4-bd52-94d43fc336a7" />

</div>

###  Código de Implementación

```cpp
#include "WiFi.h"
// Credenciales de la red (Hotspot del celular)
const char* ssid = "iPhone de Diego";
const char* password = "diego1234567";
void setup() {
  Serial.begin(115200);
  delay(10);
  Serial.println("\n--- Configurando Conexión Wi-Fi ---");
  // 1. Configuramos el ESP32 en modo "Estación" (Cliente)
  WiFi.mode(WIFI_STA);
  
  // 2. Iniciamos la solicitud de conexión
  WiFi.begin(ssid, password);
  Serial.print("Conectando a la red: ");
  Serial.println(ssid);

  // 3. Esperamos a que la conexión se establezca
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  // 4. Conexión exitosa: Mostramos los datos de red
  Serial.println("\n\n=================================");
  Serial.println("¡CONEXIÓN EXITOSA!");
  Serial.print("Conectado a: ");
  Serial.println(ssid);
  
  Serial.print("Dirección IP asignada: ");
  Serial.println(WiFi.localIP()); 
  Serial.println("=================================\n");
}

void loop() {
  // 5. Monitoreo constante: Si se pierde la red, intenta reconectar
  if (WiFi.status() != WL_CONNECTED) {
    Serial.println("Se perdió la conexión. Intentando reconectar...");
    WiFi.begin(ssid, password);
    
    // Bucle de espera para la reconexión
    while (WiFi.status() != WL_CONNECTED) {
      delay(500);
      Serial.print(".");
    }
    
    Serial.println("\nReconectado. Nueva IP: ");
    Serial.println(WiFi.localIP());
  }
  
  // Esperamos 5 segundos antes de volver a comprobar el estado
  delay(5000);
}
```
##  Ejercicio 03: Telemetría en Tiempo Real y Monitoreo en la Nube (IoT)

En este ejercicio escalamos nuestra aplicación al nivel de un sistema IoT completo. Conectamos un potenciómetro al ESP32 para adquirir datos del mundo físico, procesarlos mediante promediado para eliminar el ruido y transmitir el valor de voltaje en tiempo real hacia plataformas de IoT en la nube (como **Arduino IoT Cloud**, **ThingSpeak** o **Ubidots**).

### ¿Qué se necesitó para llevarlo a cabo?
  * ESP32.
  * Potenciómetro (10kΩ recomendado).
  * Protoboard y cables puente (jumpers).
  * Entorno de desarrollo Arduino IDE 
  * Cuenta activa en la plataforma **Arduino IoT Cloud** (o plataformas compatibles como ThingSpeak / Ubidots).
  * Archivo de propiedades de la nube, donde se gestionan las credenciales WiFi de forma segura y la declaración de variables sincronizadas.

---

### Explicación de las Conexiones y Arquitectura
El esquema físico de conexión del potenciómetro al ESP32 se realizó de la siguiente manera:
1. **Pauta / Terminal Extrema 1:** Conectada a la línea de **3.3V** del ESP32.
2. **Terminal Central (Wiper/Señal):** Conectada al **GPIO34** (Canal ADC1_CH6 del ESP32).
3. **Pauta / Terminal Extrema 2:** Conectada a **GND (Tierra)**.

**Arquitectura de Datos:** A medida que giramos la perilla del potenciómetro, la terminal central varía su nivel de voltaje entre 0V y 3.3V. El ESP32 lee esta señal analógica, realiza el filtrado por software y la convierte en una variable global que se sincroniza automáticamente con el Dashboard en la Nube.

<div align="center">
  <img width="900" height="800" alt="image" src="https://github.com/user-attachments/assets/479a0d45-e1ee-4423-a21a-5650d6787099" />
  <p> <i>Figura 1: Conexión del potenciómetro al pin analógico GPIO34 del ESP32.</i></p>
</div>

---

### ¿Cómo se trabajó la integración con la Nube?
**Gestión de la Nube con thingProperties.h y ArduinoCloud:**
En lugar de programar peticiones HTTP o conexiones MQTT desde cero, utilizamos la librería oficial de Arduino Cloud. En el archivo auxiliar thingProperties.h se define la variable voltaje y las credenciales WiFi. En la función setup()`, con `ArduinoCloud.begin()` el ESP32 inicia la comunicación con los servidores.
Antes de saturar la red enviando datos crudos e instables, el código ejecuta un ciclo de muestreo local:
   * Captura **15 lecturas** consecutivas (delay(100)).
   * Calcula el promedio matemático (suma / 15.0`) para eliminar picos de ruido eléctrico.
   * Convierte el promedio digital a voltaje real usando la escala del ADC de 12 bits: 
     $$\text{Voltaje} = \frac{\text{Promedio Digital} \times 3.3}{4095}$$
En cada iteración del loop(), la función ArduinoCloud.update() gestiona en segundo plano la reconexión y transmisión de datos. Al momento de asignar el resultado del cálculo a la variable voltaje, la librería detecta el cambio de valor y lo envía inmediatamente a la Nube. Se incluye una función tipo *callback* que reacciona si el valor de la variable es modificado desde un control interactivo (como un Slider o Knob) en el Dashboard web o la App móvil.

---

###  Visualización en las Plataformas IoT (Dashboards)

Una vez que los datos llegan a la Nube, se pueden vincular a diferentes elementos gráficos (widgets) para visualizar la variación del potenciómetro en tiempo real.

<div align="center">
  <img width="1600" height="997" alt="image" src="https://github.com/user-attachments/assets/d705a15f-6318-488c-ba6f-1cb55d7d1d94" />
  <p>
</div>

<br>

<div align="center">
  <img width="800" height="347" alt="image" src="https://github.com/user-attachments/assets/332a218f-2874-42ef-984d-80f0cf17ce7f" />
<img width="450" height="800" alt="image" src="https://github.com/user-attachments/assets/9ac434f1-2df2-4fbe-88d9-480164774e72" />

  <p>
</div>

## Ejercicio 04: Monitoreo de Temperatura en Tiempo Real con Sensor LM35 y Plataformas IoT

En este ejercicio se realiza el monitoreo de temperatura en tiempo real utilizando un sensor LM35 del kit Keyestudio conectado al microcontrolador ESP32. El dato de temperatura es procesado localmente mediante un filtrado por promediado de lecturas y posteriormente transmitido a plataformas de IoT en la nube como Arduino IoT Cloud, ThingSpeak y Ubidots.

### Que se necesitó

* Hardware: Placa de desarrollo ESP32, sensor de temperatura LM35 del kit Keyestudio, protoboard y cables de conexion.
* Software y Plataformas Cloud: Entorno de desarrollo Arduino IDE, archivo de configuracion thingProperties.h, cuenta en Arduino IoT Cloud, ThingSpeak y Ubidots.

---

### Explicacion de las Conexiones y Funcionamiento del Sensor

El sensor LM35 mide temperatura entregando un voltaje de salida proporcional a la escala Celsius, con una relacion de 10 milivoltios por cada grado Celsius (10 mV / °C). 

Las conexiones entre el sensor y la placa ESP32 se realizaron de la siguiente manera:
1. Pin VCC del LM35: Conectado al pin de alimentacion de la placa.
2. Pin SIGNAL / OUT del LM35: Conectado al pin GPIO34 (canal ADC1_CH6) del ESP32.
3. Pin GND del LM35: Conectado a la linea de tierra (GND) del ESP32.

<div align="center">
 <img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/c95a77ed-b3a9-4a4c-afe2-66a7afe93850" />
</div>

---

###  Como se trabajo el codigo y la integracion Cloud

El programa realiza el procesamiento de la senal del sensor y gestiona la transmision de datos a la nube mediante los siguientes pasos:

1. Lectura directa en milivoltios: Se utiliza la funcion analogReadMilliVolts en el pin GPIO34 para obtener la lectura directamente en milivoltios.
2. Muestreo y acumulacion: Se toman 15 lecturas consecutivas con un intervalo de 100 milisegundos entre cada una, acumulando los valores en milivoltios.
3. Promediado y conversion a grados Celsius: Una vez acumuladas las 15 muestras, se calcula el promedio dividiendo la suma entre 15.0. El resultado en milivoltios se divide entre 10.0 para obtener el valor equivalente en grados Celsius.
4. Sincronizacion con la nube: La funcion ArduinoCloud.update() se ejecuta continuamente en el bucle principal para mantener la conexion activa y transmitir la variable de temperatura actualizada hacia el dashboard en tiempo real.

---

### 4. Visualizacion en las Plataformas IoT (Dashboards)



<div align="center">
 <img width="900" height="1600" alt="image" src="https://github.com/user-attachments/assets/636d4177-4848-436c-afd0-c2c56cb8ed6e" />

</div>



## Ejercicio 05: Control de LED vía Interfaz Web (ESP32)

En este ejercicio, hemos dado un paso crucial en el mundo del IoT: la interacción remota. Configuramos el ESP32 no solo para conectarse a una red WiFi, sino para actuar como un **Servidor Web** capaz de alojar una página web y recibir comandos desde un navegador para encender o apagar un componente físico (un LED).

### ¿Qué se necesitó para llevarlo a cabo?

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
