# Gist of Flutter

## CheckboxListTile Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///CheckboxListTile Widget
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
              child: CheckBoxListTileWidget()
          ),
        ),
      ),
    );
  }
}

///The CheckboxListTile Widget is similar to the RadioListTile Widget with additional properties such as the 'title'
///and 'secondary' properties. The 'secondary' property can be any widget, in the example below, it is a Text Widget
///The two main properties of the CheckboxListTile widget are the value (which is a bool) and the onChanged() property. The value
///property can be initialized to a default state of false (or true depending on use case) and changed by using the
///onChanged() property, which takes a bool as an argument. The value property can then be set to this bool argument
///to change the state of the CheckboxListTile widget.

class CheckBoxListTileWidget extends StatefulWidget {
  @override
  _CheckBoxListTileWidgetState createState() => _CheckBoxListTileWidgetState();
}

class _CheckBoxListTileWidgetState extends State<CheckBoxListTileWidget> {

  int countDogs;

  Map<String, bool> dogs = {
    'Dog 1': false,
    'Dog 2': false,
    'Dog 3': false,
    'Dog 4': false
  };

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    countDogs = 0;
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      width: 250,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          CheckboxListTile(
              activeColor: Colors.blue[900],
              value: dogs['Dog 1'],
              title: Text(dogs.keys.toList()[0]),
              secondary: Text('🐶', style: TextStyle(fontSize: 20),),
              onChanged: (val) {
                dogSelectorFunction(val);
                dogs['Dog 1'] = val;
              }
          ),
          CheckboxListTile(
              activeColor: Colors.blue[900],
              value: dogs['Dog 2'],
              title: Text(dogs.keys.toList()[1]),
              secondary: Text('🐶', style: TextStyle(fontSize: 20),),
              onChanged: (val) {
                dogSelectorFunction(val);
                dogs['Dog 2'] = val;
              }
          ),
          CheckboxListTile(
              activeColor: Colors.blue[900],
              value: dogs['Dog 3'],
              title: Text(dogs.keys.toList()[2]),
              secondary: Text('🐶', style: TextStyle(fontSize: 20),),
              onChanged: (val) {
                dogSelectorFunction(val);
                dogs['Dog 3'] = val;
              }
          ),
          CheckboxListTile(
              activeColor: Colors.blue[900],
              value: dogs['Dog 4'],
              title: Text(dogs.keys.toList()[3]),
              secondary: Text('🐶', style: TextStyle(fontSize: 20),),
              onChanged: (val) {
                dogSelectorFunction(val);
                dogs['Dog 4'] = val;
              }
          ),
          Text('$countDogs dogs selected', style: TextStyle(fontSize: 20),),
        ],
      ),
    );
  }

  ///This function is called to increment or decrement the value of the countDogs variable, depending on the number
  ///of dogs selected. Accordingly, the state of the Text widget (that shows how many dogs are selected) changes.
  void dogSelectorFunction(bool dogVal){
    setState(() {
      if (dogVal == true)
        countDogs++;
      else
        countDogs--;
    });
  }
}
```

##### Refer this link [https://flutter-examples.com/get-multiple-checkbox-checked-value-in-flutter/](https://flutter-examples.com/get-multiple-checkbox-checked-value-in-flutter/)  

#### Screenshots

[CheckboxListTile01](Screenshots/CheckboxListTile01.png)  
[CheckboxListTile02](Screenshots/CheckboxListTile02.png)