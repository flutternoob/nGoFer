# Gist of Flutter

## Dialog Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///AlertDialog Widget, CustomDialog, SimpleDialog and AboutDialog Widget

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
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
        body: ButtonsWidget(),
      ),
    );
  }
}

class ButtonsWidget extends StatelessWidget {
  List dialogTypes = [
    'Alert Dialog',
    'Custom Dialog',
    'Simple Dialog',
    'About Dialog'
  ];

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceAround,
        children: [
          ///These buttons are used to invoke the different types of dialog widgets using the showDialogFunction
          for(String dialogTitle in dialogTypes)
            CustomButton(dialogTitle: dialogTitle,)
        ],
      ),
    );
  }
}

class CustomButton extends StatefulWidget {
  final String dialogTitle;

  CustomButton({this.dialogTitle});

  @override
  _CustomButtonState createState() => _CustomButtonState();
}

class _CustomButtonState extends State<CustomButton> {

  @override
  Widget build(BuildContext context) {
    return MaterialButton(
      elevation: 10,
      color: Colors.black,
      onPressed: () => dialogFunction(widget.dialogTitle, context),
      child: Text(widget.dialogTitle, style: TextStyle(color: Colors.white),),
    );
  }
}

///This is a custom function that is used for determining the dialog type and calling the showDialog function to invoke
///the dialog
void dialogFunction(String dialogType, BuildContext context){
  Widget dialogTypeWidget;

  if (dialogType == 'Alert Dialog')
    dialogTypeWidget = AlertDialogWidget();
  if (dialogType == 'Custom Dialog')
    dialogTypeWidget = CustomDialogWidget();
  if (dialogType == 'Simple Dialog')
    dialogTypeWidget = SimpleDialogWidget();
  if (dialogType == 'About Dialog')
    dialogTypeWidget = AboutDialogWidget();
  ///All Dialog Widgets are invoked by the showDialog Function. This function takes a context and a builder as its
  ///main parameters. The builder takes a BuildContext as an argument and returns a Dialog. If barrierDismissible is
  ///set to true, the dialog can be dismissed by tapping anywhere in the Viewport, otherwise functionality should be
  ///implemented in the dialog to dismiss it.
  showDialog(
      context: context,
      builder: (BuildContext context) => dialogTypeWidget,
      barrierDismissible: true
  );
}

///The AlertDialog Widget can be used in cases to create alerts, such as an app error or when permissions are required
class AlertDialogWidget extends StatefulWidget {
  @override
  _AlertDialogWidgetState createState() => _AlertDialogWidgetState();
}

class _AlertDialogWidgetState extends State<AlertDialogWidget> {
  @override
  Widget build(BuildContext context) {
    return AlertDialog(
      backgroundColor: Colors.white,
      title: Text('Alert'),
      content: Text('This is an Alert Dialog'),
      actions: [
        FlatButton(
            onPressed: () => Navigator.pop(context),
            child: Text('OK')
        )
      ],
    );
  }
}

///The CustomDialog Widget can be used in cases where a lot of customization is required for an app-wide dialog. Unlike
///other dialog widgets, the size of the dialog changes based on device orientation. To constrain the size, either a
///Container Widget or a SizedBox Widget (with proportions for both, landscape and portrait orientation) should be used
///as the dialog's child.
class CustomDialogWidget extends StatefulWidget {
  @override
  _CustomDialogWidgetState createState() => _CustomDialogWidgetState();
}

class _CustomDialogWidgetState extends State<CustomDialogWidget> {
  double dialogWidth;
  double dialogHeight;

  @override
  Widget build(BuildContext context) {
    if (MediaQuery.of(context).orientation == Orientation.portrait){
      dialogWidth = 300;
      dialogHeight = 175;
    }
    if (MediaQuery.of(context).orientation == Orientation.landscape){
      dialogWidth = 350;
      dialogHeight = 180;
    }
    return Dialog(
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.all(Radius.circular(15))
      ),
      child: Container(
        width: dialogWidth,
        height: dialogHeight,
        child: Padding(
          padding: const EdgeInsets.all(10.0),
          child: Column(
            children: [
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Text('Custom'),
              ),
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Text('This is a Custom Dialog'),
              ),
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.spaceAround,
                  children: [
                    MaterialButton(
                      elevation: 10,
                      color: Colors.black,
                      onPressed: () => Navigator.pop(context),
                      child: Text('Yes', style: TextStyle(color: Colors.white),),
                    ),
                    MaterialButton(
                      elevation: 10,
                      color: Colors.black,
                      onPressed: () => Navigator.pop(context),
                      child: Text('No', style: TextStyle(color: Colors.white),),
                    )
                  ],
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}

///The SimpleDialog Widget can be used in cases where minimal information is required
class SimpleDialogWidget extends StatefulWidget {
  @override
  _SimpleDialogWidgetState createState() => _SimpleDialogWidgetState();
}

class _SimpleDialogWidgetState extends State<SimpleDialogWidget> {
  @override
  Widget build(BuildContext context) {
    return SimpleDialog(
      title: Text('Simple Dialog'),
      titlePadding: EdgeInsets.all(20),
      contentPadding: EdgeInsets.all(10),
      children: [
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: Text('This is a Simple Dialog'),
        ),
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: FlatButton(
            onPressed: () => Navigator.pop(context),
            child: Text('OK')
          ),
        )
      ],
    );
  }
}

///The AboutDialog Widget gives information such as the name of the application, version and legal information
class AboutDialogWidget extends StatefulWidget {
  @override
  _AboutDialogWidgetState createState() => _AboutDialogWidgetState();
}

class _AboutDialogWidgetState extends State<AboutDialogWidget> {
  @override
  Widget build(BuildContext context) {
    return AboutDialog(
      applicationName: 'Demo App',
      applicationVersion: '1.0.0',
      applicationLegalese: 'Legal Information comes here',
      applicationIcon: Icon(Icons.info_outline),
    );
  }
}
```

#### Screenshots

[DialogWidgets01](Screenshots/DialogWidgets01.png)  
[DialogWidgets02](Screenshots/DialogWidgets02.png)  
[DialogWidgets03](Screenshots/DialogWidgets03.png)  
[DialogWidgets04](Screenshots/DialogWidgets04.png)  
[DialogWidgets05](Screenshots/DialogWidgets05.png)  
[DialogWidgets06](Screenshots/DialogWidgets06.png)