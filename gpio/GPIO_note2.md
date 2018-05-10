#### Windows.Devices.Gpio Namespace
#### https://docs.microsoft.com/en-us/uwp/api/Windows.Devices.Gpio

##### Excerpts as accessed May 9, 2018

##### Windows.Devices.Gpio Namespace
##### Assemblies:
##### Windows.Devices.Gpio.dll, Windows.dll

##### Contains types for using general-purpose I/O (GPIO) pins in user mode.

##### Classes 
##### GpioChangeCounter	
##### Counts changes of a specified polarity on a general-purpose I/O (GPIO) pin.

##### GpioChangeReader	
##### Represents a shared circular buffer between kernel mode and user mode into which high-resolution timestamps are placed when a general-purpose I/O (GPIO) pin changes value.

##### GpioController	
##### Represents the d efault general-purpose I/O (GPIO) controller for the system.

##### GpioPin	
##### Represents a general-purpose I/O (GPIO) pin.

##### GpioPinValueChangedEventArgs	
##### Provides data about the GpioPin.ValueChanged event that occurs when the value of the general-purpose I/O (GPIO) pin changes, either because of an external stimulus when the pin is configured as an input, or when a value is written to the pin when the pin in c onfigured as an output.

##### Structs 
##### GpioChangeCount	
##### Represents a near-simultaneous sampling of the number of times a pin has changed value, and the time at which this count was sampled. This structure can be used to determine the number of pin value changes over a period of time.

##### GpioChangeRecord	
##### Stores a relative timestap of a general-purpose I/O (GPIO) pin value change, and whether the pin transitioned from low to high or from high to low.

##### Enums  
##### GpioChangePolarity	
##### Represents the polarity of changes that are relevant to the associated action.

##### GpioOpenStatus	
##### Describes the possible results of opening a pin with the GpioPin.TryOpenPin method.

##### GpioPinDriveMode	
##### Describes whether a general-purpose I/O (GPIO) pin is configured as an input or an output, and how values are driven onto the pin.

##### GpioPinEdge	
##### Describes the possible types of change that can occur to the value of the general-purpose I/O (GPIO) pin for the GpioPin.ValueChanged event.

##### pioPinValue	
##### Describes the possible values for a general-purpose I/O (GPIO) pin.

##### GpioSharingMode	
##### Describes the modes in which you can open a general-purpose I/O (GPIO) pin. These modes determine whether other connections to the GPIO pin can be opened while you have the pin open.
