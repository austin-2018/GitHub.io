#### DHT11 /DHT22 Temperature Sensor
#### https://www.hackster.io/porrey/dht11-dht22-temperature-sensor-077790
##### Daniel Porrey
##### Published October 6, 2015 © GPL3+
##### Accessed May 9, 2018

##### Excerpts
#### Library
#####The library I created is a simple refactoring of the code originally posted by Microsoft so I take no credit for the work done to get the sensor reading.

#### The library presents a simple *class* called *Dht11* in the *namesapace* *Sensors.Dht.* 
##### Creating a new object in C# is simple.
1. First open the GPIO pin you have the DHT11 sensor pin connected.

        using Sensors.Dht;
        GpioPin pin = GpioController.GetDefault().OpenPin(4, GpioSharingMode.Exclusive);
        
2. Then pass this pin to the constructor of the Dht11 class and specify the GPIO Pin Drive Mode. This allows you to decide whether you will add your own pull-up resistor.

        Dht11 dht11 = new Dht11(_pin, GpioPinDriveMode.Input);

3. To get a reading from the device use the GetReadingAsync method.
        DhtReading reading = await dht11.GetReadingAsync().AsTask();
        
        DhtReading reading = await dht11.GetReadingAsync().AsTask();
        
4. There is an overload that allows the maximum retry value to be specified. The default value is 20. This specifies how many attempts to make to read the sensor before giving up and returning a failed reading.

The DhtReading structure is defined as:


        public value struct DhtReading
        {
          bool TimedOut;
          bool IsValid;
          double Temperature;
          double Humidity;
          int RetryCount;
        };
