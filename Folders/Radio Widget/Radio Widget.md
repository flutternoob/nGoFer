# Gist of Flutter

## Radio Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Radio Widget
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
          ///The Center widget is used to align the child widget to the center of the parent widget
          body: Center(
              child: RadioButtonWidget()
          ),
        ),
      ),
    );
  }
}

///Like RadioListTile widgets, Radio Widgets are grouped using an integer value using the groupValue property of the Radio widget
///with each Radio widget in the group having a unique int value. The onChanged() property of the Radio
///is used to set (via the setState() method) the groupValue property equal to the value of the given RadioListTile.
///When this happens, the visual state of the given Radio widget changes. The changed value can then either be
///used to redirect the user to another screen or change the state of another widget or the app (useful when changing
///themes) Radios are useful when only one value (or condition) has to be met, either true (selected ) or false
///(not selected). When more than one item has to be selected, use a CheckBox Widget.

class RadioButtonWidget extends StatefulWidget {
  @override
  _RadioButtonWidgetState createState() => _RadioButtonWidgetState();
}

class _RadioButtonWidgetState extends State<RadioButtonWidget> {

  int groupValue;
  String radioListTileSelected;
  String buttonText;
  int pageValue;
  String pageText;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    groupValue = 0;
    pageValue = 0;
    pageText = 'Not going to any page';
    radioListTileSelected = 'Nothing selected';
    buttonText = 'Nothing selected';
  }

  ///This function is called to set the groupValue property to the value of a give Radio widget
  void radioSelectorFunction(int radioValue){
    setState(() {
      groupValue = radioValue;
      radioListTileSelected = 'Radio Button $radioValue selected';
    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 250,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: <Widget>[
          Row(
            children: <Widget>[
              Radio(
                value: 1,
                groupValue: groupValue,
                onChanged: (radioListTileValue) => radioSelectorFunction(radioListTileValue),
                activeColor: Colors.black,
              ),
              Text('Radio Button 1')
            ],
          ),
          Row(
            children: <Widget>[
              Radio(
                value: 2,
                groupValue: groupValue,
                onChanged: (radioListTileValue) => radioSelectorFunction(radioListTileValue),
                activeColor: Colors.black,
              ),
              Text('Radio Button 2')
            ],
          ),
          Row(
            children: <Widget>[
              Radio(
                value: 3,
                groupValue: groupValue,
                onChanged: (radioListTileValue) => radioSelectorFunction(radioListTileValue),
                activeColor: Colors.black,
              ),
              Text('Radio Button 3')
            ],
          ),
          Row(
            children: <Widget>[
              Radio(
                value: 4,
                groupValue: groupValue,
                onChanged: (radioListTileValue) => radioSelectorFunction(radioListTileValue),
                activeColor: Colors.black,
              ),
              Text('Radio Button 4')
            ],
          ),
          Text(radioListTileSelected, style: TextStyle(color: Colors.blue, fontSize: 20),),
          MaterialButton(
            shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.all(Radius.circular(20)),
            ),
            color: Colors.black,
            elevation: 10,
            onPressed: () => setState((){
              buttonText = radioListTileSelected;
              ///The below function is called to determine Material Route Navigation based on the groupValue of a given
              ///Radio widget
              pageSelectorFunction(groupValue);
            }),
            child: Text(buttonText, style: TextStyle(color: Colors.white),),
          ),
          Text(pageText, style: TextStyle(color: Colors.blue, fontSize: 20),),
        ],
      ),
    );
  }

  ///If material route navigation is used, this function can be used as boilerplate code to navigate to a screen
  ///in the app. Here the groupValue is used as an 'identifier' to identify which page navigation has to be implemented
  void pageSelectorFunction (int pageIdentifier){
    switch (pageIdentifier) {
      case 1:
        pageText = 'Going to page $pageIdentifier';
        break;
      case 2:
        pageText = 'Going to page $pageIdentifier';
        break;
      case 3:
        pageText = 'Going to page $pageIdentifier';
        break;
      case 4:
        pageText = 'Going to page $pageIdentifier';
        break;
    }
  }
}
```

#### Screenshots

[RadioWidget](Screenshots/RadioWidget.png)  