# Gist of Flutter

## Responsive UI Template

#### Code
```Java
import 'package:flutter/material.dart';

///Responsive UI template

///Create the enum for device type
enum DeviceType { PC, MOBILE, TABLET, WEARABLE, UNKNOWN }

///Create a blueprint for device sizing information
class DeviceInformation {
  final Orientation orientation;
  final DeviceType deviceType;
  final Size screenSize;
  final Size localWidgetSize;
  final Brightness platformBrightness;

  DeviceInformation(
      {this.orientation, this.deviceType, this.screenSize, this.localWidgetSize, this.platformBrightness});

  ///Override the toString() method for this class for easy display in the UI (this is not compulsory).
  @override
  String toString() {
    return 'Orientation: $orientation\nDevice Type: $deviceType\nScreen Size: $screenSize\nLocal Widget Size: $localWidgetSize\nPlatform Brightness: $platformBrightness';
  }
}

///Create a base Stateless Widget. This Widget has a builder function (needed for getting the Scaffold's context - for
///MediaQueryData). This should be a required parameter in this widget. Create a SizingInformation object in the build
///method of this base widget and return a builder widget. To use this widget, wrap the child widget in it.
class DeviceInfoWidget extends StatelessWidget {
  final Widget Function(BuildContext context, DeviceInformation deviceInformation) builder;

  const DeviceInfoWidget({Key key, this.builder}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    MediaQueryData mediaQueryData = MediaQuery.of(context);

    ///To get the Layout Widget Size, wrap the builder function in a LayoutBuilder Widget with a BuildContext and
    ///BoxConstraints as parameters. Create the SizingInformation object in the LayoutBuilder Widget's builder function.
    ///In this object pass the Size function (for the current Widget's size).
    return LayoutBuilder(builder: (context, boxConstraints) {
      DeviceInformation sizingInformation = DeviceInformation(
          orientation: mediaQueryData.orientation,
          deviceType: getDeviceType(mediaQueryData),
          screenSize: mediaQueryData.size,
          ///Platform Brightness information can be used to determine the Brightness Mode of the app, which can be used
          ///as a basis for the app's default theme. 
          platformBrightness: mediaQueryData.platformBrightness,
          localWidgetSize: Size(boxConstraints.maxWidth, boxConstraints.maxHeight));
      return builder(context, sizingInformation);
    });
  }
}

///The below function is used to get device sizing and device type information
DeviceType getDeviceType(MediaQueryData mediaQueryData) {
  Orientation orientation = mediaQueryData.orientation;

  ///Creating conditional bool variables
  bool landscapeMode = orientation == Orientation.landscape;
  bool portraitMode = orientation == Orientation.portrait;

  ///Retrieve device width and height
  double deviceWidth = mediaQueryData.size.width;
  double deviceHeight = mediaQueryData.size.height;

  DeviceType deviceType;

  ///Using deviceWidth and deviceHeight, determine the type of device (based on pixel thresholds) - LandscapeMode function
  DeviceType landscapeModeFunction() {
    if (deviceWidth > deviceHeight && deviceWidth >= 1024)
      return deviceType = DeviceType.PC;
    else if (deviceWidth > deviceHeight && deviceHeight >= 415 && deviceHeight < 768)
      return deviceType = DeviceType.TABLET;
    else if (deviceWidth > deviceHeight && deviceHeight < 415)
      return deviceType = DeviceType.MOBILE;
    else if (deviceWidth > deviceHeight && deviceHeight < 320)
      return deviceType = DeviceType.WEARABLE;
    else
      return deviceType = DeviceType.UNKNOWN;
  }

  ///Using deviceWidth and deviceHeight, determine the type of device (based on pixel thresholds) - portraitMode function
  DeviceType portraitModeFunction() {
    if (deviceWidth < deviceHeight && deviceHeight >= 1024)
      return deviceType = DeviceType.PC;
    else if (deviceWidth < deviceHeight && deviceWidth >= 415)
      return deviceType = DeviceType.TABLET;
    else if (deviceWidth < deviceHeight && deviceWidth < 415 && deviceWidth > 320)
      return deviceType = DeviceType.MOBILE;
    else if (deviceWidth < deviceHeight && deviceWidth <= 320)
      return deviceType = DeviceType.WEARABLE;
    else if (deviceWidth == deviceHeight && deviceWidth <= 320)
      return deviceType = DeviceType.WEARABLE;
    else
      return deviceType = DeviceType.UNKNOWN;
  }

  ///Function call if landscapeMode
  if (landscapeMode == true) landscapeModeFunction();

  ///Function call if portraitMode
  if (portraitMode == true) portraitModeFunction();

  return deviceType;
}

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        body: Center(child: DeviceUI()),
      ),
    );
  }
}

class DeviceUI extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return DeviceInfoWidget(builder: (context, deviceInformation) {
      return Center(child: Text(deviceInformation.toString()));
    });
  }
}
```

Refer this link [https://medium.com/flutter-community/the-best-flutter-responsive-ui-pattern-ba52875d70cd](https://medium.com/flutter-community/the-best-flutter-responsive-ui-pattern-ba52875d70cd)  
Refer this link [https://material.io/resources/devices/](https://material.io/resources/devices/)  
Refer this link [https://www.responsivedesignchecker.com/](https://www.responsivedesignchecker.com/)  
Refer this link [https://mediag.com/blog/popular-screen-resolutions-designing-for-all/](https://mediag.com/blog/popular-screen-resolutions-designing-for-all/)  

#### Screenshots
[ResponsiveUI01](Screenshots/ResponsiveUI01.png)  
[ResponsiveUI02](Screenshots/ResponsiveUI02.png)  
[ResponsiveUI03](Screenshots/ResponsiveUI03.png)  
[ResponsiveUI04](Screenshots/ResponsiveUI04.png)  
[ResponsiveUI05](Screenshots/ResponsiveUI05.png)  
[ResponsiveUI06](Screenshots/ResponsiveUI06.png)  