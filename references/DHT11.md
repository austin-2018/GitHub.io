# Temperature Sensor DHT11

If you are testing with the C# code don't forget to change the line:

_dht = new Dht11(_pin, GpioPinDriveMode.Input);

to use the Dht22 instead:

_dht = new Dht22(_pin, GpioPinDriveMode.Input);

##### Above code from:
#### https://microsoft.hackster.io/en-US/porrey/dht11-dht22-temperature-sensor-077790

Library
The library I created is a simple refactoring of the code originally posted by Microsoft so I take no credit for the work done to get the sensor reading.

The library presents a simple class called Dht11 in the namesapace Sensors.Dht. Creating a new object in C# is simple.

First open the GPIO pin you have the DHT11 sensor pin connected.
using Sensors.Dht;GpioPin pin = GpioController.GetDefault().OpenPin(4, GpioSharingMode.Exclusive);

##### Above code from:
#### https://www.hackster.io/porrey/dht11-dht22-temperature-sensor-077790

#### Temperature Sensor for Windows 10 IoT Core
#### https://jev-pankov.com/2017/08/24/temperature-sensor-for-windows-10-iot-core/

#### DHT11 (Raspberry Pi)
#### https://www.youtube.com/watch?v=KUr8WgSIsfk
##### https://github.com/szazo/DHT11_Python
