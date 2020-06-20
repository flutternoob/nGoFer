# Gist of Flutter

## Container, Opacity, Material and Wrap Widgets

#### Code
```Java
import 'package:flutter/material.dart';
import 'dart:math';

void main() => runApp(MyApp());

///Container, Opacity, Material and Wrap Widgets
///A container is a widget that contains its child widget
///A Wrap widget is used to wrap the widgets either horizontally (like a row) or vertically (like a Column)
///If the number of widgets that can be visible in the viewport exceeds the viewport's size, the Wrap widget will
///move the widgets to a new row or column, depending on the Wrap widget's 'direction' property
///The Material Widget can be used to apply basic Material Design properties (such as color and text style) to the
///Material widget's child
///The Opacity widget is used to apply some level of opacity to its child widget. The opacity value overrides the
///blend mode of its child (like for a Container widget), if set to a value other than 1. The opacity value is a double
///and ranges from 0 - 1.
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        body: Center(child: ContainerWidget()),
      ),
    );
  }
}

class ContainerWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Wrap(
        direction: Axis.vertical,
        ///Spacing property is for the spacing between widgets along the main axis of the Axis direction property
        spacing: 50,
        ///runSpacing property is for the spacing between widgets along the cross axis of the Axis direction property
        runSpacing: 50,
        runAlignment: WrapAlignment.spaceEvenly,
        children: <Widget>[
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
              color: Colors.blue[900],
            ),
          ),
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
                gradient: RadialGradient(
                  colors: [Colors.black, Colors.blue[700], Colors.black],
                )
            ),
          ),
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
                shape: BoxShape.circle,
                gradient: SweepGradient(
                    colors: [Colors.black, Colors.blue[700], Colors.black],
                    startAngle: 0,
                    endAngle: pi*2
                )
            ),
          ),
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
                shape: BoxShape.rectangle,
                gradient: LinearGradient(
                    colors: [Colors.black, Colors.blue[700], Colors.black],
                    begin: Alignment.topCenter,
                    end: Alignment.bottomCenter
                )
            ),
          ),
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
                shape: BoxShape.rectangle,
                gradient: LinearGradient(
                    colors: [Colors.black, Colors.blue[700], Colors.black],
                    begin: Alignment.topCenter,
                    end: Alignment.bottomCenter
                ),
                ///To apply radius to a particular corner/s use BorderRadius.only constructor
                borderRadius: BorderRadius.only(
                    topLeft: Radius.circular(20),
                    bottomRight: Radius.circular(20)
                ),
                border: Border.all(
                  color: Colors.deepOrange,
                  width: 4,
                )
            ),
          ),
          Container(
            width: 100,
            height: 100,
            decoration: BoxDecoration(
                shape: BoxShape.rectangle,
                gradient: LinearGradient(
                    colors: [Colors.black, Colors.blue[700], Colors.black],
                    begin: Alignment.topCenter,
                    end: Alignment.bottomCenter
                ),
                borderRadius: BorderRadius.all(Radius.circular(20)),
                boxShadow: [
                  BoxShadow(
                    offset: Offset(5, 5),
                    color: Colors.black45,
                    blurRadius: 2,
                    //spreadRadius: 2
                  )
                ],
                backgroundBlendMode: BlendMode.luminosity
            ),
          ),
          Material(
            elevation: 10,
            borderRadius: BorderRadius.all(Radius.circular(20)),
            color: Colors.black,
            shadowColor: Colors.black,
            child: Container(
              width: 100,
              height: 100,
              decoration: BoxDecoration(
                  shape: BoxShape.rectangle,
                  gradient: LinearGradient(
                      colors: [Colors.black, Colors.blue[700], Colors.black],
                      begin: Alignment.topCenter,
                      end: Alignment.bottomCenter
                  ),
                  borderRadius: BorderRadius.all(Radius.circular(20)),
                  backgroundBlendMode: BlendMode.luminosity
              ),
            ),
          ),
          Material(
            elevation: 10,
            borderRadius: BorderRadius.all(Radius.circular(20)),
            color: Colors.black,
            shadowColor: Colors.black,
            ///The Opacity widget overrides the blend mode of the Container (if set to a value other than 1)
            child: Opacity(
              opacity: 0.5,
              child: Container(
                width: 100,
                height: 100,
                decoration: BoxDecoration(
                    shape: BoxShape.rectangle,
                    gradient: LinearGradient(
                        colors: [Colors.black, Colors.blue[700], Colors.black],
                        begin: Alignment.topCenter,
                        end: Alignment.bottomCenter
                    ),
                    borderRadius: BorderRadius.all(Radius.circular(20)),
                    backgroundBlendMode: BlendMode.luminosity
                ),
              ),
            ),
          ),
          Container(
            child: Material(
              elevation: 10,
              borderRadius: BorderRadius.all(Radius.circular(20)),
              color: Colors.transparent,
              shadowColor: Colors.blue,
              ///The Opacity widget overrides the blend mode of the Container (if set to a value other than 1)
              child: Container(
                width: 100,
                height: 100,
                decoration: BoxDecoration(
                  shape: BoxShape.rectangle,
                  gradient: LinearGradient(
                      colors: [Colors.black, Colors.blue[700], Colors.black],
                      begin: Alignment.topCenter,
                      end: Alignment.bottomCenter
                  ),
                  borderRadius: BorderRadius.all(Radius.circular(20)),
                ),
              ),
            ),
            transform: Matrix4.skewX(0.4)..rotateY(pi/12),
          ),
        ]
    );
  }
}
```

#### Screenshots

[ContainerOpacityMaterialWrapWidgets](Screenshots/ContainerOpacityMaterialWrapWidgets.png)