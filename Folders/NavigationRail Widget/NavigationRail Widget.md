# Gist of Flutter

## NavigationRail Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///NavigationRail Widget
///The NavigationRail Widget is a new widget that is "meant to be displayed at the left or right of an app between a
///small number of view, the minimum number of views being 3 (and up to 5)". It is the first or last element in a Row.
///Unlike other Navigation Material Widgets such as the TabBar and the BottomSheet, there is no property in the Scaffold
///Widget that allows a NavigationRail widget to be set. It can be set anywhere in the Widget tree by wrapping it in a
///Row Widget.

///The main properties of the NavigationRail Widget are the selectedIndex, destinations and the onDestinationSelected
///properties. These properties are used for enabling navigation from the NavigationRail Widget. The destinations
///property takes a list of NavigationRailDestination Widgets. The icon property for NavigationRailDestination is
///mandatory. If no icon is to be displayed, use the statement SizedBox.shrink(). To always show the label vertically
///in the NavigationRailDestination Widget, wrap the Text Widget in a RotatedBox Widget.

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
            child: NavigationRailWidget(),
          ),
        ),
      ),
    );
  }
}

class NavigationRailWidget extends StatefulWidget {
  @override
  _NavigationRailWidgetState createState() => _NavigationRailWidgetState();
}

class _NavigationRailWidgetState extends State<NavigationRailWidget> {

  ///Initializing variable for the Navigation Rail index
  int navigationSelectedIndex = 0;

  TextStyle railTextStyle = TextStyle(color: Colors.black);

  @override
  Widget build(BuildContext context) {
    return Row(
      children: <Widget>[
        NavigationRail(
          ///The elevation property is optional
          elevation: 20,
          ///Call setState() in the onDestinationSelected property to set the selected index in the list of
          ///NavigationRailDestination Widgets.
          onDestinationSelected: (int currentIndex) => setState(() => navigationSelectedIndex = currentIndex),
          selectedLabelTextStyle: railTextStyle,
          unselectedLabelTextStyle: railTextStyle,
          ///The leading property can be any widget. It can be used along with the trailing property or one or the other,
          ///either the leading or trailing property can be used.
          leading: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Container(
              width: 40,
              height: 40,
              child: CircleAvatar(
                backgroundImage: AssetImage('assets/cars/Cars05.jpg'),
              ),
            ),
          ),
          ///The selectedIndex property is mandatory and it tells the NavigationRailWidget which is the current selected
          ///navigation rail destination.
          selectedIndex: navigationSelectedIndex,
          labelType: NavigationRailLabelType.selected,
          ///A minimum of 3 NavigationRailDestination Widgets are required, with up to a maximum of 5.
          destinations: [
            ///Use SizedBox.shrink() property for a given property in a NavigationRailDestination Widget in order to
            ///make that property invisible.

            ///To rotate any widget in the NavigationRailDestination Widget vertically, wrap the widget of that property
            ///in a RotatedBox Widget and set the quarterTurns property to -1.
            NavigationRailDestination(
              icon: Icon(Icons.list),
              label: SizedBox.shrink(),
            ),
            NavigationRailDestination(
                icon: Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: RotatedBox(quarterTurns: -1, child: Text('Item 1', style: railTextStyle,)),
                ),
                label: SizedBox.shrink()
            ),
            NavigationRailDestination(
              icon: Padding(
                padding: const EdgeInsets.all(8.0),
                child: RotatedBox(quarterTurns: -1, child: Text('Item 2', style: railTextStyle,)),
              ),
              label: SizedBox.shrink(),
            ),
            NavigationRailDestination(
                icon: Padding(
                  padding: const EdgeInsets.all(8.0),
                  child: RotatedBox(quarterTurns: -1, child: Text('Item 3', style: railTextStyle,)),
                ),
                label: SizedBox.shrink()
            ),
          ],
        ),
        ///For best results in displaying the NavigationRail Widget in its parent Row, wrap all other widgets in the
        ///Row Widget in an Expanded Widget.
        Expanded(
          child: Center(
            child: Text('${navigationSelectedIndex == 0? 'Nothing selected': 'Item $navigationSelectedIndex selected'}'),
          ),
        ),
      ],
    );
  }
}
```

Refer this link [https://medium.com/flutter-community/flutter-navigationrail-widget-new-in-v1-17-4b8c5416a081](https://medium.com/flutter-community/flutter-navigationrail-widget-new-in-v1-17-4b8c5416a081)  
Refer this link [https://api.flutter.dev/flutter/material/NavigationRail-class.html](https://api.flutter.dev/flutter/material/NavigationRail-class.html)

#### Screenshots
[NavigationRailWidget](Screenshots/NavigationRailWidget.png)