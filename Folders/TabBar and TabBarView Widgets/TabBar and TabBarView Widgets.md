# Gist of Flutter

## TabBar and TabBarView Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///TabBar and TabBarView
///The TabBar Widget is used to display a list of tabs in the app bar. It is often used in conjunction with the TabBarView
///Widget, although it is not mandatory to use the TabBarView widget. The major properties of the TabBar Widget are the
///controller and the tabs properties. The TabBar Widget itself is assigned to the 'bottom' property of the AppBar Widget.
///If the TabBarView Widget is used, both the TabBar and the TabBarView Widget should have the same controller.

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {

  final List numbers = [1, 2, 3, 4, 5, 6];

  @override
  _MyAppState createState() => _MyAppState();
}

///Since animation is implemented for the TabBar, SingleTickerProviderStateMixin should be extended along with the State
///of the Stateful Widget
class _MyAppState extends State<MyApp> with SingleTickerProviderStateMixin {

  ///Declaring the TabController
  TabController _tabController;
  int index = 0;
  bool tabBar = false;

  @override
  void initState() {
    ///Initializing the TabController. The length and vsync properties are required. The initialIndex property is optional
    ///and can be used to set the default tab to be shown in the TabBarView, based on the number of Tabs, i.e the length
    _tabController = TabController(length: 6, vsync: this);
    super.initState();
  }

  @override
  void dispose() {
    super.dispose();
    ///Dispose the TabController
    _tabController.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          leading: IconButton(
            icon: Icon(Icons.swap_vert),
            onPressed: () {
              setState(() {
                tabBar = !tabBar;
                index = 0;
              });
            },
          ),
          title: Text('Demo App'),
          centerTitle: true,
          ///The TabBar() Widget is assigned to the AppBar() Widget's 'bottom' property
          bottom:  TabBar(
            ///The onTap property is mandatory only if a TabBarView Widget is not used in conjunction with the TabBar
            ///Widget
            onTap: (int){
              if (tabBar == false)
                setState(() {
                  index = int;
                });
            },
            ///If there are many tabs, set the isScrollable property to true
            isScrollable: true,
            labelStyle: TextStyle(fontSize: 16),
            indicatorPadding: EdgeInsets.all(8),
            indicatorSize: TabBarIndicatorSize.tab,
            indicatorWeight: 5,
            ///The tabs property in the TabBar widget takes a list of Tab Widgets
            tabs: [
              for(int value in widget.numbers)
                Tab(
                  text: 'Item $value',
                  icon: Icon(Icons.adb, size: 16,),
                )
            ],
            ///The TabController is passed to the controller property of the TabBar
            controller: _tabController,
          )
        ),
        body: tabBar == false?
        Center(
          child: Text('Tab Number: ${widget.numbers[index]}', style: TextStyle(fontSize: 20, fontWeight: FontWeight.w500)),
        ):
        ///The TabBarView Widget is not mandatory, but is recommended for better user experience when it comes to scrolling
        ///between different tabs and their respective content
        TabBarView(
          children: [
            for (int value in widget.numbers)
              DummyWidget(tabNumber: value,)
          ],
          ///The TabView controller that is used by the TabBar is passed in the controller property of the TabBarView widget
          controller: _tabController
        ),
      ),
    );
  }
}

///Dummy Widget used to display the tab number in the Scaffold's body
class DummyWidget extends StatelessWidget {

  final int tabNumber;

  DummyWidget({this.tabNumber});

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Tab Number: $tabNumber', style: TextStyle(fontSize: 20, fontWeight: FontWeight.w500))
    );
  }
}
```

#### Screenshots
[TabBarTabBarViewWidgets01](Screenshots/TabBarTabBarViewWidgets01.png)  
[TabBarTabBarViewWidgets02](Screenshots/TabBarTabBarViewWidgets02.png)