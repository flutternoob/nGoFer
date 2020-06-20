# Gist of Flutter

## CircleAvatar Widget, Widget functions, Custom Widgets, Image class and the Spread operator

#### Code
```Java
import 'dart:typed_data';
import 'package:flutter/material.dart';
import 'dart:io';
import 'package:flutter/services.dart';

void main() => runApp(MyApp());

///CircleAvatar Widget, Widget functions, Image class and the Spread operator
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
          body: Center(child: CircleAvatarWidget()),
        ),
      ),
    );
  }
}

///The CircleAvatar Widget is used to display an image in circular 'container (not to be confused with the Container Widget)'
///widget. The two main properties of the CircleAvatar widget are its radius and backgroundImage properties. Avoid using
///the child property of the Circle Avatar widget for displaying the image as it will not display the image in a circular
///manner. The radius property is used to set the size of the CircleAvatar Widget. The backgroundImage property is used
///to provide the source of the image, which can be either from Asset, Network, File or from Memory

///Image class. The image class is used to 'provide' an image source to a widget using ImageProvider. The
///ImageProvider can be an asset, network, file or memory. The procedure to load images for each of these providers is
///as follows:
///First, create an ImageProvider variable like so: ImageProvider variable_name;
///Use the following syntax and/or steps for the respective ImageProvider:
///
///1) Image from Asset syntax: variable_name = AssetImage('AssetImagePath'); (Remember to add the assets in pubspec.yaml)
///
///2) Image from Network syntax: variable_name = NetworkImage('NetworkImageURL');
///
///3) Image from File:
///   Import the 'dart:io' library;
///   Set the following permissions in the AndroidManifest.xml file (for file read and write access):
///     <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
///     <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
///   Give the app permission on the target device access to storage. Either use a Dialog prompting the user to give the
///   app permission to access storage or do it programmatically once the user grants permission
///   Syntax: variable_name = FileImage(File('FileImagePath'));
///
///4) Image from Memory:
///   Import the 'dart:typed_data' and the 'package:flutter/services.dart' libraries
///   Declare a variable of type Uint8List like so: Uint8List data;
///   Create a Future that will retrieve the data from the file as a Unit8List from a particular source (such as an Asset or
///   Network). Note: As an example, the MemoryImage ImageProvider can be used while retrieving the image used in the
///   circular avatars of a list of contacts when used with contacts_service package (from pub.dev)

///If a particular widget is going to be repeatedly used in an app, the widget can be extracted to a separate Widget function
///or a custom Stateless or Stateful widget depending on use case. In either case parameters can be passed to the
///modularized widget to make it behave differently, depending on use case.

///The spread operator was introduced in Dart 2.3.0 and allows for looping and condition checking in a list of widgets,
///whose parent widget is a Widget that take a list of widgets as a parameter (such as the Row, Column, Stack, ListView
///widgets). Syntax for condition checking:
///
///if(someCondition)...[displayThisWidget],
///
///Syntax for looping (using a List as an example):
///
///for (int count = 0; count < someListVariable.length; count++)...[displayThisWidget[count]],

class CircleAvatarWidget extends StatefulWidget {
  @override
  _CircleAvatarWidgetState createState() => _CircleAvatarWidgetState();
}

class _CircleAvatarWidgetState extends State<CircleAvatarWidget> {

  ///The below variable is declared as an example to demonstrate the use of the spread operator and custom widgets
  List<String> imageSource;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    imageSource = ['Image from Asset', 'Image from Network', 'Image from File', 'Image from Memory'];
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 500,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: <Widget>[
          ///Looping using the spread operator
          for (int i = 0; i < imageSource.length; i++)...[
            ///Calling the modularized function 'i' times
            customRowWidget(imageSource[i])
          ]
        ],
      ),
    );
  }
}

///Modularized custom Widget Function with the string from the imageSource variable used as an identifier for condition
///checking
Widget customRowWidget(String imageSourceText){
  return Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: <Widget>[
      Container(
        width: 200,
          child: Text(imageSourceText, style: TextStyle(fontSize: 18, fontWeight: FontWeight.w500),)
      ),
      ///Calling the custom circle avatar widget and passing the imageSourceText as a parameter to determine which
      ///ImageProvider has to be used
      CustomCircleAvatarWidget(imageSourceText: imageSourceText)
    ],
  );
}

///Custom Circle Avatar Stateful Widget that uses the imageSourceText as a parameter
class CustomCircleAvatarWidget extends StatefulWidget {

  final String imageSourceText;

  ///This is the widget's Default Constructor
  CustomCircleAvatarWidget({this.imageSourceText});

  @override
  _CustomCircleAvatarWidgetState createState() => _CustomCircleAvatarWidgetState();
}

class _CustomCircleAvatarWidgetState extends State<CustomCircleAvatarWidget> {

  ///Declaring the Uint8List variable for the Memory Image Provider
  Uint8List data;

  ///Declaring the ImageProvider variable whose state changes depending on the imageSourceText parameter
  ImageProvider backgroundImage;

  ///Creating the Future to get the path of the Memory Image path.
  Future getMemoryImagePath() async {
    data = (await rootBundle.load('assets/cars/Cars04.jpg')).buffer.asUint8List();
    backgroundImage = MemoryImage(data);
  }

  @override
  Widget build(BuildContext context) {
    ///Asset Image Provider
    if (widget.imageSourceText == 'Image from Asset')
      setState(() {
        backgroundImage = AssetImage('assets/cars/Cars08.jpg');
      });
    ///Network Image Provider
    if (widget.imageSourceText == 'Image from Network')
      setState(() {
        backgroundImage = NetworkImage(
            'https://images.unsplash.com/photo-1541690212779-7a48c04096cb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1534&q=80');
      });
    ///File Image Provider
    if (widget.imageSourceText == 'Image from File')
      setState(() {
        backgroundImage = FileImage(File('/storage/28CA-F3E8/demoimages/item4.jpg'));
      });
    ///Memory Image provider
    if (widget.imageSourceText == 'Image from Memory')
      setState(() {
        getMemoryImagePath();
      });
    return CircleAvatar(
      radius: 40,
      backgroundImage: backgroundImage,
    );
  }
}

```

Refer this link [https://stackoverflow.com/questions/60558577/how-to-solve-os-error-permission-denied-errno-13-in-flutter](https://stackoverflow.com/questions/60558577/how-to-solve-os-error-permission-denied-errno-13-in-flutter)  
Refer this link [https://www.woolha.com/tutorials/flutter-using-memoryimage-examples](https://www.woolha.com/tutorials/flutter-using-memoryimage-examples)  
Refer this link [https://www.woolha.com/tutorials/dart-using-triple-dot-spread-operator-examples](https://www.woolha.com/tutorials/dart-using-triple-dot-spread-operator-examples)

#### Screenshots

[CircleAvatarWidgetCustomStatefulWidgetFunctionsSpreadOperator](Screenshots/CircleAvatarWidgetCustomStatefulWidgetFunctionsSpreadOperator.png)