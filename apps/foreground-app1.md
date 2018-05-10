#### Developing foreground applications
#### https://docs.microsoft.com/en-us/windows/iot-core/develop-your-app/BuildingAppsForIoTCore

#### EXCERPT
#### Traditional UWP Apps
##### UWP apps just work on IoT Core, just as they do on other Windows 10 editions. A simple, blank Xaml app in Visual Studio will properly deploy to your IoT Core device just as it would on a phone or Windows 10 PC. All of the standard UWP languages and project templates are fully supported on IoT Core.

##### There are a few additions to the traditional UWP app-model to support IoT scenarios and any UWP app that takes advantage of them will need the corresponding information added to their manifest. In paticular the "iot" namespace needs to be added to the manifest of these standard UWP apps.

##### Inside the attribute of the manifest, you need to define the iot xmlns and add it to the IgnorableNamespaces list. The final xml should look like this:
        <Package
          xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
          xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
          xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
          xmlns:iot="http://schemas.microsoft.com/appx/manifest/iot/windows10"
          IgnorableNamespaces="uap mp iot">
