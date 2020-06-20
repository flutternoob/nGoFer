# Gist of Flutter

## SafeArea, AppBar Icons and Builder widgets

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///SafeArea, AppBar Icons and Builder widgets
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      ///To prevent intrusion into other parts of the device screen (such as the notch), wrap the Scaffold widget in a
      ///SafeArea widget.
      home: SafeArea(
        child: Scaffold(
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
            ///For a custom icon button, or any button, wrap the button in a Builder widget
            ///The Builder widget can be used anywhere in the app in cases where the Scaffold's context is not available
            ///for a given widget. This widget is especially useful when using properties such as
            ///Scaffold.of(context).someProperty, Theme.of(context).someProperty or MediaQuery.of(context).someProperty
            leading: Builder(builder: (context) {
              ///Using IconButton
              return IconButton(
                icon: Icon(
                  Icons.menu,
                  color: Colors.blue[200],
                ),
                onPressed: () {
                  print('Button pressed');
                },
              );
              ///Using FlatButton
              /*return FlatButton( 
                 child: Icon( 
                   Icons.menu, 
                   color: Colors.blue[200], 
                 ), 
                 onPressed: () { 
                   print('Button pressed'); 
                 }, 
               );*/
            }),
            ///Actions are a list of widgets that are shown on the trailing side of the AppBar's title
            actions: <Widget>[
              IconButton(
                icon: Icon(Icons.settings, color: Colors.blue[200],),
                onPressed: () {
                  print('Trailing button tapped');
                },
              ),
            ],
          ),
          body: Container(),
        ),
      ),
    );
  }
}
```

#### Screenshots

[SafeAreaAppBarIconsBuilderWidget](Screenshots/SafeAreaAppBarIconsBuilderWidget.png)