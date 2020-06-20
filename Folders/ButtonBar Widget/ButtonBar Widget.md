# Gist of Flutter

## ButtonBar Widget

#### Code
```Java
import 'package:flutter/material.dart';

///ButtonBar Widget
///This Widget creates a ButtonBar on the ViewPort. The main property is the children, which takes a list of widgets. Any
///widget can be used as a list of children and behaviours attached to them. In this case, MaterialButton Widgets have
///been used.

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        body: ButtonBarWidget(),
      ),
    );
  }
}

class ButtonBarWidget extends StatefulWidget {
  @override
  _ButtonBarWidgetState createState() => _ButtonBarWidgetState();
}

class _ButtonBarWidgetState extends State<ButtonBarWidget> {
  int buttonIndex;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Padding(
          padding: const EdgeInsets.all(17.5),
          child: ButtonBar(
            alignment: MainAxisAlignment.center,
            buttonHeight: 30,
            buttonMinWidth: 90,
            buttonPadding: EdgeInsets.all(0),
            children: [
              for (int index = 0; index < 4; index++) ...[
                MaterialButton(
                  elevation: 10,
                  color: Colors.black,
                  shape: BeveledRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(10))),
                  onPressed: () {
                    setState(() {
                      buttonIndex = index + 1;
                    });
                  },
                  child: Padding(
                    padding: const EdgeInsets.all(10.0),
                    child: Text(
                      'Item: ${index + 1}',
                      style: TextStyle(color: Colors.white, fontSize: 16),
                    ),
                  ),
                )
              ]
            ],
          ),
        ),
        Padding(
          padding: const EdgeInsets.all(25.0),
          child: ButtonBarWidgetStatus(buttonIndex: buttonIndex),
        ),
      ],
    );
  }
}

class ButtonBarWidgetStatus extends StatefulWidget {
  final int buttonIndex;

  ButtonBarWidgetStatus({Key key, this.buttonIndex}) : super(key: key);

  @override
  _ButtonBarWidgetStatusState createState() => _ButtonBarWidgetStatusState();
}

class _ButtonBarWidgetStatusState extends State<ButtonBarWidgetStatus> {
  @override
  Widget build(BuildContext context) {
    return Container(
        child: Text(widget.buttonIndex == null ? '' : 'Button ${widget.buttonIndex} tapped',
            style: TextStyle(fontSize: 18, fontWeight: FontWeight.w500)));
  }
}
```

#### Screenshots
[ButtonBarWidget01](Screenshots/ButtonBarWidget01.png)  
[ButtonBarWidget02](Screenshots/ButtonBarWidget02.png)