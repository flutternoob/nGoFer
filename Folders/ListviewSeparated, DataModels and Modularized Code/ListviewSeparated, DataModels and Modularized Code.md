# Gist of Flutter

## ListviewSeparated, DataModels and Modularized Code

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///ListView.separated Widget and Data Modelling (and Modularizing)
///The ListView.separated Widget is like an extension of the ListView Widget. It is similar to the ListView.builder
///Widget, the only difference being that unlike the ListView.builder Widget, it has a separatorBuilder property for
///a Widget that can be used for a separator between the other widgets in the list. The separator can be any Widget, like
///the Divider Widget. The other main properties of the ListView.separated Widget are the itemCount (which is usually the
///length of a list) and the itemBuilder property which uses a BuildContext and an int (index) as arguments and returns
///a Widget.

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
            child: ListViewSeparatedWidget(),
          ),
        ),
      ),
    );
  }
}

class ListViewSeparatedWidget extends StatefulWidget {
  @override
  _ListViewSeparatedWidgetState createState() => _ListViewSeparatedWidgetState();
}

class _ListViewSeparatedWidgetState extends State<ListViewSeparatedWidget> {

  @override
  Widget build(BuildContext context) {
    return ListView.separated(
      itemCount: fullColorPalette.length,
      itemBuilder: (context, index) {
        return Column(
          children: <Widget>[
            ///Checking the color's name from the fullColorPalette list to determine which Widget function to call
            if (fullColorPalette[index].colorName == 'BLACK' || fullColorPalette[index].colorName == 'WHITE')
            ///Calls function for Black and White
              blackWhiteWidgetMaker(fullColorPalette[index].colorName),
            if (fullColorPalette[index].colorName != 'BLACK' && fullColorPalette[index].colorName != 'WHITE')...[
              ///Calls materialColorMaker function for MaterialColor
              materialColorMaker(fullColorPalette[index].colorName, fullColorPalette[index].primaryColorShadeName,
                  fullColorPalette[index].primaryColor),
              ///The below check is required as not all material colors have their respective accent colors (such as Brown)
              if(fullColorPalette[index].accentColorName != null)
              ///Calls materialColorMaker function for MaterialAccentColor
                materialColorMaker(fullColorPalette[index].accentColorName, fullColorPalette[index].accentColorShadeName,
                    fullColorPalette[index].accentColor),
            ],
          ],
        );
      },
      separatorBuilder: (context, index) {
        return Padding(
          padding: const EdgeInsets.symmetric(horizontal: 50.0),
          child: Divider(
            color: Colors.black,
            indent: 50,
            endIndent: 50,
            thickness: 2,
          ),
        );
      },
    );
  }
}

///Widget function for MaterialColor and MaterialAccentColor
Widget materialColorMaker(String materialColorName, String materialShadeName, dynamic materialColor){

  List<int> materialColorIndices;

  !materialColorName.contains('ACCENT')? materialColorIndices = materialShadeIndices: materialColorIndices = accentShadeIndices;

  return Padding(
    padding: const EdgeInsets.all(20.0),
    child: Card(
      elevation: 10,
      shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.all(Radius.circular(15))
      ),
      child: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: <Widget>[
          Padding(
            padding: const EdgeInsets.all(10.0),
            child: Text(materialColorName, style: TextStyle(fontSize: 20),),
          ),
          for(int materialColorIndex = 0; materialColorIndex < materialColorIndices.length; materialColorIndex++)...[
            Padding(
              padding: const EdgeInsets.all(10.0),
              child: ListTile(
                ///Representing the name of the color with its index (eg. Colors.blue[500])
                title: Text('$materialShadeName[${materialColorIndices[materialColorIndex]}]', style: TextStyle(fontSize: 16),),
                ///Representing the color as a hex value
                subtitle: Text('#${materialColor[materialColorIndices[materialColorIndex]].value.toRadixString(16).replaceRange(0, 2, '')}'),
                trailing: Container(
                  width: 50,
                  decoration: BoxDecoration(
                      shape: BoxShape.rectangle,
                      borderRadius: BorderRadius.all(Radius.circular(10)),
                      color: materialColor[materialColorIndices[materialColorIndex]]),
                ),
              ),
            ),
          ],
        ],
      ),
    ),
  );
}

///Widget function for Black and White colors (with opacity as per MaterialDesign Specifications)
Widget blackWhiteWidgetMaker(String colorName) {

  List<int> shadeListIndices;
  Color parentContainerColor;

  if(colorName == 'BLACK'){
    shadeListIndices = blackShadeIndices;
    parentContainerColor = Colors.white;
  }
  if(colorName == 'WHITE'){
    shadeListIndices = whiteShadeIndices;
    parentContainerColor = Colors.black;
  }
  return Column(
    children: <Widget>[
      Padding(
        padding: const EdgeInsets.all(20.0),
        child: Card(
          elevation: 10,
          shape: RoundedRectangleBorder(
              borderRadius: BorderRadius.all(Radius.circular(15))
          ),
          child: Column(
            children: <Widget>[
              Padding(
                padding: const EdgeInsets.all(10.0),
                child: Text(colorName, textAlign: TextAlign.center, style: TextStyle(fontSize: 20),),
              ),
              for (int shadeIndicesValues in shadeListIndices)...[
                Padding(
                  padding: const EdgeInsets.all(10.0),
                  child: ListTile(
                    title: Text('${getBlackWhiteShadeName(colorName, shadeIndicesValues)}'),
                    subtitle: Text('${getBlackWhiteColorIntValue(colorName, shadeIndicesValues)}'),
                    trailing: Container(
                        decoration: BoxDecoration(
                          shape: BoxShape.rectangle,
                          borderRadius: BorderRadius.all(Radius.circular(10)),
                          color: parentContainerColor,
                        ),
                        child: Container(
                          width: 50,
                          decoration: BoxDecoration(
                            shape: BoxShape.rectangle,
                            borderRadius: BorderRadius.all(Radius.circular(10)),
                            color: getBlackWhiteColor(colorName, shadeIndicesValues),
                          ),
                        )),
                  ),
                )
              ]
            ],
          ),
        ),
      ),
    ],
  );
}

///Data Model for the full color palette (including black and white with opacity), MaterialColor and MaterialAccentColor
class FullColorPalette {

  final String colorName;
  final Color blackWhiteColor;
  final String blackWhiteShadeName;
  final MaterialColor primaryColor;
  final String primaryColorShadeName;
  final String accentColorName;
  final MaterialAccentColor accentColor;
  final String accentColorShadeName;

  FullColorPalette(
      {
        this.colorName,
        this.blackWhiteColor,
        this.blackWhiteShadeName,
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

///This variables refers to the name of the Black or White shade with opacity (eg. Colors.black12, 12 being the opacity)
String blackWhiteShadeName;
///This variable refers to the Black or White color itself with opacity (eg. Colors.black24)
Color blackWhiteColor;
///This variable refers to the color Black or White (with opacity) shade expressed as an Android integer
String colorIntValue;

///This variable contains a list of all the colors in the color palette based on the FullColorPalette class
final List<FullColorPalette> fullColorPalette = [
  FullColorPalette(
      colorName: 'BLACK', blackWhiteColor: blackWhiteColor, blackWhiteShadeName: blackWhiteShadeName
  ),
  FullColorPalette(
      colorName: 'WHITE', blackWhiteColor: blackWhiteColor, blackWhiteShadeName: blackWhiteShadeName
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

///The below 3 functions are for Black and White only

///This function determines the Android int value of the given shade of Black or White (with opacity)
getBlackWhiteColorIntValue(String blackWhiteColorName, int shadeIndex) {
  if(blackWhiteColorName == 'BLACK')
    shadeIndex != 100? colorIntValue = ('${Colors.black.withOpacity((shadeIndex).toDouble()/100)}'): colorIntValue = '${Colors.black}';
  if(blackWhiteColorName == 'WHITE')
    shadeIndex != 100? colorIntValue = ('${Colors.white.withOpacity((shadeIndex).toDouble()/100)}'): colorIntValue = '${Colors.white}';
  return colorIntValue;
}

///This function is used only to represent (in the app) the name of the shade of Black or White (with opacity)
getBlackWhiteShadeName(String blackWhiteColorName, int shadeIndex) {
  if(blackWhiteColorName == 'BLACK')
    shadeIndex != 100? blackWhiteShadeName = 'Colors.black$shadeIndex': blackWhiteShadeName = 'Colors.black';
  if(blackWhiteColorName == 'WHITE')
    shadeIndex != 100? blackWhiteShadeName = 'Colors.white$shadeIndex': blackWhiteShadeName = 'Colors.white';
  return blackWhiteShadeName;
}

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
[ListviewSeparatedDataModelsModularizedCode01](Screenshots/ListviewSeparatedDataModelsModularizedCode01.png)  
[ListviewSeparatedDataModelsModularizedCode02](Screenshots/ListviewSeparatedDataModelsModularizedCode02.png)