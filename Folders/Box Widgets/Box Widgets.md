# Gist of Flutter

## Box Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///Box Widgets
///ConstrainedBox Widget - If the child is bigger than the parent widget's size, the ConstrainedBox widget can be used to
///constrain the size of the child to the parent widget
///FittedBox Widget - To show the child fully in the parent, with constraints, and to prevent clipping of the child, use
///a FittedBox Widget. It can also be used when the size and legibility of the child is not important.
///FractionallySizedBox - This widget is used to set the size of the child in to a fraction of the available space in the
///parent Widget.
///LimitedBox Widget - In an unconstrained environment, such as a ListView, the LimitedBox Widget can be used to give a
///size to its child widget.
///SizedBox Widget - Used to create a box of fixed dimensions.

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
        body: Center(child: BoxWidgets()),
      ),
    );
  }
}

class BoxWidgets extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceAround,
      children: [
        ///ConstrainedBox
        Container(
          color: Colors.black,
          child: ConstrainedBox(
            constraints: BoxConstraints(minHeight: 50),
            child: Icon(
              Icons.music_video,
              size: 80,
              color: Colors.blue,
            ),
          ),
        ),
        ///FittedBox
        FittedBox(
          fit: BoxFit.contain,
          child: Text(
            'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout.',
            maxLines: 1,
            style: TextStyle(fontSize: 16),
          ),
        ),
        ///FractionallySizedBox - size of the child is determined using the width and height factor (as a double from 0
        ///to 1) based on the parent widget's size.
        Container(
          width: 350,
          height: 50,
          child: FractionallySizedBox(
            widthFactor: 0.9,
            heightFactor: 0.9,
            child: Container(
              decoration: BoxDecoration(
                color: Colors.green[900]
              ),
            )
          ),
        ),
        ///LimitedBox - check further on how to use it
        LimitedBox(
          maxHeight: 50,
          maxWidth: 50,
          child: Container(
            color: Colors.blue[900],
          ),
        ),
        SizedBox(
          width: 100,
          height: 100,
          child: Container(
            color: Colors.black
          ),
        )
      ],
    );
  }
}
```

##### Refer this link [https://medium.com/@pinkesh.earth/top-5-flutter-box-widgets-you-should-know-f86d8e02d86b](https://medium.com/@pinkesh.earth/top-5-flutter-box-widgets-you-should-know-f86d8e02d86b)

#### Screenshots

[BoxWidgets](Screenshots/BoxWidgets01.png)