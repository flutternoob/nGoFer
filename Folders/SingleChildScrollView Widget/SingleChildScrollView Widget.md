# Gist of Flutter

## SingleChildScrollView Widget

#### Code
```Java
import 'package:flutter/material.dart';

///SingleChildScrollView Widget
///This Widget is useful if its child, which is an otherwise non-scrollable widget such as a Row or Column Widget, needs
///to be made scrollable. This Widget takes a single child Widget which is made scrollable. If a Row Widget is used, set
///the scrollDirection to Axis.horizontal. If a Column Widget is used, set the scrollDirection to Axis.vertical.

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
        body: SingleChildScrollViewWidget(),
      ),
    );
  }
}

class SingleChildScrollViewWidget extends StatefulWidget {
  @override
  _SingleChildScrollViewWidgetState createState() => _SingleChildScrollViewWidgetState();
}

class _SingleChildScrollViewWidgetState extends State<SingleChildScrollViewWidget> {
  @override
  Widget build(BuildContext context) {
    Orientation orientation = MediaQuery.of(context).orientation;
    return SingleChildScrollView(
      physics: BouncingScrollPhysics(),
      scrollDirection: orientation == Orientation.landscape ? Axis.horizontal : Axis.vertical,
      child: orientation == Orientation.landscape
          ? Row(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              mainAxisSize: MainAxisSize.min,
              children: [
                for (String imagePath in imagePaths)
                  Padding(
                    padding: const EdgeInsets.all(10.0),
                    child: Card(
                      clipBehavior: Clip.antiAlias,
                      elevation: 10,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.all(Radius.circular(15))
                      ),
                      child: Image.asset(imagePath),
                    ),
                  )
              ],
            )
          : Column(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              mainAxisSize: MainAxisSize.min,
              children: [
                for (String imagePath in imagePaths)
                  Padding(
                    padding: const EdgeInsets.all(10.0),
                    child: Card(
                      clipBehavior: Clip.antiAlias,
                      elevation: 10,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.all(
                          Radius.circular(15),
                        ),
                      ),
                      child: Image.asset(imagePath),
                    ),
                  )
              ],
            ),
    );
  }
}

final List<String> imagePaths = [
  "assets/cars/Cars01.jpg",
  "assets/cars/Cars02.jpg",
  "assets/cars/Cars03.jpg",
  "assets/cars/Cars04.jpg",
  "assets/cars/Cars05.jpg",
  "assets/cars/Cars06.jpg",
  "assets/cars/Cars07.jpg",
  "assets/cars/Cars08.jpg",
  "assets/cars/Cars09.jpg",
  "assets/cars/Cars10.jpg",
  "assets/cars/Cars11.jpg"
];
```

#### Screenshots
[SingleChildScrollViewWidget01](Screenshots/SingleChildScrollViewWidget01.png)  
[SingleChildScrollViewWidget02](Screenshots/SingleChildScrollViewWidget02.png)