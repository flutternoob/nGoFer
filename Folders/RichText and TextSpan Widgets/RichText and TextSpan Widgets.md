# Gist of Flutter

## RichText and TextSpan Widgets

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///RichText and TextSpan Widgets
///As an alternative to using Rows and Columns to arrange differently styled text, a RichText Widget can be used. The
///two main property of the RichText Widget is the text property. The text property accepts an InlineSpan as a child (
///which is a TextSpan widget). As the name suggests an inline span refers to text that has to be displayed in a single
///line with different styles.

///Either a single InlineSpan TextSpan can be passed to the RichText Widget or multiple TextSpan widgets can be used.
///The main properties of the TextSpan Widget are the text and style properties. The style property is used to define
///the style that is to be used for the TextSpan Widget's style. The text property requires a String or another TextSpan
///Widget to be passed to it. The TextSpan widget itself can be used to pass a list of TextSpan widgets to its text
///property.

class MyApp extends StatelessWidget {
  String appTitle;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Builder(builder: (BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              elevation: 10,
              backgroundColor: Colors.blue[900],
              title: Text('Demo App'),
              centerTitle: true,
            ),
            body: Center(child: RichTextWidget()),
          );
        }),
      ),
    );
  }
}

class RichTextWidget extends StatefulWidget {
  @override
  _RichTextWidgetState createState() => _RichTextWidgetState();
}

class _RichTextWidgetState extends State<RichTextWidget> {

  ///TextStyles for the TextSpan Widgets
  TextStyle staticText = TextStyle(
      color: Colors.lightBlue, fontSize: 20, fontWeight: FontWeight.w700, shadows: [
        Shadow(
          color: Colors.black26,
          offset: Offset(3, 3),
          blurRadius: 2,
        )
  ]);
  TextStyle deviceText = TextStyle(color: Colors.black, fontSize: 18, fontWeight: FontWeight.w500, shadows: [
    Shadow(
      color: Colors.black26,
      offset: Offset(3, 3),
      blurRadius: 2,
    )
  ]);

  @override
  Widget build(BuildContext context) {
    ///Retrieving device information using MediaQueryData class
    Size size = MediaQuery.of(context).size;
    Orientation orientation = MediaQuery.of(context).orientation;
    double devicePixelRatio = MediaQuery.of(context).devicePixelRatio;
    Brightness deviceBrightness = MediaQuery.of(context).platformBrightness;
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        ///Using the RichText and TextSpan Widgets to display device information
        RichText(
          textAlign: TextAlign.center,
          text: TextSpan(children: [
            TextSpan(text: 'Logical Pixels:\n', style: staticText),
            TextSpan(
                text: 'Width: ${(size.width).toStringAsPrecision(5)}, Height: ${(size.height).toStringAsPrecision(5)}',
                style: deviceText),
          ]),
        ),
        RichText(
          textAlign: TextAlign.center,
          text: TextSpan(
              children: [
                TextSpan(text: 'Device Pixel Ratio:', style: staticText),
                TextSpan(
                    text: ' $devicePixelRatio',
                    style: deviceText),
              ]),
        ),
        RichText(
          textAlign: TextAlign.center,
          text: TextSpan(
              children: [
                TextSpan(text: 'Resolution:\n', style: staticText),
                TextSpan(
                    text: 'Width: ${(size.width) * devicePixelRatio}, Height: ${(size.height) * devicePixelRatio}',
                    style: deviceText),
              ]),
        ),
        RichText(
          textAlign: TextAlign.center,
          text: TextSpan(
              children: [
                TextSpan(text: 'Current Device Orientation:\n', style: staticText),
                TextSpan(
                    text: ' ${orientation == Orientation.portrait ? 'Portrait Mode' : 'Landscape Mode'}',
                    style: deviceText),
              ]),
        ),
        RichText(
          textAlign: TextAlign.center,
          text: TextSpan(
              children: [
                TextSpan(text: 'Device Display Mode:', style: staticText),
                TextSpan(
                    text: ' ${deviceBrightness == Brightness.light ? 'Light Mode' : 'Dark Mode'}',
                    style: deviceText),
              ]),
        ),
      ],
    );
  }
}
```

#### Screenshots
[RichTextTextSpanWidgets01](Screenshots/RichTextTextSpanWidgets01.png)  
[RichTextTextSpanWidgets02](Screenshots/RichTextTextSpanWidgets02.png)