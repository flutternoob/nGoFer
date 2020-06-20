# Gist of Flutter

## Drawer Widget, Custom Widget and ExitApp Function

#### Code
```Java
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

void main() => runApp(MyApp());

///Drawer Widget, Custom Widget and Exit App function
///The Drawer Widget can be any widget that shows a menu of some sort. Either Flutter's default Drawer() Widget can be
///used along with either a UserAccountDrawerHeader() Widget or a regular DrawerHeader() Widget. Optionally the
///DrawerHeader() Widget need not be used. Also, a custom Menu can be created without using the built-in default Drawer()
///and DrawerHeader() Widgets.

///The two main steps to perform while calling a Widget that has Menu/Drawer functionality are:
///1) Set the drawer property of the Scaffold Widget to the Menu Widget's name like so - drawer: MenuWidget()
///2) Call the openDrawer() function using the Scaffold's context using the Scaffold's context like so:
///Scaffold.of(context).openDrawer(). For this to work, a Scaffold's context must be available.

///StatefulWidget is used as the app's entry point widget as the state of the Widget has to be updated depending on
///the custom menu to be shown.
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool drawerChoice;

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    drawerChoice = false;
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Scaffold(
          ///Drawer property has to be set
          drawer: drawerChoice ? CustomDrawerWidgetOne() : CustomDrawerWidgetTwo(),
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
            leading: Builder(builder: (context) {
              return IconButton(
                icon: Icon(Icons.menu, color: Colors.blue[200]),
                onPressed: () {
                  setState(() {
                    drawerChoice = !drawerChoice;
                  });
                  ///Call the openDrawer() function using the below statement (ensure Scaffold's context is available).
                  Scaffold.of(context).openDrawer();
                },
              );
            }),
          ),
          body: Center(
            child: Padding(
              padding: const EdgeInsets.all(20.0),
              child: Text(
                'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam leo lorem, iaculis et egestas sed, '
                    'ultricies vel ligula. Suspendisse potenti. Donec ac elit dui. Aliquam molestie mattis risus quis '
                    'posuere. Nulla sodales, metus vel interdum fringilla, ligula dolor porttitor velit, quis gravida '
                    'augue eros faucibus lectus. Donec consectetur dictum sem nec egestas. Mauris molestie tortor metus, '
                    'non faucibus purus sodales ac. Vivamus laoreet elit sed sapien commodo fringilla sed id erat. Donec '
                    'varius ex at lectus aliquam varius. Etiam nec auctor velit. Quisque rhoncus lorem at ex auctor tempus. '
                    'Morbi ut enim in elit euismod gravida ut eget velit. Mauris at velit eros. Donec maximus elit at '
                    'rutrum scelerisque. Vivamus auctor eget lacus ac sollicitudin.',
                textAlign: TextAlign.justify,
              ),
            ),
          ),
        ),
      ),
    );
  }
}

///Custom Drawer Widget - without using the built-in Drawer() and DrawerHeader() Widgets
class CustomDrawerWidgetOne extends StatefulWidget {
  @override
  _CustomDrawerWidgetOneState createState() => _CustomDrawerWidgetOneState();
}

class _CustomDrawerWidgetOneState extends State<CustomDrawerWidgetOne> {
  ItemList itemList = ItemList();
  List<dynamic> theList;

  @override
  initState() {
    super.initState();
    theList = itemList.menuItems;
  }

  @override
  Widget build(BuildContext context) {
    return Align(
      alignment: Alignment.topLeft,
      child: Container(
        width: 220,
        height: 720,
        child: Opacity(
          opacity: 0.7,
          child: Container(
            decoration: BoxDecoration(
              color: Colors.black,
              shape: BoxShape.rectangle,
              border: Border.all(color: Colors.black, width: 2),
              borderRadius: BorderRadius.only(
                topRight: Radius.circular(30.9016994),
                bottomRight: Radius.circular(30.9016994),
              ),
              boxShadow: [
                BoxShadow(
                  color: Colors.black26,
                  offset: new Offset(7.0, 7.0),
                  blurRadius: 5.0,
                )
              ],
            ),
            ///To make the the custom drawer header sticky, first create a Column() widget whose children can be two
            ///Container() Widgets (whose parent Widgets are Expanded Widgets). Wrap the header in the first Container()
            ///Widget with a given size. The second Container() Widget should have a ListView (or any other scrollable)
            ///Widget as its child Widget.
            child: Column(
              children: <Widget>[
                Expanded(
                  flex: 0,
                  child: Container(
                    width: 220,
                    height: 150,
                    decoration: BoxDecoration(
                        image: DecorationImage(image: AssetImage('assets/cars/Cars11.jpg'), fit: BoxFit.cover),
                        borderRadius: BorderRadius.only(topRight: Radius.circular(30.9016994))),
                    child: Align(
                      alignment: Alignment.bottomLeft,
                      child: Padding(
                        padding: const EdgeInsets.all(10.0),
                        child: Text('Menu', style: TextStyle(color: Colors.white70)),
                      ),
                    ),
                  ),
                ),
                MenuListWidget(
                  theList: theList,
                  menuIdentifier: 'One',
                )
              ],
            ),
          ),
        ),
      ),
    );
  }
}

///Custom Drawer Widget Two - using the built-in Drawer() Widget and UserAccountDrawerHeader() Widget
class CustomDrawerWidgetTwo extends StatefulWidget {
  @override
  _CustomDrawerWidgetTwoState createState() => _CustomDrawerWidgetTwoState();
}

class _CustomDrawerWidgetTwoState extends State<CustomDrawerWidgetTwo> {
  ItemList itemList = ItemList();
  List<dynamic> theList;

  @override
  initState() {
    super.initState();
    theList = itemList.menuItems;
  }

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: Column(
        children: <Widget>[
          Container(
            child: UserAccountsDrawerHeader(
                decoration: BoxDecoration(
                  color: Colors.black87,
                ),
                currentAccountPicture: CircleAvatar(
                  backgroundImage: AssetImage('assets/cars/Cars04.jpg'),
                ),

                ///The accountName and accountEmail properties are required if the UserAccountsDrawerHeader() Widget is used.
                accountName: Text('User Name'),
                accountEmail: Text('someEmail@someEmail.com')),
          ),
          MenuListWidget(
            theList: theList,
            menuIdentifier: 'Two',
          )
        ],
      ),
    );
  }
}

///Custom Widget extracted from the two Custom Drawer Widgets and modularized for both drawers to avoid code repetition
///This Widget has two main properties: theList property which is the List of items in the menu and a menu identifier
///to determine which textStyle and icon color to apply (depending whether the menu to be displayed is the first or
///second custom drawer widget
class MenuListWidget extends StatefulWidget {
  const MenuListWidget({Key key, @required this.theList, @required this.menuIdentifier}) : super(key: key);

  final List theList;
  final String menuIdentifier;

  @override
  _MenuListWidgetState createState() => _MenuListWidgetState();
}

class _MenuListWidgetState extends State<MenuListWidget> {
  @override
  Widget build(BuildContext context) {
    return Expanded(
      child: ListView(
        children: widget.theList
            .map((theListItem) => ListTile(
                  title: Text(theListItem.title,
                      style: widget.menuIdentifier == 'One' ? theListItem.textStyle : TextStyle(color: Colors.black)),
                  trailing:
                      Icon(theListItem.iconData, color: widget.menuIdentifier == 'One' ? theListItem.iconColor : Colors.black),
                  onTap: () {
                    if (theListItem.title == 'Exit')
                      ///The following statement is used to allow the user to exit from the app (to minimize device
                      ///resources used by the app). Do not implement this feature if the app is being developed for
                      ///the Apple Store as Apple does not allow app exit in this manner.
                      SystemChannels.platform.invokeMethod('SystemNavigator.pop');
                  },
                ))
            .toList(),
      ),
    );
  }
}

///Model used to generate a List of items
class MenuItem {
  bool isTapped;
  String title;
  IconData iconData;
  TextStyle textStyle;
  Color iconColor;

  MenuItem(
      {this.isTapped: false,
      this.title,
      this.iconData,
      this.textStyle: const TextStyle(color: Colors.white70),
      this.iconColor: Colors.white70});
}

class ItemList {
  MenuItem menuItem = MenuItem();

  List<MenuItem> menuItems = [
    MenuItem(
      title: 'Item 1',
      iconData: Icons.home,
    ),
    MenuItem(
      title: 'Item 2',
      iconData: Icons.subject,
    ),
    MenuItem(
      title: 'Item 3',
      iconData: Icons.list,
    ),
    MenuItem(
      title: 'Item 4',
      iconData: Icons.subject,
    ),
    MenuItem(
      title: 'Item 5',
      iconData: Icons.help_outline,
    ),
    MenuItem(
      title: 'Item 6',
      iconData: Icons.share,
    ),
    MenuItem(
      title: 'Item 7',
      iconData: Icons.perm_device_information,
    ),
    MenuItem(
      title: 'Item 8',
      iconData: Icons.remove_circle_outline,
    ),
    MenuItem(
      title: 'Item 9',
      iconData: Icons.email,
    ),
    MenuItem(
      title: 'Exit',
      iconData: Icons.exit_to_app,
    )
  ];
}
```

#### Screenshots

[DrawerWidgetCustomWidgetExitAppFunction01](Screenshots/DrawerWidgetCustomWidgetExitAppFunction01.png)  
[DrawerWidgetCustomWidgetExitAppFunction02](Screenshots/DrawerWidgetCustomWidgetExitAppFunction02.png)  
[DrawerWidgetCustomWidgetExitAppFunction03](Screenshots/DrawerWidgetCustomWidgetExitAppFunction03.png)  
[DrawerWidgetCustomWidgetExitAppFunction04](Screenshots/DrawerWidgetCustomWidgetExitAppFunction04.png)