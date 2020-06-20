# Gist of Flutter

## Card and Stack Widgets, Model From Model

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Card and Stack Widget, creating models from a model
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
          body: Center(child: CardWidget()),
        ),
      ),
    );
  }
}

///The Card Widget is a Layout widget and can be used in any manner depending on use case for the app.
class CardWidget extends StatefulWidget {
  @override
  _CardWidgetState createState() => _CardWidgetState();
}

class _CardWidgetState extends State<CardWidget> {
  CarModels carModels = CarModels();

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
  }

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

                              ///The car image is accessed from the CarModels model using its getCarImage() method
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
                    child: Container(
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

#### Screenshots

[CardStackWidgetsModelFromAModel01](Screenshots/CardStackWidgetsModelFromAModel01.png)  
[CardStackWidgetsModelFromAModel02](Screenshots/CardStackWidgetsModelFromAModel02.png)