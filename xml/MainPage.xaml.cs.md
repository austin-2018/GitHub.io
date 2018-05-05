#### Internet of Things - Working with Raspberry Pi and Windows 10
#### https://msdn.microsoft.com/en-us/magazine/mt808503.aspx

##### Excerpt

```Once you do that, you’ll have the tools installed and you can start developing for the Raspberry Pi using Windows 10. Create a new project and select the “Blank” UWP app.```

```This will create a blank app and you’ll create an app that shows the name of the current machine in the main screen. In Main­Page.xaml, add the following code:```
         <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
          <TextBlock FontSize="32" x:Name="MachineText"
            HorizontalAlignment="Center"
            VerticalAlignment="Center"/>
        </Grid>
