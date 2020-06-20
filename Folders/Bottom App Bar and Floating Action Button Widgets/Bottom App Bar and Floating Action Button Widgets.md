# Gist of Flutter

## Bottom App Bar and Floating Action Button Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///BottomAppBar and FloatingActionButton Widget
///The FloatingActionButton Widget is, as the name suggests, a button that 'floats' on the Viewport, irrespective of
///changing UI elements (unless programmed to behave otherwise). Its main properties are the onPressed() property and
///the shape property (using which a custom shape can be given to the button). Using the floatingActionButtonLocation
///property of the FloatingActionButton, the button can be aligned to different positions on the Viewport.
///The BottomAppBar Widget is like an AppBar Widget, but located at the bottom of the Viewport. However, unlike the
///AppBar Widget, the BottomAppBar Widget does not have many properties. The major property of the BottomAppBar Widget
///are the notchMargin property (for giving margin between the FloatingActionButton and the notch) and the shape
///property which is used to give the notch a shape.

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Scaffold(
          ///Setting the location of the FloatingActionButton Widget
          floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
          bottomNavigationBar: BottomAppBarWidget(),
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
          ),
          body: Center(
            child: Container(),
          ),
          floatingActionButton: FloatingActionButton(
            elevation: 10,
            backgroundColor: Colors.black,
            child: Icon(Icons.add, size: 24),
            ///The shape property is used to apply a custom shape to the FloatingActionButton Widget
            shape: BeveledRectangleBorder(
                borderRadius: BorderRadius.all(Radius.circular(15))
            ),
            onPressed: (){},
          ),
        ),
      ),
    );
  }
}

class BottomAppBarWidget extends StatefulWidget {
  @override
  _BottomAppBarWidgetState createState() => _BottomAppBarWidgetState();
}

class _BottomAppBarWidgetState extends State<BottomAppBarWidget> {
  @override
  Widget build(BuildContext context) {
    return BottomAppBar(
      color: Colors.blue[900],
      ///The notch margin property is used for adding a margin between the notch and FloatingActionButton Widget.
      notchMargin: 3.5,
      ///The AutomaticNotchedShape constructor is used here for implementing the shape of the notch (which contains the
      ///FloatingActionButton Widget). The other constructor that can be used is the CircularNotchedRectangle
      ///constructor. The AutomaticNotchedShape constructor has two main properties - the host (which is of the type
      ///ShapeBorder and is mandatory) and the guest (which is of the type ShapeBorder). For custom border styles, the
      ///host border's properties can be left as they are without passing any properties, and applying properties
      ///to the guest ShapeBorder (in this case the BeveledRectangleBorder constructor).
      shape: AutomaticNotchedShape(
          RoundedRectangleBorder(),
          BeveledRectangleBorder(
              borderRadius: BorderRadius.all(Radius.circular(15))
          )
      ),
      ///The BottomAppBar Widget can have any widget as its child. It need not have a child Widget either. Here, a
      ///Container widget is given as its child for customizing the size of the BottomAppBar Widget.
      child: Container(
        color: Colors.transparent,
        height: 75,
        child: Padding(
          padding: const EdgeInsets.all(10.0),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: <Widget>[
              ///The below loop calls the bottomAppBarButtons Widget and depending on the index, constructs the items
              ///in the BottomAppBar Widget
              for (int index = 0; index < 4; index++)
                bottomAppBarButtons(index),
            ],
          ),
        ),
      ),
    );
  }

  ///BottomAppBar item Widget for a given index
  Widget bottomAppBarButtons(int index) {
    return InkWell(
      onTap: () {},
      splashColor: Colors.white24,
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceAround,
        children: [
          Text('Item ${index + 1}', style: TextStyle(color: Colors.white),),
          Icon(Icons.subject, color: Colors.white, size: 20),
        ],
      ),
    );
  }
}
```

#### Screenshots

[Bottom App Bar and Floating Action Button Widgets](Screenshots/BottomAppBarFloatingActionButtonWidgets.png)