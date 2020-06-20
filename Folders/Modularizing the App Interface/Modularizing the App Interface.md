# Gist of Flutter

## Modularizing the App Interface

#### Code
```Java
import 'package:flutter/material.dart';

///Modularizing the App Interface

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  List<String> buttonText = ['Page 1', 'Page 2'];

  @override
  Widget build(BuildContext context) {
    return AppInterface(
      title: 'Demo App',
      appBarColor: Colors.blue[900],
      scaffoldBackgroundColor: Colors.white,
      bodyWidget: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: [
            for (int i = 0; i < buttonText.length; i++)
              ButtonsWidget(
                buttonText: buttonText[i],
              ),
            DummyWidget(pageContent: 'This is the home page')
          ],
        ),
      ),
    );
  }
}

///Custom Buttons Widget
class ButtonsWidget extends StatefulWidget {
  final String buttonText;

  ButtonsWidget({this.buttonText});

  @override
  _ButtonsWidgetState createState() => _ButtonsWidgetState();
}

class _ButtonsWidgetState extends State<ButtonsWidget> {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: MaterialButton(
        elevation: 10,
        color: Colors.black,
        child: Text(
          widget.buttonText,
          style: TextStyle(color: Colors.white),
        ),
        onPressed: () => appRoutingFunction(widget.buttonText, context),
      ),
    );
  }
}

///Navigation routing function
void appRoutingFunction(String pageName, BuildContext context) {
  if (pageName == 'Page 1')
    Navigator.pushReplacement(
      context,
      MaterialPageRoute(
        builder: (context) => AppInterface(
          title: 'Page 1',
          appBarColor: Colors.black,
          scaffoldBackgroundColor: Colors.grey[900],
          bodyWidget: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              children: [
                DummyWidget(
                  pageContent: 'This is page 1',
                ),
                ButtonsWidget(
                  buttonText: 'Home Page',
                ),
              ],
            ),
          ),
        ),
      ),
    );
  else if (pageName == 'Page 2')
    Navigator.pushReplacement(
      context,
      MaterialPageRoute(
        builder: (context) => AppInterface(
          title: 'Page 2',
          appBarColor: Colors.red[900],
          scaffoldBackgroundColor: Colors.grey[900],
          bodyWidget: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              children: [
                DummyWidget(
                  pageContent: 'This is page 2',
                ),
                ButtonsWidget(
                  buttonText: 'Home Page',
                ),
              ],
            ),
          ),
        ),
      ),
    );
  else Navigator.pushReplacement(context, MaterialPageRoute(builder: (context) => MyApp()));
}

///Create Widgets for the Body depending on the requirements of the screens in the app. Here a custom dummy Widget is used
class DummyWidget extends StatelessWidget {
  final String pageContent;

  DummyWidget({this.pageContent});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text(pageContent, style: TextStyle(color: Colors.red[900], fontSize: 18, fontWeight: FontWeight.bold)),
    );
  }
}

///Create a base UI widget
class AppInterface extends StatefulWidget {
  final String title;
  final appBarColor;
  final scaffoldBackgroundColor;
  final Widget bodyWidget;

  AppInterface({this.title, this.appBarColor, this.scaffoldBackgroundColor, this.bodyWidget});

  @override
  _AppInterfaceState createState() => _AppInterfaceState();
}

class _AppInterfaceState extends State<AppInterface> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        backgroundColor: widget.scaffoldBackgroundColor,
        appBar: AppBar(
          elevation: 10,
          backgroundColor: widget.appBarColor,
          title: Text(widget.title, style: TextStyle(color: Colors.white),),
          centerTitle: true,
        ),
        body: widget.bodyWidget,
      ),
    );
  }
}
```

#### Screenshots
[ModularizingAppInterface01](Screenshots/ModularizingAppInterface01.png)  
[ModularizingAppInterface02](Screenshots/ModularizingAppInterface02.png)  
[ModularizingAppInterface03](Screenshots/ModularizingAppInterface03.png)