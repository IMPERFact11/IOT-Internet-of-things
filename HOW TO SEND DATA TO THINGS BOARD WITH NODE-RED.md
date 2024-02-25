# HOW TO SEND DATA TO THINGS BOARD WITH NODE

1-connect to wifi 

2-connect to MQTT 

3-write the JSON code and send 

## Publication by node red

go on node red

* create an inject box

  to write the message you would like to publish

  Attenttion: only in **JSON format**

  example :

  ```
  {"serialNumber": "NNIssa",     "sensorType":"Thermometer","temp":-15,"hum":20}
  
  
  
  
  ```

  ```
  Jason message is written on this format
  "key":value, // for integer 
  "key":"message" // for messages in letter 
  
  
  
  ```
* create JSON BOX

  to see the object created via the inject box on the debugger
* Create the mqtt out to send/publish the message in a specific topic

![image.png](.attachments.244728179/image.png)  
![image (2).png](.attachments.244728179/image%20%282%29.png)

# How to use ESP to send data to the things board

# Thingsboard is the platform to receive data and look at them on real time (for the prof only)

first write the message on arduino

we tray to make a jason code with arduino

```
String text1;
String text2;
String text3;
String text4;
String text5;
String text6;
String q;
const float T= 20;
const float H=10;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
text1 = "serialNumber";
text2 = "ISSA";
text3 = "sensorType";
text4 = "thermometer";
text5 = "temp";
text6 ="hum";
q="\"";
Serial.println("{"+q+text1+q+":"+q+text2+q+","+q+text3+q+":"+q+text4+q+","+q+text5+q+":"+T+","+q+text6+q+":"+H+"}");


delay(1000);
}
```

# then we enter this jason code on Mqtt boker to send it into node red ....