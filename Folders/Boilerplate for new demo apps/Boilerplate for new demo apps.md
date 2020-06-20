# Gist of Flutter

## Boilerplate for new demo apps

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    ///MaterialApp() widget is a widget that is necessary for other widgets to conform to Material Design guidelines
    ///and it should be returned within the Widget build() method
    return MaterialApp(
      ///This property is used to disable the 'debug' banner at the top right of the screen
      debugShowCheckedModeBanner: false,
      ///The theme property is used to define the theme standard that will be used throughout the app
      ///The properties of the ThemeData() class can be called by any widget in the app using Theme.of(context).propertyName
      theme: ThemeData(

      ),
      ///The 'home' property of the MaterialApp widget is a Scaffold widget
      home: Scaffold(
        ///The Scaffold's default color can be changed using the backgroundColor property
        ///backgroundColor: Colors.white,
        ///For MaterialDesign apps, an AppBar is one of the properties of the Scaffold
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        ///The 'body' property of the Scaffold widget can be any widget, even a Stateful one
        body: Container(),
      ),
    );
  }
}
```

#### Screenshots

[Boilerplate](Screenshots/Boilerplate.png)