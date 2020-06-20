# Gist of Flutter

## Tooltip Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Tooltip Widget
///The Tooltip Widget is used to give its child Widget a Tooltip. Different styles can be applied to the Tooltip Widget.
///The two main properties are the message (which is of the type String) and the preferBelow property which can be used
///to set the appearance of the Tooltip Widget either above or below its child widget. The Tooltip Widget is shown when
///its child is long pressed.

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
            child: TooltipWidget(),
          ),
        ),
      ),
    );
  }
}

class TooltipWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Tooltip(
        ///This the message that the Tooltip widget displays when its child is long pressed
        message: 'Tooltip Widget',
          ///The Tooltip widget is shown above its child Widget
          preferBelow: false,
          textStyle: TextStyle(color: Colors.white, fontSize: 16),
          decoration: BoxDecoration(
            color: Colors.black26,
            boxShadow: [
              BoxShadow(
                color: Colors.black26,
                offset: Offset(4, 4),
                blurRadius: 2
              )
            ]
          ),
          ///The showDuration property is used to set the duration for which the tooltip is shown
          showDuration: Duration(seconds: 1),
          child: Text('What\'s this demo about?', style: TextStyle(fontSize: 18),),
      ),
    );
  }
}
```

#### Screenshots
[TooltipWidget](Screenshots/TooltipWidget.png)  