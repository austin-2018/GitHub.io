#### C# implementation of MS5637 sensor with I2C on IoT
##### https://raspberrypi.stackexchange.com/questions/41726/c-implementation-of-ms5637-sensor-with-i2c-on-iot
```using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;
using Windows.Devices.Enumeration;
using Windows.Devices.I2c;

namespace MS5637
{
    /*
        This class was written by:  Curtis V. Harrison - curtiscode@gmail.com
        You can use it all you want, just be nice and keep my name at the top of the file.

        Sample code for using the 'Windows.Devices.I2c.I2cDevice' can be found at:
        https://ms-iot.github.io/content/en-US/win10/samples/I2CAccelerometer.htm

        Data Sheet for MS5637 can be found at:
        http://www.farnell.com/datasheets/1756129.pdf
    */

    /// <summary>
    /// MS5637Device class usage
    /// This class is simple to use:
    /// 
    /// 1.  Create an instance using the default no param constructor, or provide a Slave Address
    ///     The constructors will initialize the sensor and prepare it data retrieval
    /// 2.  Call 'GetTemperaturePressure()' and you will receive a 'TemperaturePressure' object.
    ///     Temperature is in 'farenheit' and pressure is in 'mbars';
    /// 3.  Use the 'Temperature' or 'Pressure' properties of the TemperaturePressure object as you like.
    /// 4.  Whenever you need updated Temperature or pressure, follow instruction 2 above..
    /// </summary>
    public class MS5637Device : IDisposable
    {
        private const int MS5637_SLAVE_ADDRESS = 0x76;
        private static readonly byte[] MS5637_RESET_COMMAND = {0x1E};
        private static readonly byte[] MS5637_COEFFICENTS_COMMAND = {0xA0};
        private static readonly byte[] MS5637_COEFFICENTS_END_COMMAND = {0xAE};
        private static readonly byte[] MS5637_HI_RES_TEMPERATURE = {0x5A};
        private static readonly byte[] MS5637_HI_RES_PRESSURE = {0x4A};
        private static readonly byte[] MS5637_DATA_READ_COMMAND = {0x00};

        private I2cDevice Sensor { get; set; }
        private List<ushort> Coefficients { get; set; }
        private double Temperature { get; set; }
        private double Pressure { get; set; }

        /// <summary>
        /// Default constructor requires no arguments.
        /// This constructor assumes a SlaveAddress of 0x76 for the MS5637 sensor.
        /// Constructing this object will initialize it and prepare it for data retrieval.
        /// </summary>
        public MS5637Device() : this(MS5637_SLAVE_ADDRESS)
        {
        }

        /// <summary>
        /// Constructor requires a single byte 'SlaveAddress' as an argument.
        /// The typical SlaveAddress for the MS5637 sensor is 0x76.
        /// Constructing this object will initialize it and prepare it for data retrieval.
        /// </summary>
        public MS5637Device(byte slaveAddress)
        {
            Init(slaveAddress);
        }

        /// <summary>
        /// Call this method whenever you want to get current Temperature and Pressure values.
        /// This method returns a 'TemperaturePressure' object which in turn has a Temperature and a Pressure
        /// property.
        /// </summary>
        /// <returns></returns>
        public TemperaturePressure GetTemperaturePressure()
        {
            try
            {
                GetD1D2();
            }
            catch
            {
                SpinWait.SpinUntil(() => false, 500);
                Sensor.Write(MS5637_RESET_COMMAND); //Reset Device
                SpinWait.SpinUntil(() => false, 10);
                Debug.WriteLine("BOOM !!!  CRASH !!!  RESET !!!");
            }

            return new TemperaturePressure(Temperature, Pressure);
        }

        private void Init(int slaveAddress)
        {
            InitSensor(slaveAddress).Wait();

            byte[] command = new byte[1];
            Sensor.Write(MS5637_RESET_COMMAND); //Reset Device
            SpinWait.SpinUntil(() => false, 10);

            Coefficients = new List<ushort>();
            byte[] coefficent = new byte[2];

            for (command[0] = MS5637_COEFFICENTS_COMMAND[0];
                command[0] < MS5637_COEFFICENTS_END_COMMAND[0];
                command[0] += 2)
            {
                coefficent[0] = 0;
                coefficent[1] = 0;
                Sensor.WriteRead(command, coefficent);
                Coefficients.Add((ushort)(coefficent[0] << 8 | coefficent[1]));
                SpinWait.SpinUntil(() => false, 50);
            }

            GetTemperaturePressure();
        }

        private async Task InitSensor(int slaveAddress)
        {
            var settings = new I2cConnectionSettings(slaveAddress) {BusSpeed = I2cBusSpeed.FastMode};
            string aqs = I2cDevice.GetDeviceSelector();
            var dis = await DeviceInformation.FindAllAsync(aqs);
            Sensor = await I2cDevice.FromIdAsync(dis[0].Id, settings);
        }

        private uint ConvertBytesToInt32(byte[] data)
        {
            uint value = ((uint)data[0] << 16) | (uint)data[1] << 8 | data[2];
            return value;
        }

        private void GetD1D2()
        {
            byte[] d1PressureBytes = new byte[3];
            Sensor.Write(MS5637_HI_RES_PRESSURE);
            SpinWait.SpinUntil(() => false, 30);
            Sensor.WriteRead(MS5637_DATA_READ_COMMAND, d1PressureBytes);
            uint D1 = ConvertBytesToInt32(d1PressureBytes);

            byte[] d2TemperatureBytes = new byte[3];
            Sensor.Write(MS5637_HI_RES_TEMPERATURE);
            SpinWait.SpinUntil(() => false, 30);
            Sensor.WriteRead(MS5637_DATA_READ_COMMAND, d2TemperatureBytes);
            uint D2 = ConvertBytesToInt32(d2TemperatureBytes);

            CalculateTemperaturePressure(D1, D2);
        }

        private void CalculateTemperaturePressure(uint D1, uint D2)
        {
            var dT = D2 - Coefficients[5] * Math.Pow(2, 8);
            var offset = Coefficients[2]*Math.Pow(2, 17) + (dT*Coefficients[4])/Math.Pow(2, 6);
            var sensitivity = Coefficients[1]*Math.Pow(2, 16) + (dT*Coefficients[3])/Math.Pow(2, 7);
            var t1 = (2000 + (dT * Coefficients[6]) / Math.Pow(2, 23)) / 100;
            //Assume temperature is > 20 celsus inside somebody's home
            var t2 = 5 * Math.Pow(dT, 2) / Math.Pow(2, 38);
            t1 -= t2;

            Temperature = t1 * 1.8 + 32;
            Pressure = (D1*sensitivity/Math.Pow(2, 21) - offset)/Math.Pow(2, 15)/100;
        }

        /// <summary>
        /// Disposes the internal Sensor object when Dispose() is called on this object.
        /// </summary>
        public void Dispose()
        {
            if (Sensor != null)
            {
                Sensor.Dispose();
                Sensor = null;
            }
        }
    }

    /// <summary>
    /// This is a simple container class which allows for a Temperature and a Pressure
    /// to be stored and passed.
    /// </summary>
    public class TemperaturePressure
    {
        public double Temperature { get; set; }
        public double Pressure { get; set; }

        public TemperaturePressure(double temperature, double pressure)
        {
            Temperature = temperature;
            Pressure = pressure;
        }
    }
}
