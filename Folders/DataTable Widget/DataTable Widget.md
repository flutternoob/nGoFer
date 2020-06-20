# Gist of Flutter

## DataTable Widget

#### Code
```Java
import 'package:flutter/material.dart';

///DataTable Widget
///The DataTable Widget is used when a small amount of data has to be displayed in a table. The data can be sorted by
///setting the sortAscending property (to true or false) and by setting the sortColumnIndex property to the index of the
///column that has to be sorted. The columnSpacing property is used to set the spacing between the columns in the
///DataTable Widget. The DataTable Widget takes a list of DataColumn Widgets in the columns property and a list of
///DataCell Widgets in the rows property.

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        body: DataTableWidget(),
      ),
    );
  }
}

class DataTableWidget extends StatefulWidget {
  @override
  _DataTableWidgetState createState() => _DataTableWidgetState();
}

class _DataTableWidgetState extends State<DataTableWidget> {
  bool sort = false;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(20.0),
      child: ListView(
        children: [
            DataTable(
              sortAscending: sort,
              sortColumnIndex: 1,
              columnSpacing: 50,
              columns: [
                DataColumn(label: Text('Serial'), numeric: true),
                DataColumn(
                    label: Text('Car Model'),
                    numeric: false,
                    onSort: (columnIndex, ascending) {
                      setState(() {
                        sort = !sort;
                      });
                      onSortColumn(columnIndex, ascending);
                    }
                ),
                DataColumn(label: Text('Cost'), numeric: true),
                DataColumn(label: Text(''))
              ],
              rows: vehicleCostData.map((vehicleInformation) =>
                DataRow(
                  cells: [
                    DataCell(Text('${vehicleInformation.serialNumber}')),
                    DataCell(Text(vehicleInformation.vehicleName)),
                    DataCell(Text('${vehicleInformation.vehicleCost.toInt()}')),
                    DataCell(
                        Icon(vehicleInformation.iconData),
                      onTap: () {
                          setState(() {
                            vehicleCostData.remove(vehicleInformation);
                          });
                      }
                    ),
                  ],
                ),
            ).toList(),
            )],
      ),
    );
  }

  onSortColumn(int columnIndex, bool ascending) {
    if (columnIndex == 1) {
      if (ascending) {
        vehicleCostData.sort(
              (a, b) => a.vehicleName.compareTo(
            b.vehicleCost.toString(),
          ),
        );
      } else {
        vehicleCostData.sort(
              (a, b) => b.vehicleName.compareTo(
            a.vehicleCost.toString(),
          ),
        );
      }
    }
  }
}

final List<VehicleCostData> vehicleCostData = [
  VehicleCostData(
    serialNumber: 1,
    vehicleName: 'Honda Civic',
    vehicleCost: 500
  ),
  VehicleCostData(
    serialNumber: 2,
    vehicleName: 'Toyota Corolla',
    vehicleCost: 700
  ),
  VehicleCostData(
    serialNumber: 3,
    vehicleName: 'Mitsubishi Lancer',
    vehicleCost: 600
  ),
  VehicleCostData(
    serialNumber: 4,
    vehicleName: 'Mazda RX7',
    vehicleCost: 400
  ),
  VehicleCostData(
    serialNumber: 5,
    vehicleName: 'Nissan Skyline R34',
    vehicleCost: 1000
  )
];

class VehicleCostData {
  int serialNumber;
  String vehicleName;
  double vehicleCost;
  IconData iconData;

  VehicleCostData({this.serialNumber, this.vehicleName, this.vehicleCost, this.iconData = Icons.delete_forever});
}
```

Refer this link [https://www.coderzheaven.com/2019/01/24/flutter-tutorials-datatable-android-ios/](https://www.coderzheaven.com/2019/01/24/flutter-tutorials-datatable-android-ios/)

#### Screenshots

[DataTableWidget01](Screenshots/DataTableWidget01.png)  
[DataTableWidget02](Screenshots/DataTableWidget02.png)  
[DataTableWidget03](Screenshots/DataTableWidget03.png)