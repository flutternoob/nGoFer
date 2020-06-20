# Gist of Flutter

## FABExtended and Multiple FABs

#### Code
```Java
import 'package:flutter/material.dart';

///FloatingActionButtonExtended Widget. This widget is like a FloatingActionButton Widget, with the additional feature of
///adding a label (as a Text Widget) to the FloatingActionButton.

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
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
        body: Container(),
        floatingActionButton: _buildFab(context),
      ),
    );
  }
}

///This function uses a context and is used to instantiate an icon list and returns the FabWithIcons Widget
Widget _buildFab (BuildContext context) {
  final icons = [
    Icons.music_note,
    Icons.music_video,
    Icons.music_video,
    Icons.music_video
  ];
  return FabWithIcons(
    icons: icons,
    onIconTapped: (index) {},
  );
}

///This Widget is used to build the main FAB and the menu FABs. TickerProviderStateMixin has to be mixed with this Widget
///to implement the animation.
class FabWithIcons extends StatefulWidget {

  FabWithIcons({this.icons, this.onIconTapped});

  final List<IconData> icons;
  ValueChanged<int> onIconTapped;

  @override
  _FabWithIconsState createState() => _FabWithIconsState();
}

class _FabWithIconsState extends State<FabWithIcons> with TickerProviderStateMixin{
  ///Declaring an animation controller for animating the FABs in the menu
  AnimationController _controller;

  @override
  void initState() {
    super.initState();
    ///Setting the initial state of the animation controller
    _controller = AnimationController(
      vsync: this,
      ///Setting the duration of the animation for forward() and reverse() states of the animation controller.
      duration: const Duration(milliseconds: 100),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Column(
        mainAxisAlignment: MainAxisAlignment.center,
        mainAxisSize: MainAxisSize.min,
        ///Depending on the number of Icon Widgets in the list of icons, a list is generated and the _buildChild()
        ///Widget function is returned in a temporary list, only for displaying the FABs in the FAB menu.
        children: List.generate(widget.icons.length, (int index) {
          return _buildChild(index);
        }).toList()..add(_buildFab(),)
    );
  }

  ///This function implements the FAB in the FAB menu depending on the index.
  Widget _buildChild (int index) {
    Color backgroundColor = Colors.blue[700];

    return Container(
      height: 70,
      width: 70,
      ///The alignment property is used to adjust the location of each FAB in the FAB menu
      alignment: FractionalOffset.topCenter,
      child: ScaleTransition(
        ///The type of curved animations is implemented using the CurvedAnimation constructor
        scale: CurvedAnimation(
          parent: _controller,
          curve: Interval(
              0.0,
              1.0 - index/widget.icons.length/2.0,
              curve: Curves.easeOut
          ),
        ),
        ///The other FABs in the FAB menu are implemented using the extended constructor
        child: FloatingActionButton.extended(
          backgroundColor: backgroundColor,
          label: Text('Item $index'),
          onPressed: () => _onTapped(index),
        ),
      ),
    );
  }

  ///This function created the FAB Widget
  Widget _buildFab() {
    ///FloatingActionButton using the extended constructor
    return FloatingActionButton.extended(
      label: Text('Menu'),
      onPressed: () {
        ///If the animation controller is dismissed by default, the animation begins on pressing the FAB to display
        ///the other FABs
        if (_controller.isDismissed){
          _controller.forward();
        }
        ///If the animation controller is not dismissed, i.e. animation has taken place, the animation is reversed, i.e.
        ///the other FABs are not displayed
        else {
          _controller.reverse();
        }
      },
      backgroundColor: Colors.blue[900],
      elevation: 10,
    );
  }

  void _onTapped(int index) {
    _controller.reverse();
    widget.onIconTapped(index);
  }
}
```

Refer this link [https://codewithandrea.com/articles/2018-09-13-bottom-bar-navigation-with-fab/](https://codewithandrea.com/articles/2018-09-13-bottom-bar-navigation-with-fab/)

#### Screenshots
[FABExtendedMultipleFABs01](Screenshots/FABExtendedMultipleFABs01.png)  
[FABExtendedMultipleFABs02](Screenshots/FABExtendedMultipleFABs02.png)