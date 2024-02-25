source : arduino VEML7700 library 

Source : <https://learn.adafruit.com/adafruit-veml7700/arduino>

```
#include <Wire.h>
#include <Adafruit_VEML7700.h>

Adafruit_VEML7700 veml;

void setup() {
  Serial.begin(9600);
  Serial.println("VEML7700 test");

  if (!veml.begin()) {
    Serial.println("Failed to communicate with VEML7700 sensor, check wiring?");
    while (1);
  }
  Serial.println("Found VEML7700 sensor");
 
  // Optional settings to configure the sensor, uncomment if needed
  // veml.setGain(VEML7700_GAIN_1);          // set gain 1x (default is 2x)
  // veml.setIntegrationTime(VEML7700_IT_100MS); // set integration time
  // veml.setPowerSaveMode(false);            // disable power save mode
  // veml.setAuto(false);                     // disable auto mode
}

void loop() {
  // Read ambient light data in lux
  float lux = veml.readLux();

  // Print lux value
  Serial.print("Ambient Light (lux): ");
  Serial.println(lux);

  delay(1000); // Wait for a second before taking another reading
}
```