# Gist of Flutter

## Checkbox Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Checkbox Widget
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
          body: Center(
              child: CheckBoxWidget()
          ),
        ),
      ),
    );
  }
}

///The two main properties of the Checkbox widget are the value (which is a bool) and the onChanged() property. The value
///property can be initialized to a default state of false (or true depending on use case) and changed by using the
///onChanged() property, which takes a bool as an argument. The value property can then be set to this bool argument
///to change the state of the Checkbox widget.

class CheckBoxWidget extends StatefulWidget {
  @override
  _CheckBoxWidgetState createState() => _CheckBoxWidgetState();
}

class _CheckBoxWidgetState extends State<CheckBoxWidget> {

  bool checkboxValue;
  String textState;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    checkboxValue = false;
    textState = 'Checkbox unchecked';
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Checkbox(
          activeColor: Colors.blue[900],
            value: checkboxValue,
            onChanged: (val) {
              setState(() {
                checkboxValue = val;
                checkboxValue? textState = 'Checkbox checked': textState = 'Checkbox unchecked';
              });
            }
        ),
        Text(textState, style: TextStyle(fontSize: 20, fontWeight: FontWeight.w500),)
      ],
    );
  }
}
```

#### Screenshots

[Checkbox01](Screenshots/Checkbox01.png)  
[Checkbox02](Screenshots/Checkbox02.png)