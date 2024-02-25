
# Connect arduino to ESP & Node_red Using 

By Issa SIDIBE 

## Connect arduino IDE with the ESP

1- go on tool "choose the right ESP

2- go on tool again choose the right USB port

## how to launch Node-red

1. go on command prompt
2. type node-red
3. copy the IP adress and paste it on webside

## How to use Node-red

1. to send a message

   \- create "inject"
   * create "mqtt out"
2. To receive a message
   * choose "debuger"
   * choose "mqtt in"
3. To Export a project

   go on export

   ![image (2).png](.attachments.243862496/image%20%282%29.png)

   ```
   [
       {
           "id": "f1ce21e22ab3fe86",
           "type": "tab",
           "label": "Flow 1",
           "disabled": false,
           "info": "",
           "env": []
       },
       {
           "id": "e3efa8eeb72ce633",
           "type": "mqtt in",
           "z": "f1ce21e22ab3fe86",
           "name": "",
           "topic": "Master ",
           "qos": "2",
           "datatype": "auto",
           "broker": "11898a99e8f10733",
           "nl": false,
           "rap": true,
           "rh": 0,
           "inputs": 0,
           "x": 320,
           "y": 560,
           "wires": [
               [
                   "e4cfc6009493586f"
               ]
           ]
       },
       {
           "id": "fffbe00ffb09f25a",
           "type": "mqtt out",
           "z": "f1ce21e22ab3fe86",
           "name": "",
           "topic": "MASTER GROUP",
           "qos": "",
           "retain": "",
           "respTopic": "",
           "contentType": "",
           "userProps": "",
           "correl": "",
           "expiry": "",
           "broker": "11898a99e8f10733",
           "x": 840,
           "y": 660,
           "wires": []
       },
       {
           "id": "d2acf7c89b8fca3f",
           "type": "inject",
           "z": "f1ce21e22ab3fe86",
           "name": "",
           "props": [
               {
                   "p": "payload"
               },
               {
                   "p": "topic",
                   "vt": "str"
               }
           ],
           "repeat": "",
           "crontab": "",
           "once": false,
           "onceDelay": 0.1,
           "topic": "",
           "payload": "",
           "payloadType": "date",
           "x": 330,
           "y": 660,
           "wires": [
               [
                   "fffbe00ffb09f25a"
               ]
           ]
       },
       {
           "id": "e4cfc6009493586f",
           "type": "debug",
           "z": "f1ce21e22ab3fe86",
           "name": "",
           "active": true,
           "tosidebar": true,
           "console": false,
           "tostatus": false,
           "complete": "false",
           "statusVal": "",
           "statusType": "auto",
           "x": 770,
           "y": 560,
           "wires": []
       },
       {
           "id": "11898a99e8f10733",
           "type": "mqtt-broker",
           "name": "",
           "broker": "192.168.1.3",
           "port": "1883",
           "clientid": "",
           "autoConnect": true,
           "usetls": false,
           "protocolVersion": "4",
           "keepalive": "60",
           "cleansession": true,
           "birthTopic": "",
           "birthQos": "0",
           "birthPayload": "",
           "birthMsg": {},
           "closeTopic": "",
           "closeQos": "0",
           "closePayload": "",
           "closeMsg": {},
           "willTopic": "",
           "willQos": "0",
           "willPayload": "",
           "willMsg": {},
           "sessionExpiry": ""
       }
   ]
   
   ```

![image.png](.attachments.243862496/image.png)with the code above we could retrive our node red

## For viewing the received and sent messages

## go on debugger

## ![image (3).png](.attachments.243862496/image%20%283%29.png)