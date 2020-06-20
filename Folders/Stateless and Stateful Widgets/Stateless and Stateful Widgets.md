# Gist of Flutter

## Stateless and Stateful Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///The main() function is the entry point of a Flutter application. It calls the runApp() function which uses a widget
///as an argument
void main() => runApp(AStatelessWidget());

///Boilerplate for Stateless Widget and Stateful widget
///A Stateless widget is a widget whose state does not change based on user interaction
class AStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}

///A StatefulWidget is a widget whose state changes based on user interaction
///There are six main aspects to Stateful Widget:
///1) The widget itself that has a createState() function which creates the Stateful Widget state
///2) The widget's state inherits from the widget itself
///3) An overridden initState() function that initializes the default state of the widget when the widget is built for the first time
///4) A setState((){}) function that is used to set the state of widgets used within the Stateful widget
///5) An overridden dispose() function that is used to dispose the states of any controllers, streams and/or subscription services
///used in the stateful widget. This function should be called to avoid unnecessary device resources
///6) A Widget build(BuildContext context) method that builds the Stateful Widget using other widgets
///setState((){}) can be used anywhere in the Stateful widget (such as in the initState() method or a button action)
///The above methods and functions are implemented in the Stateful Widget's state class
class AStatefulWidget extends StatefulWidget {
  @override
  _AStatefulWidgetState createState() => _AStatefulWidgetState();
}

class _AStatefulWidgetState extends State<AStatefulWidget> {

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    setState(() {
      //TODO: implement setState
    });
  }

  @override
  void dispose() {
    // TODO: implement dispose
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```