# Gist of Flutter

## Button Widgets, Ternary Operator

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Button Widgets, Ternary operator
class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Scaffold(
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
          ),
          ///The Center widget is used to align the child widget to the center of the parent widget
          body: Center(
              child: ButtonsWidget()
          ),
        ),
      ),
    );
  }
}

///There are five main button widgets:
///1) IconButton
///2) FlatButton
///3) RaisedButton
///4) MaterialButton
///5) OutlineButton

///The ternary operator can be used to change the state of a widget from one value of a given property to another
///value of that property (for a given widget).
class ButtonsWidget extends StatefulWidget {
  @override
  _ButtonsWidgetState createState() => _ButtonsWidgetState();
}

class _ButtonsWidgetState extends State<ButtonsWidget> {

  bool isIconButtonTapped;
  bool isFlatButtonTapped;
  bool isRaisedButtonTapped;
  bool isMaterialButtonTapped;
  bool isOutlineButtonTapped;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    isIconButtonTapped = false;
    isFlatButtonTapped = false;
    isRaisedButtonTapped = false;
    isMaterialButtonTapped = false;
    isOutlineButtonTapped = false;
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceAround,
      children: <Widget>[
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('ICON BUTTON: '),
            IconButton(
              iconSize: isIconButtonTapped? 50: 40,
              color: isIconButtonTapped? Colors.green: Colors.red,
              icon: Icon(Icons.developer_mode),
              onPressed: (){
                setState(() {
                  isIconButtonTapped = !isIconButtonTapped;
                });
              },
            ),
          ],
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('FLAT BUTTON: '),
            FlatButton(
              color: isFlatButtonTapped? Colors.blue: Colors.red,
              textColor: isFlatButtonTapped? Colors.white: Colors.black,
              child: Text(isFlatButtonTapped? 'Tapped': 'Untapped'),
              onPressed: (){
                setState(() {
                  isFlatButtonTapped = !isFlatButtonTapped;
                });
              },
              shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(10)
              ),
            ),
          ],
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('RAISED BUTTON: '),
            RaisedButton(
              elevation: isRaisedButtonTapped? 10: 0,
              color: Colors.black,
              child: Text(isRaisedButtonTapped? 'Tapped': 'Untapped', style: TextStyle(color: Colors.white),),
              onPressed: (){
                setState(() {
                  isRaisedButtonTapped = !isRaisedButtonTapped;
                });
              },
            ),
          ],
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('MATERIAL BUTTON: '),
            MaterialButton(
              elevation: isMaterialButtonTapped? 10: 0,
              color: Colors.black,
              child: Text(isMaterialButtonTapped? 'Tapped': 'Untapped', style: TextStyle(color: Colors.white),),
              onPressed: (){
                setState(() {
                  isMaterialButtonTapped = !isMaterialButtonTapped;
                });
              },
              shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.all(Radius.circular(20))
              ),
            ),
          ],
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('OUTLINE BUTTON: '),
            OutlineButton(
              child: Text(isOutlineButtonTapped? 'Tapped': 'Untapped', style: TextStyle(color: Colors.black),),
              onPressed: (){
                setState(() {
                  isOutlineButtonTapped = !isOutlineButtonTapped;
                });
              },
              shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.all(Radius.circular(20))
              ),
            ),
          ],
        )
      ],
    );
  }
}
```

#### Screenshots
[Buttons01](Screenshots/Buttons01.png)  
[Buttons02](Screenshots/Buttons02.png)  