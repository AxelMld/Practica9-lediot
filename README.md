# **PRÁCTICA 9 LED IOT**

## **INICIO DE NODEJS** ##

1. Se abre el programa "CMD" en modo administrador.
2. Una vez abierto se ponen el siguiente comando.

                    2. Para arrancar nodejs se usa el comando **node- red** 

Aparecera lo siguiente ya inicio el nodejs, se deja abierto para su uso 

![](https://github.com/AxelMld/Practica6-enviodedatos/blob/main/arranque%20nodejs.png?raw=true)

3. Nos Dirigimos al navegador buscamos la pagina **localhost:1880**

Aparecera la siguiente imagen lugar de trabajo de nodejs


![](https://github.com/AxelMld/Practica6-enviodedatos/blob/main/nodejs%20trabajo.png?raw=true)

----------------------------------------------------------------

## **REALIZACION Y CONFIGURACION DE ESTRUCTURA EN NODEJS** ##

1. Se realiza la siguiente estructura 

![]()

### Configuracion y herramientas usadas 

* Para axelm se utilizo  **mqtt out** "nombre utilizado 
* para Boton de encendido **switch** 


--------------------------------------------------------------

## CONFIGURACION ESTRUCTURA NODEJS

* Para la configuracion de mqtt in se utilizo la siguiente 
![]()

* Para boton switch 

![]()

---------------------------------------------------------------

# **CONEXION Y CODIGO EN WOKWI**

## Para la simulación nos dirigimos a la página  

woki : https://wokwi.com

#### Dashboard de página a utilizar 
![](https://github.com/AxelMld/Practica-3-Sensor-Ultrasonico-/blob/main/dash.png?raw=true)


## Para está práctica se utilizó 

* Módulo ESP32 
* Relay


## Pasos a Seguir 

1. Seleccionar el módulo ESP32.
2. Escoger los dispositivos a utilizar anteriormente mensionados. 
3. Realizar las conexiones como se muestra en el apartado "conexión".
4. Agregar las librerias mensiadas en el apartado Librerías 




## **Conexión**

![]()


## **Librerías**

1. ArduinoJson
2. PubSubClient
3. SimpleWiFiClient

## Código utilizado 


```
#include <WiFi.h>
#include <PubSubClient.h>

const char* ssid = "Wokwi-GUEST";
const char* password = "";
const char* mqttServer = "44.195.202.69";
const int mqttPort = 1883;
const char* mqttUser = "axelm";
const char* mqttPassword = "1234";
const char* mqttTopic = "axelm";

WiFiClient espClient;
PubSubClient client(espClient);

int ledPin = 13; // Pin del LED

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqttServer, mqttPort);
  client.setCallback(callback);
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop();
}

void setup_wifi() {
  delay(10);
  Serial.println();
  Serial.print("Conectando a: ");
  Serial.println(ssid);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println("Conectado a la red WiFi");
}

void reconnect() {
  while (!client.connected()) {
    Serial.print("Intentando conexión MQTT...");
    if (client.connect("ESP32Client", mqttUser, mqttPassword)) {
      Serial.println("Conectado");
      client.subscribe(mqttTopic);
    } else {
      Serial.print("Error de conexión, rc=");
      Serial.print(client.state());
      Serial.println(" Intentando de nuevo en 5 segundos");
      delay(5000);
    }
  }
}

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Mensaje recibido: [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  if (strcmp(topic, mqttTopic) == 0) {
    if ((char)payload[0] == '1') {
      digitalWrite(ledPin, HIGH);
    } else {
      digitalWrite(ledPin, LOW);
    }
  }
}

```


# **RESULTADO**

## 1. Resultado de la pagina WOKWI 

![]()

![]()





# Creditos 

**Axel Miranda.**
