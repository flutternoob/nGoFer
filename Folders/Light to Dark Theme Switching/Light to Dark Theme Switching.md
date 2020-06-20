# Gist of Flutter

## Light to Dark Theme Switching

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Switching between Light and Dark Theme modes without using Inherited Widget and/or Provider
///To change the theme mode from a child widget, it is preferable to use either Inherited Widget or a state management
///solution such as Provider. Otherwise all theme changing has to be carried out within the parent widget.
///When switching between light and dark modes in the parent widget, call the setState() function to change the
///brightness property in the ThemeData class

///If no state management solution is used (as in this case), the app entry point widget has to be a Stateful Widget.
///There should be a more efficient way of switching between themes. Look into using Inherited Widget and Provider for
///the same.
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  Brightness brightness;
  int groupValue;
  String radioListTileSelected;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    groupValue = 0;
    brightness = Brightness.light;
  }

  ///This function is called to set the groupValue property to the value of a give RadioListTile widget and to change
  ///the value of the brightness property
  void radioListTileSelectorFunction(int radioListTileValue){
    setState(() {
      groupValue = radioListTileValue;
      if (groupValue == 1)
        brightness = Brightness.light;
      if (groupValue == 2)
        brightness = Brightness.dark;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        brightness: brightness,
        primaryColor: brightness == Brightness.light? Colors.blue[900]: Colors.black,
      ),
      home: SafeArea(
        child: Scaffold(
          appBar: AppBar(
            elevation: 10,
            title: Text('Demo App'),
            centerTitle: true,
          ),
          body: Center(
            child: Container(
              width: 250,
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    RadioListTile(
                      value: 1,
                      groupValue: groupValue,
                      title: Text('Light Theme'),
                      onChanged: (radioListTileValue) => radioListTileSelectorFunction(radioListTileValue),
                      activeColor: brightness == Brightness.light? Colors.blue[900]: Colors.black,
                    ),
                    RadioListTile(
                      value: 2,
                      groupValue: groupValue,
                      title: Text('Dark Theme'),
                      onChanged: (radioListTileValue) => radioListTileSelectorFunction(radioListTileValue),
                      activeColor: brightness == Brightness.light? Colors.blue[900]: Colors.black,
                    ),
                  ],
                ),
            ),
          ),
        ),
      ),
    );
  }
}
```

#### Screenshots
[DarkTheme](Screenshots/DarkTheme.png)  
[LightTheme](Screenshots/LightTheme.png)  