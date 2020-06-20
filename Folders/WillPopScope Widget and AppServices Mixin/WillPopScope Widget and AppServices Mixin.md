# Gist of Flutter

## WillPopScope Widget and AppServices Mixin

#### Code
```Java
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

///WillPopScope Widget, AppServices Mixin
///The WillPopScope Widget is used to control the behaviour of the app's interaction with the device's back button. The
///main property is the onWillPop property that uses an anonymous function which returns a Future.value, which in turn
///takes a future bool value. If this bool value is set to false, the device's back button cannot be used. As per the
///documentation, this Widget registers a callback to veto attempts by the user to dismiss the enclosing ModalRoute.
///The AppServices Mixin is a custom mixin that can be used to set the SystemChrome settings and control the device GUI
///buttons depending on use case for a given app. For best results, the methods pertaining to the
///SystemChrome.setSystemUIOverlayStyle constructor should be used in the root Widget (in this case the MyApp() Widget).
///The methods pertaining to the SystemChrome.setPreferredOrientations can be used any where in the app depending on the
///required orientation for the app (for a given screen).

void main() => runApp(MyApp());

class MyApp extends StatelessWidget with AppServicesMixin{
  @override
  Widget build(BuildContext context) {
    //systemChromeSettingsCustom();
    //systemChromeSettingsDark();
    //systemChromeSettingsLight();
    //landscapeModeFunction();
    //portraitModeFunction();
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: WillPopScope(
        onWillPop: () => Future.value(false),
        child: Scaffold(
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
          ),
          body: Container(),
        ),
      ),
    );
  }
}

///This mixin is used to set the SystemChrome settings depending on use case for the app.
mixin AppServicesMixin {
  ///Function to set the preferred device orientation to landscape mode
  landscapeModeFunction() {
    SystemChrome.setPreferredOrientations([DeviceOrientation.landscapeLeft, DeviceOrientation.landscapeRight]);
  }

  ///Function to set the preferred device orientation to portrait mode
  portraitModeFunction() {
    SystemChrome.setPreferredOrientations([DeviceOrientation.portraitUp, DeviceOrientation.portraitDown]);
  }

  ///The device's GUI buttons that interact with the app are set to dark
  systemChromeSettingsDark() {
    SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle.dark,
    );
  }

  ///The device's GUI buttons that interact with the app are set to light
  systemChromeSettingsLight() {
    SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle.light,
    );
  }

  ///Custom settings for the GUI buttons that interact with the app
  systemChromeSettingsCustom() {
    SystemChrome.setSystemUIOverlayStyle(
      SystemUiOverlayStyle(
          statusBarColor: Colors.blue[900],
          statusBarBrightness: Brightness.light,
          systemNavigationBarColor: Colors.blue[900],
          systemNavigationBarIconBrightness: Brightness.light),
    );
  }
}
```

#### Screenshots
[WillPopScopeWidgetAppServicesMixin01](Screenshots/WillPopScopeWidgetAppServicesMixin01.png)  
[WillPopScopeWidgetAppServicesMixin02](Screenshots/WillPopScopeWidgetAppServicesMixin02.png)  
[WillPopScopeWidgetAppServicesMixin03](Screenshots/WillPopScopeWidgetAppServicesMixin03.png)