## How to send data from an ESP to Mqtt broker (via node red )

By Issa SIDIBE 

we define the topic in which we publish

we write the data on arduino

we translate the string to a json code

```
message.toCharArray(msg, 240);
  client.publish("/sensor/data", msg);
```

```
#include <WiFi.h>
#include <PubSubClient.h>

// Update these with values suitable for your network.

const char* ssid = "NNLocalNetwork";
const char* password = "hv65RNFbiQVP";
const char* mqtt_server = "192.168.1.3";
String text1 = "serialNumber";
String text2 = "NNIssa";
String text3 = "sensorType";
String text4 = "thermometer";
String text5 = "temp";
String text6 = "hum";
String q = "\"";
String C;
const float T = 20;
const float H = 10;


WiFiClient espClient;
PubSubClient client(espClient);
#define MSG_BUFFER_SIZE 240
char msg[MSG_BUFFER_SIZE];


void setup_wifi() {

  delay(10);
  // We start by connecting to a WiFi network
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);

  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  randomSeed(micros());

  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  // Switch on the LED if an 1 was received as first character
  if ((char)payload[0] == '1') {
    digitalWrite(BUILTIN_LED, LOW);   // Turn the LED on (Note that LOW is the voltage level
    // but actually the LED is on; this is because
    // it is active low on the ESP-01)
  } else {
    digitalWrite(BUILTIN_LED, HIGH);  // Turn the LED off by making the voltage HIGH
  }

}

void reconnect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
    if (client.connect("ISSA2")) {
      Serial.println("connected");
      // Once connected, publish an announcement...
      client.publish("/sensor/data", "hello world");
      // ... and resubscribe
      client.subscribe("inTopic");
    } else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
      delay(5000);
    }
  }
}

void setup() {
  pinMode(BUILTIN_LED, OUTPUT);     // Initialize the BUILTIN_LED pin as an output
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop() {

  if (!client.connected()) {
    reconnect();
  }
  client.loop();

  String message = "{" + q + text1 + q + ":" + q + text2 + q + "," + q + text3 + q + ":" + q + text4 + q + "," + q + text5 + q + ":" + q + T + q + "," + q + text6 + q + ":" + q + H + q + "}";
  Serial.println(message);

  message.toCharArray(msg, 240);
  client.publish("/sensor/data", msg);



  delay(2000);
}
```

Real sensor part

```
#include <WiFi.h>
#include <PubSubClient.h>
#include "DHTesp.h" // Click here to get the library: http://librarymanager/All#DHTesp
#include <Ticker.h>
DHTesp dht;


int dhtPin = 17;


// Update these with values suitable for your network.

const char* ssid = "NNLocalNetwork";
const char* password = "hv65RNFbiQVP";
const char* mqtt_server = "192.168.1.3";
String text1 = "serialNumber";
String text2 = "NNIssa";
String text3 = "sensorType";
String text4 = "thermometer";
String text5 = "temp";
String text6 = "hum";
String q = "\"";
String C;
const float T = dht.getTemperature();
const float H = dht.getHumidity();


WiFiClient espClient;
PubSubClient client(espClient);
#define MSG_BUFFER_SIZE 240
char msg[MSG_BUFFER_SIZE];


void setup_wifi() {

  delay(10);
  // We start by connecting to a WiFi network
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);

  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  randomSeed(micros());

  Serial.println("");
  Serial.println("WiFi connected");
  Serial.println("IP address: ");
  Serial.println(WiFi.localIP());
}

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i = 0; i < length; i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();

  // Switch on the LED if an 1 was received as first character
  if ((char)payload[0] == '1') {
    digitalWrite(BUILTIN_LED, LOW);   // Turn the LED on (Note that LOW is the voltage level
    // but actually the LED is on; this is because
    // it is active low on the ESP-01)
  } else {
    digitalWrite(BUILTIN_LED, HIGH);  // Turn the LED off by making the voltage HIGH
  }

}

void reconnect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
    if (client.connect("ISSA2")) {
      Serial.println("connected");
      // Once connected, publish an announcement...
      client.publish("/sensor/data", "hello world");
      // ... and resubscribe
      client.subscribe("inTopic");
    } else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
      delay(5000);
    }
  }
}

void setup() {
  pinMode(BUILTIN_LED, OUTPUT);     // Initialize the BUILTIN_LED pin as an output
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void loop() {

  if (!client.connected()) {
    reconnect();
  }
  client.loop();

  String message = "{" + q + text1 + q + ":" + q + text2 + q + "," + q + text3 + q + ":" + q + text4 + q + "," + q + text5 + q + ":" + q + T + q + "," + q + text6 + q + ":" + q + H + q + "}";
  Serial.println(message);

  message.toCharArray(msg, 240);
  client.publish("/sensor/data", msg);



  delay(2000);
}
```

![image.png](.attachments.245540927/image.png)  
s