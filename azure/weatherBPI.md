### Using Power BI to Visualize Sensor Data from Windows 10 IoT Core
#### https://blogs.msdn.microsoft.com/iot/2016/01/26/using-power-bi-to-visualize-sensor-data-from-windows-10-iot-core/

### IMPORTANT NOTES

##### Authenticating a Headless Device
In a typical OAuth 2.0 authorization flow, the user is presented with a browser window where they can enter their credentials. The application then obtains an access token that is used to communicate with the desired cloud service. Alas, this approach is not suitable for headless IoT devices without the mouse and keyboard attached, or devices that only offer console I/O.

This problem is solved with the latest version of the Active Directory Authentication Library (still in preview) that introduces a new authentication flow tailored for headless devices. The approach goes like this: when a user authentication is required, instead of bringing up a browser window, the app asks the user to use another device to navigate to https://aka.ms/devicelogin and enter a specific code. Once the code is provided, the web page will lead the user through a normal authentication experience, including consent prompts and multi factor authentication if necessary. Upon successful authentication, the app will receive the required access tokens through a back channel and use it to access the desired cloud service.

### Registering an Application in Azure
This step assumes that your organization already has an Azure Active Directory set up. If not, you can get started here.

You can register your application from the Azure Portal, however it's easier to do it from the dedicated Power BI application registration page: https://dev.powerbi.com/apps.

Navigate to the above page, log in with your Power BI credentials and fill out the information about your app:
