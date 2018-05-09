#### Raspberry Pi: Measure Humidity and Temperature with DHT11/DHT22
#### https://tutorials-raspberrypi.com/raspberry-pi-measure-humidity-temperature-dht11-dht22/

First of all, some packages have to be installed:

sudo apt-get update
sudo apt-get install build-essential python-dev python-openssl git
Now the library for the sensors can be loaded. I use a pre-built Adafruit library that supports a variety of sensors:

git clone https://github.com/adafruit/Adafruit_Python_DHT.git && cd Adafruit_Python_DHT
sudo python setup.py install
This creates a Python library that we can easily integrate into our projects.

If everything went well, we can already read the temperature and humidity. The easiest way is to first use the demo files:

cd examples
sudo ./AdafruitDHT.py 11 4
The first parameter (11) indicates which sensor was used (22 for the DHT22) and the second, to which GPIO it is connected (not the pin number, but the GPIO number). This produces an output like the following:

$ sudo ./AdafruitDHT.py 11 4
Temp=24.0*  Humidity=41.0%
Attention: The sensors are only ready every two seconds. Be careful not to start a query every second.
