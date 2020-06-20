# Gist of Flutter

## Device Info using MediaQuery

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Getting basic device information using MediaQuery
///The size property of the MediaQuery class uses logical pixels. To calculate the device resolution, multiply the
///logical pixels by the device pixel ratio
class MyApp extends StatelessWidget {
  String appTitle;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Builder(builder: (BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              elevation: 10,
              backgroundColor: Colors.blue[900],
              title: Text('Demo App'),
              centerTitle: true,
            ),
            body: Center(child: MediaQueryWidget()),
          );
        }),
      ),
    );
  }
}

class MediaQueryWidget extends StatefulWidget {
  @override
  _MediaQueryWidgetState createState() => _MediaQueryWidgetState();
}

class _MediaQueryWidgetState extends State<MediaQueryWidget> {
  @override
  Widget build(BuildContext context) {
    ///Get the size in logical pixels
    Size size = MediaQuery.of(context).size;

    ///Get the device orientation
    Orientation orientation = MediaQuery.of(context).orientation;

    ///Get the device pixel ratio
    double devicePixelRatio = MediaQuery.of(context).devicePixelRatio;

    ///Get the device display mode
    Brightness deviceBrightness = MediaQuery.of(context).platformBrightness;
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        Text(
          'Logical Pixels:\nWidth: ${(size.width).toStringAsPrecision(5)}, Height: ${(size.height).toStringAsPrecision(5)}',
          textAlign: TextAlign.center,
        ),
        Text(
          'Resolution:\nWidth: ${(size.width) * devicePixelRatio}, Height: ${(size.height) * devicePixelRatio}',
          textAlign: TextAlign.center,
        ),
        Text(
          'Current Device Orientation:\n${orientation == Orientation.portrait ? 'Portrait Mode' : 'Landscape Mode'}',
          textAlign: TextAlign.center,
        ),
        Text(
          'Device Pixel Ratio: $devicePixelRatio',
          textAlign: TextAlign.center,
        ),
        Text(
          'Device Display Mode:\n${deviceBrightness == Brightness.light ? 'Light Mode' : 'Dark Mode'}',
          textAlign: TextAlign.center,
        ),
      ],
    );
  }
}
```

Refer this link [https://stackoverflow.com/questions/8785643/what-exactly-is-device-pixel-ratio](https://stackoverflow.com/questions/8785643/what-exactly-is-device-pixel-ratio)  
Refer this link [https://api.flutter.dev/flutter/widgets/MediaQueryData-class.html](https://api.flutter.dev/flutter/widgets/MediaQueryData-class.html)

#### Screenshots

[DeviceInfoMediaQuery01](Screenshots/DeviceInfoMediaQuery01.png)  
[DeviceInfoMediaQuery02](Screenshots/DeviceInfoMediaQuery02.png)