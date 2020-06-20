# Gist of Flutter

## Switch Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Switch Widget
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
              child: SwitchWidget()
          ),
        ),
      ),
    );
  }
}

///The two main properties of the Switch widget are the value (which is a bool) and the onChanged() property. The value
///property can be initialized to a default state of false (or true depending on use case) and changed by using the
///onChanged() property, which takes a bool as an argument. The value property can then be set to this bool argument
///to change the state of the Switch widget.

class SwitchWidget extends StatefulWidget {
  @override
  _SwitchWidgetState createState() => _SwitchWidgetState();
}

class _SwitchWidgetState extends State<SwitchWidget> {

  bool switchValue;
  String textState;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    switchValue = false;
    textState = 'Switch off';
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        ///The width of the Switch widget can be changed by wrapping it in a Container widget of a given width
        Container(
          width: 75,
          child: Switch(
            activeColor: Colors.blue[900],
            activeTrackColor: Colors.blue[200],
            inactiveThumbColor: Colors.grey[700],
            value: switchValue,
            onChanged: (val){
              setState(() {
                switchValue = val;
                if(switchValue == true)
                  textState = 'Switch on';
                else
                  textState = 'Switch off';
              });
            },
          ),
        ),
        Text(textState, style: TextStyle(fontSize: 20, fontWeight: FontWeight.w500),)
      ],
    );
  }
}
```

#### Screenshots
[SwitchWidget01](Screenshots/SwitchWidget01.png)  
[SwitchWidget02](Screenshots/SwitchWidget02.png)