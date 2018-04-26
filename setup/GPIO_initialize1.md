# GPIO Pen

### Hello, blinky!" background service
#### Section: Initialize the GPIO pin
#### https://github.com/Microsoft/Windows-iotcore-samples/blob/develop/Samples/HelloBlinkyBackground/CS/README.md
#### Accessed April 25, 2018

1. To drive the GPIO pin, first we need to initialize it. Here is the C# code (notice how we leverage the new WinRT classes in the Windows.Devices.Gpio namespace):

using Windows.Devices.Gpio;

private void InitGPIO()
{
    var gpio = GpioController.GetDefault();

    if (gpio == null)
    {
        pin = null;
        return;
    }

    pin = gpio.OpenPin(LED_PIN);

    if (pin == null)
    {
        return;
    }

    pin.Write(GpioPinValue.High);
    pin.SetDriveMode(GpioPinDriveMode.Output);
}
