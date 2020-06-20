# Gist of Flutter

## Portrait and Landscape Modes

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Making an app responsive to portrait and landscape modes

///To make an app responsive to portrait and landscape modes, create two separate files - one that contains widgets to
///be displayed if the device is in Portrait Mode, and another that contains widgets to be displayed if the device is in
///landscape mode.
class MyApp extends StatelessWidget {

  String appTitle;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Builder(
          builder: (BuildContext context){
            return Scaffold(
              appBar: AppBar(
                elevation: 10,
                backgroundColor: Colors.blue[900],
                ///MediaQuery.of(context).orientation is used to get the orientation of the device. For it to work (in
                ///the root widget), the Scaffold has to be wrapped in a Builder Widget to get context 'above' the
                ///MaterialApp Widget. As an alternative, the OrientationBuilder Widget can be used. In this case, the
                ///title of the app changes based on the device's orientation
                title: Text(MediaQuery.of(context).orientation == Orientation.portrait? 'Demo App - Portrait Mode': 'Demo App - Landscape Mode'),
                centerTitle: true,
              ),
              body: Center(child: ResponsiveWidget()),
            );
          }
        ),
      ),
    );
  }
}

///The Card Widget is a Layout widget and can be used in any manner depending on use case for the app.
class ResponsiveWidget extends StatefulWidget {
  @override
  _ResponsiveWidgetState createState() => _ResponsiveWidgetState();
}

class _ResponsiveWidgetState extends State<ResponsiveWidget> {

  @override
  Widget build(BuildContext context) {
    ///If the device is in portrait mode, the PortraitMode() widget is called. This is a custom widget that was created
    ///specifically for the portrait mode of a device
    if (MediaQuery.of(context).orientation == Orientation.portrait)
      return PortraitMode();
    ///If the device is in landscape mode, the LandscapeMode() widget is called. This is a custom widget that was created
    ///specifically for the landscape mode of a device
    if (MediaQuery.of(context).orientation == Orientation.landscape)
      return LandscapeMode();
  }
}

///Widget to be displayed if the device is in Portrait mode
class PortraitMode extends StatefulWidget {
  @override
  _PortraitModeState createState() => _PortraitModeState();
}

class _PortraitModeState extends State<PortraitMode> {

  CarModels carModels = CarModels();

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 500,
      child: Card(
        margin: EdgeInsets.all(50),
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.all(Radius.circular(10)),
        ),
        elevation: 10,
        child: Padding(
          padding: EdgeInsets.all(10),

          ///The Stack widget arranges widgets in a list of widgets on top of each other
          child: Stack(
            ///The alignment property is used to orient the alignment of the widgets that are on top of the list of
            ///widgets in the Stack
            alignment: AlignmentDirectional.topStart,
            children: <Widget>[
              Column(
                children: <Widget>[
                  Expanded(
                    flex: 0,
                    child: Container(
                      height: 325,
                      child: Column(children: <Widget>[
                        Padding(
                          padding: const EdgeInsets.all(10.0),
                          child: Container(
                              height: 200,
                              color: Colors.black,
                              child: Image.asset(carModels.getCarImage())),
                        ),
                        Padding(
                          padding: const EdgeInsets.all(10.0),

                          ///The car manufacturer is accessed from the CarModels model using its getCarManufacturer()
                          ///method
                          child: Text('Manufacturer: ${carModels.getCarManufacturer()}'),
                        ),
                        Padding(
                          padding: const EdgeInsets.all(10.0),

                          ///The car model is accessed from the CarModels model using its getCarModel() method
                          child: Text('Model: ${carModels.getCarModel()}'),
                        )
                      ]),
                    ),
                  ),
                  Expanded(
                    flex: 1,
                    child: Row(
                      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                      children: <Widget>[
                        MaterialButton(
                          onPressed: () {
                            setState(() {
                              ///This method is used to go to the previous item in the CarModels list
                              carModels.previousCar();
                            });
                          },
                          shape: RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(10))),
                          color: Colors.blue[900],
                          elevation: 10,
                          child: Text(
                            'Previous',
                            style: TextStyle(color: Colors.white),
                          ),
                        ),
                        MaterialButton(
                          onPressed: () {
                            setState(() {
                              ///This method is used to go to the next item in the CarModels list
                              carModels.nextCar();
                            });
                          },
                          shape: RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(10))),
                          color: Colors.blue[900],
                          elevation: 10,
                          child: Text(
                            'Next',
                            style: TextStyle(color: Colors.white),
                          ),
                        )
                      ],
                    ),
                  )
                ],
              ),
              Container(
                decoration: BoxDecoration(shape: BoxShape.circle, border: Border.all(color: Colors.white, width: 2)),
                child: CircleAvatar(
                  backgroundColor: Colors.blue[900],
                  child: Text(
                    (carModels.carNumber + 1).toString(),
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}

///Widget to be displayed if the device is in landscape mode
class LandscapeMode extends StatefulWidget {
  @override
  _LandscapeModeState createState() => _LandscapeModeState();
}

class _LandscapeModeState extends State<LandscapeMode> {

  CarModels carModels = CarModels();

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Card(
        margin: EdgeInsets.all(50),
        shape: RoundedRectangleBorder(
          borderRadius: BorderRadius.all(Radius.circular(10)),
        ),
        elevation: 10,
        child: Padding(
          padding: EdgeInsets.all(10),

          ///The Stack widget arranges widgets in a list of widgets on top of each other
          child: Stack(
            ///The alignment property is used to orient the alignment of the widgets that are on top of the list of
            ///widgets in the Stack
            alignment: AlignmentDirectional.topStart,
            children: <Widget>[
              Row(
                children: <Widget>[
                  Expanded(
                    flex: 1,
                    child: Container(
                      width: 325,
                      child: Padding(
                        padding: const EdgeInsets.all(10.0),
                        child: Container(
                            height: 200,
                            color: Colors.black,

                            ///The car image is accessed from the CarModels model using its getCarImage() method
                            child: Image.asset(carModels.getCarImage())),
                      ),
                    ),
                  ),
                  Expanded(
                    flex: 1,
                    child: Column(
                      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                      children: <Widget>[
                        Padding(
                          padding: const EdgeInsets.all(10.0),

                          ///The car manufacturer is accessed from the CarModels model using its getCarManufacturer()
                          ///method
                          child: Text('Manufacturer: ${carModels.getCarManufacturer()}'),
                        ),
                        Padding(
                          padding: const EdgeInsets.all(10.0),

                          ///The car model is accessed from the CarModels model using its getCarModel() method
                          child: Text('Model: ${carModels.getCarModel()}'),
                        ),
                        Row(
                          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                          children: <Widget>[
                            MaterialButton(
                              onPressed: () {
                                setState(() {
                                  ///This method is used to go to the previous item in the CarModels list
                                  carModels.previousCar();
                                });
                              },
                              shape: RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(10))),
                              color: Colors.blue[900],
                              elevation: 10,
                              child: Text(
                                'Previous',
                                style: TextStyle(color: Colors.white),
                              ),
                            ),
                            MaterialButton(
                              onPressed: () {
                                setState(() {
                                  ///This method is used to go to the next item in the CarModels list
                                  carModels.nextCar();
                                });
                              },
                              shape: RoundedRectangleBorder(borderRadius: BorderRadius.all(Radius.circular(10))),
                              color: Colors.blue[900],
                              elevation: 10,
                              child: Text(
                                'Next',
                                style: TextStyle(color: Colors.white),
                              ),
                            )
                          ],
                        ),
                      ],
                    ),
                  )
                ],
              ),
              Container(
                decoration: BoxDecoration(shape: BoxShape.circle, border: Border.all(color: Colors.white, width: 2)),
                child: CircleAvatar(
                  backgroundColor: Colors.blue[900],
                  child: Text(
                    (carModels.carNumber + 1).toString(),
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}

///Here, a model (CarModels) is created from another model (CarInfo). The CarModels model is then accessed from the
///CardWidget by creating an object (of the CarModels model). The CarModels model has methods to create a walkthrough
///of the images in the list CarModels
class CarInfo {
  String imagePath;
  String manufacturer;
  String model;

  CarInfo({@required this.imagePath, @required this.manufacturer, @required this.model});
}

class CarModels {
  int carNumber = 0;

  List<CarInfo> listOfCars = [
    CarInfo(imagePath: "assets/cars/Cars01.jpg", manufacturer: "Equus", model: "Bass"),
    CarInfo(imagePath: "assets/cars/Cars02.jpg", manufacturer: "Audi", model: "B2 Quattro"),
    CarInfo(imagePath: "assets/cars/Cars03.jpg", manufacturer: "Nissan", model: "Skyline R34"),
    CarInfo(imagePath: "assets/cars/Cars04.jpg", manufacturer: "Shelby", model: "1967 GT500"),
    CarInfo(imagePath: "assets/cars/Cars05.jpg", manufacturer: "BMW", model: "Concept"),
    CarInfo(imagePath: "assets/cars/Cars06.jpg", manufacturer: "Chevrolet", model: "Camaro"),
    CarInfo(imagePath: "assets/cars/Cars07.jpg", manufacturer: "Honda", model: "NSX"),
    CarInfo(imagePath: "assets/cars/Cars08.jpg", manufacturer: "Mitsubishi", model: "Lancer EVO 5"),
    CarInfo(imagePath: "assets/cars/Cars09.jpg", manufacturer: "Toyota", model: "Corolla AE86"),
    CarInfo(imagePath: "assets/cars/Cars10.jpg", manufacturer: "Lamborghini", model: "Ankonian (concept)"),
  ];

  ///These methods are created to get each list item's parameter
  String getCarImage() => listOfCars[carNumber].imagePath;

  String getCarManufacturer() => listOfCars[carNumber].manufacturer;

  String getCarModel() => listOfCars[carNumber].model;

  ///length - 1 is used to prevent the index from going out of range when the length of the list is reached
  void nextCar() {
    if (carNumber < listOfCars.length - 1)
      carNumber++;
    else
      carNumber = 0;
  }

  void previousCar() {
    if (carNumber > 0)
      carNumber--;
    else
      carNumber = listOfCars.length - 1;
  }
}
```

Refer this link [https://stackoverflow.com/questions/50815014/how-to-detect-orientation-change-in-layout-in-flutter](https://stackoverflow.com/questions/50815014/how-to-detect-orientation-change-in-layout-in-flutter)

#### Screenshots

[PortraitLandscapeModes01](Screenshots/PortraitLandscapeModes01.png)  
[PortraitLandscapeModes02](Screenshots/PortraitLandscapeModes02.png)