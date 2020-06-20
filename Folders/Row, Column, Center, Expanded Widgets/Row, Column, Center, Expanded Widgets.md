# Gist of Flutter

## Row, Column, Center, Expanded Widgets

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Row, Column, Center and Expanded Widgets
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {

  Widget currentWidget;

  bool isTapped;

  @override
  void initState() {
    super.initState();
    currentWidget = RowWidget();
    isTapped = false;
  }

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
            leading: Builder(
              builder: (context){
                return IconButton(
                  icon: Icon(Icons.swap_horiz),
                  onPressed: () {
                    setState(() {
                      isTapped = !isTapped;
                      if (isTapped == true)
                        currentWidget = ColumnWidget();
                      if (isTapped == false)
                        currentWidget = RowWidget();
                    });
                  },
                );
              },
            ),
          ),
          ///The Center widget is used to align the child widget to the center of the parent widget
          body: Center(
              child: currentWidget
          ),
        ),
      ),
    );
  }
}

///The Row widget takes a list of children widgets and arranges them in a row
///If there are many widgets in a Row (or Column) that overflow outside the device's viewport (viewable area)
///a rendering error occurs saying that an overflow is occurred. This rendering error shows up as a a bar
///with yellow and black lines. To prevent this, wrap each individual widget in the Row's (or Column's) list of widgets
///in an Expanded widget.

///If an Expanded widget is used, the size of the child widget (in the Row or Column) is overridden to accommodate the
///children widgets. A Flex value can be assigned to the Expanded widget. The Flex property is a ratio of viewport
///occupied by the Expanded widget's child. The Flex value is always an int.

class RowWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Row(
        ///The mainAxisAlignment property is used to place the widgets in the Row. In the case of a Row, it is the
        ///horizontal direction (X-axis). It has no effect if an Expanded widget is used (because an Expanded widget
        ///fills the available space on the viewport with the child widget). If the Row widget's parent is a Container
        ///widget, don't give the parent Container a size, otherwise a rendering error will occur (i.e the parent
        ///Container's size is unbounded).
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        ///The crossAxisAlignment property is used to align the widgets on the Row widget's cross axis, which is the
        ///vertical direction (Y-axis).
        ///crossAxisAlignment: CrossAxisAlignment.stretch,
        ///The mainAxisSize property is the size that should be allocated to the widget on its main axis.
        mainAxisSize: MainAxisSize.max,
        children: <Widget>[
          Expanded(
            child: Container(
              width: 100,
              height: 100,
              color: Colors.blue,
            ),
          ),
          Text('Row Widget', style: TextStyle(fontSize: 20),),
          /*Expanded( 
            flex: 2, 
            child: Container( 
              width: 200, 
              height: 200, 
              color: Colors.red, 
            ), 
          ), 
          Expanded( 
            flex: 2, 
            child: Container( 
              width: 200, 
              height: 200, 
              color: Colors.green, 
            ), 
          ),*/
          Expanded(
            child: Container(
              width: 100,
              height: 100,
              color: Colors.indigo,
            ),
          )
        ],
      ),
    );
  }
}

class ColumnWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Column(
        ///The mainAxisAlignment property is used to place the widgets in the Column. In the case of a Column, it is the
        ///horizontal direction (Y-axis). It has no effect if an Expanded widget is used (because an Expanded widget
        ///fills the available space on the viewport with the child widget). If the Row widget's parent is a Container
        ///widget, don't give the parent Container a size, otherwise a rendering error will occur (i.e the parent
        ///Container's size is unbounded).
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        ///The crossAxisAlignment property is used to align the widgets on the Column widget's cross axis, which is the
        ///horizontal direction (X-axis).
        ///crossAxisAlignment: CrossAxisAlignment.stretch,
        ///The mainAxisSize property is the size that should be allocated to the widget on its main axis.
        mainAxisSize: MainAxisSize.max,
        children: <Widget>[
          Expanded(
            child: Container(
              width: 100,
              height: 100,
              color: Colors.blue,
            ),
          ),
          Text('Column Widget', style: TextStyle(fontSize: 20),),
          /*Expanded( 
            flex: 2, 
            child: Container( 
              width: 200, 
              height: 200, 
              color: Colors.red, 
            ), 
          ), 
          Expanded( 
            flex: 2, 
            child: Container( 
              width: 200, 
              height: 200, 
              color: Colors.green, 
            ), 
          ),*/
          Expanded(
            child: Container(
              width: 100,
              height: 100,
              color: Colors.indigo,
            ),
          )
        ],
      ),
    );
  }
}
```

#### Screenshots
[ColumnWidget](Screenshots/ColumnWidget.png)  
[RowWidget](Screenshots/RowWidget.png)