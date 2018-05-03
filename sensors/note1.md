#### source file | https://www.hackster.io/porrey/dht11-dht22-temperature-sensor-077790

### Library
##### The library I created is a simple refactoring of the code originally posted by Microsoft so I take no credit for the work done to get the sensor reading.

##### The library presents a simple class called Dht11 in the namesapace Sensors.Dht. 

1. First open the GPIO pin you have the DHT11 sensor pin connected.
1. **using Sensors.Dht;GpioPin pin = GpioController.GetDefault().OpenPin(4, GpioSharingMode.Exclusive);**
