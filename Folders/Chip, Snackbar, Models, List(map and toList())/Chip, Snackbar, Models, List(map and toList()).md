# Gist of Flutter

## Chip, Snackbar, Models, List(map and toList())

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Chip Widget, SnackBar Widget, using models, map and toList() functions (for List<model>)
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
          body: Center(child: ChipWidget()),
        ),
      ),
    );
  }
}

class ChipWidget extends StatefulWidget {
  @override
  _ChipWidgetState createState() => _ChipWidgetState();
}

class _ChipWidgetState extends State<ChipWidget> {

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
  }

  ///List Variable used to create a list of the items in a model (ChipInfo model in this case)
  List<ChipInfo> chipInfo = [
    ChipInfo(
        chipTitle: 'Chip 1',
        circleAvatarText: '1',
        chipIndex: 1
    ),
    ChipInfo(
        chipTitle: 'Chip 2',
        circleAvatarText: '2',
        chipIndex: 2
    ),
    ChipInfo(
        chipTitle: 'Chip 3',
        circleAvatarText: '3',
        chipIndex: 3
    ),
    ChipInfo(
        chipTitle: 'Chip 4',
        circleAvatarText: '4',
        chipIndex: 4
    ),
  ];

  ///This function is called to show the SnackBar Widget that shows a given item at a given index has been removed from
  ///the List of models (ChipInfo model in this case)
  void showSnackBarFunction(int chipIndex){
    ///The main properties of the SnackBar Widget are the content and the duration. The content shows the snack bar
    ///content while the duration property sets the duration for which the snack bar is shown on the device screen.
    SnackBar snackBar = SnackBar(
      content: Text('Chip $chipIndex deleted', style: TextStyle(color: Colors.white)),
      duration: Duration(seconds: 1),
    );
    ///The showSnackBar function is called using Scaffold.of(context).showSnackBar(snackBar_variable). For this to work,
    ///a Scaffold context must be available to the widget from where it (showSnackBar) is called
    Scaffold.of(context).showSnackBar(snackBar);
  }

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(10.0),
      child: Column(
        ///Use the .map method on the List<models> to map the List as an Iterable and then call the .toList() method
        ///Basic syntax for this is: listOfModels.map((modelItem) => return Widget).toList();
          children: chipInfo.map((theChipWidget) => Padding(
            padding: const EdgeInsets.all(10.0),
            child: Chip(
              shadowColor: Colors.blue,
              backgroundColor: Colors.blue[900],
              label: Padding(
                padding: const EdgeInsets.all(10.0),
                child: Text(theChipWidget.chipTitle, style: TextStyle(color: Colors.white, fontSize: 20),),
              ),
              elevation: 10,
              deleteIcon: Icon(Icons.delete, color: Colors.white),
              ///If the onDelete property is not set in the Chip Widget, the deleteIcon will not be visible
              onDeleted: () {
                setState(() {
                  chipInfo.remove(theChipWidget);
                  showSnackBarFunction(theChipWidget.chipIndex);
                });
              },
              ///The avatar property can be any widget, usually it is a CircleAvatar widget
              avatar: Padding(
                padding: const EdgeInsets.all(10.0),
                child: CircleAvatar(
                  radius: 40,
                  backgroundColor: Colors.black,
                  child: Text(theChipWidget.circleAvatarText, style: TextStyle(color: Colors.white, fontSize: 20),),
                ),
              ),
            ),
          )).toList()
      ),
    );
  }
}

///Models are used to provide a blueprint for classes and/or methods that may need to access the model during the
///app's lifecycle.

///Chip Model
class ChipInfo {
  String chipTitle;
  String circleAvatarText;
  int chipIndex;

  ///Default constructor
  ChipInfo({this.chipTitle, this.circleAvatarText, this.chipIndex});
}
```

#### Screenshots

[ChipSnackbarListModels01](Screenshots/ChipSnackbarListModels01.png)  
[ChipSnackbarListModels02](Screenshots/ChipSnackbarListModels02.png)  
[ChipSnackbarListModels03](Screenshots/ChipSnackbarListModels03.png)