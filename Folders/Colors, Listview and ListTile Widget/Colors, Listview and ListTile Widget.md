# Gist of Flutter

## Colors, Listview and ListTile Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Colors, ListView and ListTile Widget
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
          body: Center(child: ListViewWidget()),
        ),
      ),
    );
  }
}

///The ListView Widget is a scrollable widget that takes a list of widgets as one of its parameters. The other main
///property of the ListView Widget is the scrollDirection property which can be either horizontal or vertical.

class ListViewWidget extends StatefulWidget {
  @override
  _ListViewWidgetState createState() => _ListViewWidgetState();
}

class _ListViewWidgetState extends State<ListViewWidget> {

  ///These are the indices used to represent different shades of a given primary color. For eg., the color blue can be
  ///represented as Colors.blue[100], where 100 is the index. An alternative way of giving a color a shade is
  ///colors.blue.shade100
  List<int> primaryIndices = [100, 200, 300, 400, 500, 600, 700, 800, 900];

  ///These are the indices used to represent different shades of a given accent color. They can be represented in the
  ///same ways as the primary colors (according to MaterialDesign specifications)
  List<int> accentIndices = [100, 200, 400, 700];

  ///These are primary colors as per the MaterialDesign Specifications
  List<MaterialColor> primaryColorListColors = [
    Colors.blue,
    Colors.lightBlue,
    Colors.indigo,
    Colors.blueGrey,
    Colors.deepPurple,
    Colors.purple,
    Colors.cyan,
    Colors.teal,
    Colors.green,
    Colors.lightGreen,
    Colors.lime,
    Colors.yellow,
    Colors.amber,
    Colors.orange,
    Colors.deepOrange,
    Colors.red,
    Colors.pink,
    Colors.brown,
    Colors.grey
  ];

  ///These are the accent colors as per the MaterialDesign specifications
  List<MaterialAccentColor> accentColorListColors = [
    Colors.blueAccent,
    Colors.lightBlueAccent,
    Colors.indigoAccent,
    Colors.deepPurpleAccent,
    Colors.purpleAccent,
    Colors.cyanAccent,
    Colors.tealAccent,
    Colors.greenAccent,
    Colors.lightGreenAccent,
    Colors.limeAccent,
    Colors.yellowAccent,
    Colors.amberAccent,
    Colors.orangeAccent,
    Colors.deepOrangeAccent,
    Colors.redAccent,
    Colors.pinkAccent,
  ];

  List<String> primaryColorList = [
    'Blue',
    'Light Blue',
    'Indigo',
    'Blue Grey',
    'Deep Purple',
    'Purple',
    'Cyan',
    'Teal',
    'Green',
    'Light Green',
    'Lime',
    'Yellow',
    'Amber',
    'Orange',
    'Deep Orange',
    'Red',
    'Pink',
    'Brown',
    'Grey'
  ];

  List<String> accentColorList = [
    'Blue Accent',
    'Light Blue Accent',
    'Indigo Accent',
    'Deep Purple Accent',
    'Purple Accent',
    'Cyan Accent',
    'Teal Accent',
    'Green Accent',
    'Light Green Accent',
    'Lime Accent',
    'Yellow Accent',
    'Amber Accent',
    'Orange Accent',
    'Deep Orange Accent',
    'Red Accent',
    'Pink Accent'
  ];

  ///These are the shades of black according to MaterialDesign specifications. The number at the end of the Color
  ///indicates the amount of opacity (in percent) applied to the color black. For eg., Colors.black12 shows that this
  ///is the color black with 12% opacity. Note: if the parent widget is also black, then the color is not represented
  ///correctly. For it to be represented correctly, set the color property of the parent widget (such as a Container) to
  ///white (or any other color depending on use case)
  List<Color> blackColors = [
    Colors.black12,
    Colors.black26,
    Colors.black38,
    Colors.black45,
    Colors.black54,
    Colors.black87,
    Colors.black
  ];

  ///These are the shades of white according to MaterialDesign specifications. The number at the end of the Color
  ///indicates the amount of opacity (in percent) applied to the color white. For eg., Colors.white10 shows that this
  ///is the color white with 10% opacity. Note: if the parent widget is also white, then the color is not represented
  ///correctly. For it to be represented correctly, set the color property of the parent widget (such as a Container) to
  ///black (or any other color depending on use case)
  List<Color> whiteColors = [
    Colors.white10,
    Colors.white12,
    Colors.white24,
    Colors.white30,
    Colors.white38,
    Colors.white54,
    Colors.white60,
    Colors.white70,
    Colors.white
  ];

  String blackColorName = 'Black';
  String whiteColorName = 'White';
  String materialColorName = 'Material';
  String accentColorName = 'Accent';

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: Text(
            'Black Shades',
            textAlign: TextAlign.center,
            style: TextStyle(fontSize: 20),
          ),
        ),
        for (int index = 0; index < blackColors.length; index++) ...[
          customListTileWidget(blackColors[index], blackColorName, '${blackColors[index].toString()}')
        ],
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: Text(
            'White Shades',
            textAlign: TextAlign.center,
            style: TextStyle(fontSize: 20),
          ),
        ),
        for (int index = 0; index < whiteColors.length; index++) ...[
          customListTileWidget(whiteColors[index], whiteColorName, '${whiteColors[index].toString()}')
        ],
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: Text(
            'Primary Color Shades',
            textAlign: TextAlign.center,
            style: TextStyle(fontSize: 20),
          ),
        ),
        for (int index = 0; index < primaryColorListColors.length; index++) ...[
          for (int i = 0; i < primaryIndices.length; i++)
            customListTileWidget(primaryColorListColors[index][primaryIndices[i]], primaryColorList[index],
                materialColorName, primaryIndices[i]),
        ],
        Padding(
          padding: const EdgeInsets.all(10.0),
          child: Text(
            'Accent Color Shades',
            textAlign: TextAlign.center,
            style: TextStyle(fontSize: 20),
          ),
        ),
        for (int index = 0; index < accentColorListColors.length; index++) ...[
          for (int i = 0; i < accentIndices.length; i++)
            customListTileWidget(accentColorListColors[index][accentIndices[i]], accentColorList[index],
                accentColorName, accentIndices[i]),
        ],
      ],
    );
  }
}

///The ListTile Widget is a widget that can be used to represent some information. The main properties are the title and
///subtitle properties which can be any widget (such as a Text Widget). The other two main properties are the leading and
///trailing properties which can be any widget (such as an Icon Widget). The onTap() property is used to carry out a
///function such as navigation.

Widget customListTileWidget(Color color, String colorName, String colorTypeIdentifier, [int index]) {
  if (colorName == 'Black') {
    return Container(
      color: Colors.white,
      child: Container(
          color: color,
          child: ListTile(
            title: Text(
              colorName,
              style: TextStyle(color: Colors.white),
            ),
            subtitle: Text(
              colorTypeIdentifier,
              style: TextStyle(color: Colors.white),
            ),
          )),
    );
  } else if (colorName == 'White') {
    return Container(
      color: Colors.black,
      child: Container(
          color: color,
          child: ListTile(
            title: Text(
              colorName,
              style: TextStyle(color: Colors.black),
            ),
            subtitle: Text(
              colorTypeIdentifier,
              style: TextStyle(color: Colors.black),
            ),
          )),
    );
  } else if (colorName == 'Material') {
    return Container(
        color: color,
        child: ListTile(
          title: Text(colorName),
          subtitle: Text('$index'),
        ));
  } else {
    return Container(
        width: 100,
        color: color,
        child: ListTile(
          title: Text(colorName),
          subtitle: Text('$index'),
        ));
  }
}
```

Refer this link [https://www.materialpalette.com/colors](https://www.materialpalette.com/colors)  
Refer ths link [https://api.flutter.dev/flutter/material/Colors/white10-constant.html](https://api.flutter.dev/flutter/material/Colors/white10-constant.html)  
Refer this link [https://pusher.com/tutorials/flutter-listviews](https://pusher.com/tutorials/flutter-listviews)  
and this link [https://medium.com/@suragch/a-complete-guide-to-flutters-listtile-597a20a3d449](https://medium.com/@suragch/a-complete-guide-to-flutters-listtile-597a20a3d449)

#### Screenshots

[ColorsListviewListTileWidget01](Screenshots/ColorsListviewListTileWidget01.png)  
[ColorsListviewListTileWidget02](Screenshots/ColorsListviewListTileWidget02.png)  
[ColorsListviewListTileWidget03](Screenshots/ColorsListviewListTileWidget03.png)  
[ColorsListviewListTileWidget04](Screenshots/ColorsListviewListTileWidget04.png)  
[ColorsListviewListTileWidget05](Screenshots/ColorsListviewListTileWidget05.png)  
[ColorsListviewListTileWidget06](Screenshots/ColorsListviewListTileWidget06.png)