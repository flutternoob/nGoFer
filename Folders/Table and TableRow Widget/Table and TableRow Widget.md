# Gist of Flutter

## Table and TableRow Widget

#### Code
```Java
import 'package:flutter/material.dart';

///Table and TableRow Widget
///As the name suggests, the Table Widget is used to present information in a table. Rather than building the table
///column-wise, the Table Widget is built row-wise. The two main properties of the Table Widget are the columnWidths
///property and the children property. The columnWidths property is of the Map type and its value (in the Key:Value pair)
///can either take FractionColumnWidth constructor or the FixedColumnWidth constructor (which are of the type double).
///The Key is the index (int) of the column.
///The TableRow Widget takes a list of Widgets (any Widget) as its children. Decoration can be applied to the TableRow
///using the decoration property. The TableCell Widget can be a child of a TableRow, Stateless or Stateful Widget only.
///No other Widget be used as a parent for the TableCell Widget. The usage of a TableCell Widget is optional in the
///TableRow Widget.

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
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
          body: Center(
              child: VehicleInformationWidget()
          ),
      ),
    );
  }
}

class VehicleInformationWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(20.0),
      child: Container(
        ///The ListView widget is used to make the Table Widget scrollable
        child: ListView(
          children: [
            ///Table Widget used to present vehicle information
            Table(
              border: TableBorder.all(color: Colors.black, width: 2),
              ///columnsWidths property used to define the widths of the columns in the Table Widget
              columnWidths: {0: FractionColumnWidth(.60), 1: FractionColumnWidth(.40)},
              children: [
                ///This TableRow Widget is used to present the titles of given column
                TableRow(children: [
                  Container(
                    color: Colors.blue[900],
                    child: Padding(
                      padding: const EdgeInsets.all(10.0),
                      child: Text(
                        'Model',
                        textAlign: TextAlign.center,
                        style: TextStyle(color: Colors.white, fontSize: 16),
                      ),
                    ),
                  ),
                  Container(
                    color: Colors.blue[900],
                    child: Padding(
                      padding: const EdgeInsets.all(10.0),
                      child: Text(
                        'Manufacturer',
                        textAlign: TextAlign.center,
                        style: TextStyle(color: Colors.white, fontSize: 16),
                      ),
                    ),
                  ),
                ]),
                ///TableRow Widgets of vehicle information presented using a 'for...in' loop based on list of vehicle data
                for (VehicleData vehicleInformation in vehicleData) ...[
                  TableRow(children: [
                    ///The below widget is for Vehicle Model
                    Padding(
                      padding: const EdgeInsets.all(10.0),
                      child: Text(
                        vehicleInformation.vehicleModel,
                        style: TextStyle(fontSize: 16),
                      ),
                    ),
                    ///The below widget is for that vehicle model's manufacturer
                    Padding(
                      padding: const EdgeInsets.all(10.0),
                      child: Text(
                        vehicleInformation.manufacturerName,
                        textAlign: TextAlign.center,
                        style: TextStyle(fontSize: 16),
                      ),
                    )
                  ])
                ]
              ],
            ),
          ],
        ),
      ),
    );
  }
}

///Sample list of Vehicle Data
final List<VehicleData> vehicleData = [
  VehicleData(vehicleModel: '1967 Shelby GT500', manufacturerName: 'Ford'),
  VehicleData(vehicleModel: '1986 Audi B2 Quattro', manufacturerName: 'Audi'),
  VehicleData(vehicleModel: '1998 Mitsubishi Lancer EVO 5', manufacturerName: 'Mitsubishi'),
  VehicleData(vehicleModel: '2001 Nissan Skyline R34', manufacturerName: 'Nissan'),
  VehicleData(vehicleModel: '1990 Nissan 240SX', manufacturerName: 'Nissan'),
  VehicleData(vehicleModel: '2014 Ford Mustang', manufacturerName: 'Ford'),
  VehicleData(vehicleModel: '1986 BMW M3 E30', manufacturerName: 'BMW'),
  VehicleData(vehicleModel: '2016 Chevrolet Camaro SS Coupe', manufacturerName: 'Chevrolet'),
  VehicleData(vehicleModel: '1969 Chevrolet Camaro Z28', manufacturerName: 'Chevrolet'),
  VehicleData(vehicleModel: '1992 Ford Escort RS Cosworth', manufacturerName: 'Ford')
];

///VehicleData model class
class VehicleData {
  String manufacturerName;
  String vehicleModel;

  VehicleData({this.vehicleModel, this.manufacturerName});
}
```

#### Screenshots
[TableTableRowWidget01](Screenshots/TableTableRowWidget01.png)  
[TableTableRowWidget02](Screenshots/TableTableRowWidget02.png)