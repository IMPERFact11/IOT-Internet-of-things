```
#include <PubSubClient.h> 
#include<WiFi.h>
#include <DHT.h>

#define DHTPIN A5
#define DHTTYPE DHT22
DHT dht(DHTPIN, DHTTYPE);
char buf[240]  ;

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i=0;i<length;i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();
}

WiFiClient espClient;
PubSubClient client(espClient);

void reconnect() {
  // Loop until we're reconnected
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
    // Attempt to connect
    if (client.connect("espClientMaroua")) {
      Serial.println("connected");
       client.subscribe("/sensor/data");
    } else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
      delay(5000);
    }
  }
}


String text5;

String t;



void setup()
{
Serial.begin(115200);
  Serial.println();
  dht.begin();

  client.setServer("192.168.1.3", 1883);
  client.setCallback(callback);

  WiFi.begin("NNLocalNetwork","hv65RNFbiQVP");

  Serial.print("Connecting");
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println();

  Serial.print("Connected, IP address: ");
  Serial.println(WiFi.localIP());
  
}
void loop()
{
float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();
text5 = "temp";


t='"';

String total = "{"+t+text5+t+":"+temperature+"}";

  if (!client.connected()) {
reconnect();

}
if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Erreur lors de la lecture du capteur DHT22 !");
    return;
  }
  client.loop();
  Serial.println( "{"+t+text5+t+":"+temperature+"}");
  total.toCharArray(buf, 240); 
  client.publish("/sensor/data",buf);
  delay(20000);
  
}
```

```
#include <PubSubClient.h> 
#include<WiFi.h>
#include <DHT.h>

#define DHTPIN A5
#define DHTTYPE DHT22

//zlskm2u2i99di15t5j0v
DHT dht(DHTPIN, DHTTYPE);
char buf[240]  ;

void callback(char* topic, byte* payload, unsigned int length) {
  Serial.print("Message arrived [");
  Serial.print(topic);
  Serial.print("] ");
  for (int i=0;i<length;i++) {
    Serial.print((char)payload[i]);
  }
  Serial.println();
}

WiFiClient espClient;
PubSubClient client(espClient);

void reconnect() {
  // Loop until we're reconnected 
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
    // Attempt to connect
    if (client.connect("espClientMaroua")) {
      Serial.println("connected");
       client.subscribe("/sensor/data");
    } else {
      Serial.print("failed, rc=");
      Serial.print(client.state());
      Serial.println(" try again in 5 seconds");
      // Wait 5 seconds before retrying
      delay(5000);
    }
  }
}



String text1;
String text2;
String text3;
String text4;
String text5;
String text6;
String text7;
String text8;
String t;



void setup()
{
Serial.begin(115200);
  Serial.println();
  dht.begin();

  client.setServer("192.168.1.3", 1883);
  client.setCallback(callback);

  WiFi.begin("NNLocalNetwork","hv65RNFbiQVP");

  Serial.print("Connecting");
  while (WiFi.status() != WL_CONNECTED)
  {
    delay(500);
    Serial.print(".");
  }
  Serial.println();

  Serial.print("Connected, IP address: ");
  Serial.println(WiFi.localIP());
  
}
void loop()
{
  
float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();
text5 = "temp";

text1 = "serialNumber";
text2 = "NN-Maroua";
text3 = "sensorType";
text4 = "Thermometer";
text5 = "temp";
text6 = "hum";
text7 = "sensorModel";
text8 = "DHT22";
t='"';

String total ="{"+t+text1+t+":"+t+text2+t+","+t+text3+t+":"+t+text4+t+","+t+text7+t+":"+t+text8+t+","+t+text5+t+":"+temperature+","+t+text6+t+":"+humidity+"}";
  
;

  if (!client.connected()) {
reconnect();

}
if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Erreur lors de la lecture du capteur DHT22 !");
    return;
  }
  client.loop();
  Serial.println( "{"+t+text1+t+":"+t+text2+t+","+t+text3+t+":"+t+text4+t+","+t+text7+t+":"+t+text8+t+","+t+text5+t+":"+temperature+","+t+text6+t+":"+humidity+"}");

  total.toCharArray(buf, 240); 
  client.publish("/sensor/data",buf);
  delay(20000);
  
}
```