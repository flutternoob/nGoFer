# Gist of Flutter

## GridViewBuilder Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///GridView.builder Widget
///The GridView.builder is similar to the ListView.builder Widget. Its main property is the gridDelegate property which
///takes the class SliverGridDelegateWithMaxCrossAxisExtent(). Avoid widget.builder foos for finite lists. Also avoid
///them if many widgets have to be returned in the view (either ListView or GridView). They are most useful when a single
///widget has to be returned (using the itemBuilder property).
///In this example, each item in the grid is arranged using a ListView Widget to get a individually scrolling 'columns'
///of the color palette

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
            child: GridViewWidget(),
          ),
        ),
      ),
    );
  }
}

class GridViewWidget extends StatelessWidget {

  double crossAxisSpacing;

  @override
  Widget build(BuildContext context) {
    ///Checking device orientation, depending on which the crossAxisCount changes
    if (MediaQuery.of(context).orientation == Orientation.portrait)
      crossAxisSpacing = MediaQuery.of(context).size.width*0.05;
    if (MediaQuery.of(context).orientation == Orientation.landscape)
      crossAxisSpacing = MediaQuery.of(context).size.width*0.15;
    return Padding(
      padding: const EdgeInsets.all(20.0),
      child: GridView.builder(
        scrollDirection: Axis.vertical,
        ///The physics property is used to set the type of scrolling. To prevent over-scroll glow, BouncingScrollPhysics()
        ///can be used
        physics: BouncingScrollPhysics(),
        ///Set the addAutomaticKeepAlives property to false for large lists
        addAutomaticKeepAlives: false,
        gridDelegate: SliverGridDelegateWithMaxCrossAxisExtent(
          maxCrossAxisExtent: 100,
          childAspectRatio: 0.1,
          crossAxisSpacing: crossAxisSpacing,
        ),
        itemCount: 4,
        itemBuilder: (context, index) {
          return Container(
            child: ListView(
              children: <Widget>[
                for(dynamic fullColorPaletteItems in fullColorPalette)...[
                  if(fullColorPaletteItems.colorName == 'BLACK')...[
                    for (int blackShadeIndicesValues in blackShadeIndices)
                    ///Calls function for Black and White
                      blackWhiteWidgetMaker(fullColorPaletteItems.colorName, blackShadeIndicesValues),
                  ],
                  if(fullColorPaletteItems.colorName == 'WHITE')...[
                    for (int whiteShadeIndicesValues in whiteShadeIndices)
                    ///Calls function for Black and White
                      blackWhiteWidgetMaker(fullColorPaletteItems.colorName, whiteShadeIndicesValues),
                  ],
                  if(fullColorPaletteItems.colorName != 'BLACK' && fullColorPaletteItems.colorName != 'WHITE')...[
                    for (int materialShadeIndicesValues in materialShadeIndices)
                    ///Calls materialColorMaker function for MaterialColor
                      materialColorMaker(fullColorPaletteItems.primaryColor, materialShadeIndicesValues),
                    if(fullColorPaletteItems.accentColorName != null)...[
                      for (int accentShadeIndicesValues in accentShadeIndices)
                      ///Calls materialColorMaker function for MaterialAccentColor
                        materialColorMaker(fullColorPaletteItems.accentColor, accentShadeIndicesValues),
                    ],
                  ],
                ],
              ],
            )
          );
        },
      ),
    );
  }
}

///Widget function for MaterialColor and MaterialAccentColor
Widget materialColorMaker(dynamic materialColor, int materialShadeIndicesValue){
  return Container(
    width: 50,
    height: 50,
    decoration: BoxDecoration(
        shape: BoxShape.rectangle,
        borderRadius: BorderRadius.all(Radius.circular(10)),
        color: materialColor[materialShadeIndicesValue]),
  );
}

///Widget function for Black and White colors (with opacity as per MaterialDesign Specifications)
Widget blackWhiteWidgetMaker(String colorName, int shadeIndicesValues) {

  Color parentContainerColor;

  if(colorName == 'BLACK'){
    parentContainerColor = Colors.white;
  }
  if(colorName == 'WHITE'){
    parentContainerColor = Colors.black;
  }
  return Container(
      decoration: BoxDecoration(
        shape: BoxShape.rectangle,
        borderRadius: BorderRadius.all(Radius.circular(10)),
        color: parentContainerColor,
      ),
      child: Container(
        width: 50,
        height: 50,
        decoration: BoxDecoration(
          shape: BoxShape.rectangle,
          borderRadius: BorderRadius.all(Radius.circular(10)),
          color: getBlackWhiteColor(colorName, shadeIndicesValues),
        ),
      ));
}

///Data Model for the full color palette (including black and white with opacity), MaterialColor and MaterialAccentColor
class FullColorPalette {

  final String colorName;
  final Color blackWhiteColor;
  final MaterialColor primaryColor;
  final String primaryColorShadeName;
  final String accentColorName;
  final MaterialAccentColor accentColor;
  final String accentColorShadeName;

  FullColorPalette(
      {
        this.colorName,
        this.blackWhiteColor,
        this.primaryColor,
        this.primaryColorShadeName,
        this.accentColorName,
        this.accentColor,
        this.accentColorShadeName
      });
}

///This list is a list of opacity for Black color
final List<int> blackShadeIndices = [12, 26, 38, 45, 54, 87, 100];
///This list is a list of opacity for White color
final List<int> whiteShadeIndices = [10, 12, 24, 30, 38, 54, 60, 70, 100];
///This list is a list of MaterialColor Indices
final List<int> materialShadeIndices = [50, 100, 200, 300, 400, 500, 600, 700, 800, 900];
///This list is a list of MaterialAccentColor Indices
final List<int> accentShadeIndices = [100, 200, 400, 700];

///This variable refers to the Black or White color itself with opacity (eg. Colors.black24)
Color blackWhiteColor;

///This variable contains a list of all the colors in the color palette based on the FullColorPalette class
final List<FullColorPalette> fullColorPalette = [
  FullColorPalette(
      colorName: 'BLACK', blackWhiteColor: blackWhiteColor
  ),
  FullColorPalette(
      colorName: 'WHITE', blackWhiteColor: blackWhiteColor
  ),
  FullColorPalette(
      colorName: 'BLUE', primaryColor: Colors.blue, primaryColorShadeName: 'Colors.blue',
      accentColorName: 'BLUE ACCENT', accentColor: Colors.blueAccent, accentColorShadeName: 'Colors.blueAccent'
  ),
  FullColorPalette(
      colorName: 'LIGHT BLUE', primaryColor: Colors.lightBlue, primaryColorShadeName: 'Colors.lightBlue',
      accentColorName: 'LIGHT BLUE ACCENT', accentColor: Colors.lightBlueAccent, accentColorShadeName: 'Colors.lightBlueAccent'
  ),
  FullColorPalette(
      colorName: 'INDIGO', primaryColor: Colors.indigo, primaryColorShadeName: 'Colors.indigo',
      accentColorName: 'INDIGO ACCENT', accentColor: Colors.indigoAccent, accentColorShadeName: 'Colors.indigoAccent'
  ),
  FullColorPalette(
      colorName: 'DEEP PURPLE', primaryColor: Colors.deepPurple, primaryColorShadeName: 'Colors.deepPurple',
      accentColorName: 'DEEP PURPLE ACCENT', accentColor: Colors.deepPurpleAccent, accentColorShadeName: 'Colors.deepPurpleAccent'
  ),
  FullColorPalette(
      colorName: 'PURPLE', primaryColor: Colors.purple, primaryColorShadeName: 'Colors.purple',
      accentColorName: 'PURPLE ACCENT', accentColor: Colors.purpleAccent, accentColorShadeName: 'Colors.purpleAccent'
  ),
  FullColorPalette(
      colorName: 'CYAN', primaryColor: Colors.cyan, primaryColorShadeName: 'Colors.cyan',
      accentColorName: 'CYAN ACCENT', accentColor: Colors.cyanAccent, accentColorShadeName: 'Colors.cyanAccent'
  ),
  FullColorPalette(
      colorName: 'TEAL', primaryColor: Colors.teal, primaryColorShadeName: 'Colors.teal',
      accentColorName: 'TEAL ACCENT', accentColor: Colors.tealAccent, accentColorShadeName: 'Colors.tealAccent'
  ),
  FullColorPalette(
      colorName: 'GREEN', primaryColor: Colors.green, primaryColorShadeName: 'Colors.green',
      accentColorName: 'GREEN ACCENT', accentColor: Colors.greenAccent, accentColorShadeName: 'Colors.greenAccent'
  ),
  FullColorPalette(
      colorName: 'LIGHT GREEN', primaryColor: Colors.lightGreen, primaryColorShadeName: 'Colors.lightGreen',
      accentColorName: 'LIGHT GREEN ACCENT', accentColor: Colors.lightGreenAccent, accentColorShadeName: 'Colors.lightGreenAccent'
  ),
  FullColorPalette(
      colorName: 'LIME', primaryColor: Colors.lime, primaryColorShadeName: 'Colors.lime',
      accentColorName: 'LIME ACCENT', accentColor: Colors.limeAccent, accentColorShadeName: 'Colors.limeAccent'
  ),
  FullColorPalette(
      colorName: 'YELLOW', primaryColor: Colors.yellow, primaryColorShadeName: 'Colors.yellow',
      accentColorName: 'YELLOW ACCENT', accentColor: Colors.yellowAccent, accentColorShadeName: 'Colors.yellowAccent'
  ),
  FullColorPalette(
      colorName: 'YELLOW', primaryColor: Colors.yellow, primaryColorShadeName: 'Colors.yellow',
      accentColorName: 'YELLOW ACCENT', accentColor: Colors.yellowAccent, accentColorShadeName: 'Colors.yellowAccent'
  ),
  FullColorPalette(
      colorName: 'AMBER', primaryColor: Colors.amber, primaryColorShadeName: 'Colors.amber',
      accentColorName: 'AMBER ACCENT', accentColor: Colors.amberAccent, accentColorShadeName: 'Colors.amberAccent'
  ),
  FullColorPalette(
      colorName: 'ORANGE', primaryColor: Colors.orange, primaryColorShadeName: 'Colors.orange',
      accentColorName: 'ORANGE ACCENT', accentColor: Colors.orangeAccent, accentColorShadeName: 'Colors.orangeAccent'
  ),
  FullColorPalette(
      colorName: 'DEEP ORANGE', primaryColor: Colors.deepOrange, primaryColorShadeName: 'Colors.deepOrange',
      accentColorName: 'DEEP ORANGE ACCENT', accentColor: Colors.deepOrangeAccent, accentColorShadeName: 'Colors.deepOrangeAccent'
  ),
  FullColorPalette(
      colorName: 'RED', primaryColor: Colors.red, primaryColorShadeName: 'Colors.red',
      accentColorName: 'RED ACCENT', accentColor: Colors.redAccent, accentColorShadeName: 'Colors.redAccent'
  ),
  FullColorPalette(
      colorName: 'PINK', primaryColor: Colors.pink, primaryColorShadeName: 'Colors.pink',
      accentColorName: 'PINK ACCENT', accentColor: Colors.pinkAccent, accentColorShadeName: 'Colors.pinkAccent'
  ),
  FullColorPalette(
    colorName: 'BLUE GREY', primaryColor: Colors.blueGrey, primaryColorShadeName: 'Colors.blueGrey',
  ),
  FullColorPalette(
    colorName: 'BROWN', primaryColor: Colors.brown, primaryColorShadeName: 'Colors.brown',
  ),
  FullColorPalette(
    colorName: 'GREY', primaryColor: Colors.grey, primaryColorShadeName: 'Colors.grey',
  ),
];

///This function is used to determine how much opacity has to applied to Black or White depending on the list of indices
///for Black and White respectively. The index has to be converted to a double as its original type is an int expressed
///as % and the withOpacity method accepts only a double (between 0 and 1)
getBlackWhiteColor(String blackWhiteColorName, int shadeIndex) {
  if(blackWhiteColorName == 'BLACK')
    shadeIndex != 100? blackWhiteColor = Colors.black.withOpacity((shadeIndex).toDouble()/100): blackWhiteColor = Colors.black;
  if(blackWhiteColorName == 'WHITE')
    shadeIndex != 100? blackWhiteColor = Colors.white.withOpacity((shadeIndex).toDouble()/100): blackWhiteColor = Colors.white;
  return blackWhiteColor;
}
```

#### Screenshots

[GridViewBuilderWidget01](Screenshots/GridViewBuilderWidget01.png)  
[GridViewBuilderWidget02](Screenshots/GridViewBuilderWidget02.png)