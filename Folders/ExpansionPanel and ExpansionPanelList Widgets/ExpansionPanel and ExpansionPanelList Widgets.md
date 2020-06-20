# Gist of Flutter

## ExpansionPanel and ExpansionPanelList Widgets

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///ExpansionPanel and ExpansionPanelList Widgets
///These widgets are used when some part of the UI has to be expanded to show additional information. The ExpansionListTile
///is available for this purpose, however, it has been deprecated.

class MyApp extends StatelessWidget {
  String appTitle;

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
          body: Center(child: ExpansionPanelListWidget()),
        ),
      ),
    );
  }
}

class ExpansionPanelListWidget extends StatefulWidget {
  @override
  _ExpansionPanelListWidgetState createState() => _ExpansionPanelListWidgetState();
}

class _ExpansionPanelListWidgetState extends State<ExpansionPanelListWidget> {
  List<MyItems> myItems = [
    MyItems(
        header: 'Header 1',
        body:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam leo lorem, iaculis et egestas sed, ultricies vel ligula. Suspendisse potenti. Donec ac elit dui. Aliquam molestie mattis risus quis posuere. Nulla sodales, metus vel interdum fringilla, ligula dolor porttitor velit, quis gravida augue eros faucibus lectus. Donec consectetur dictum sem nec egestas. Mauris molestie tortor metus, non faucibus purus sodales ac. Vivamus laoreet elit sed sapien commodo fringilla sed id erat. Donec varius ex at lectus aliquam varius. Etiam nec auctor velit. Quisque rhoncus lorem at ex auctor tempus. Morbi ut enim in elit euismod gravida ut eget velit. Mauris at velit eros. Donec maximus elit at rutrum scelerisque. Vivamus auctor eget lacus ac sollicitudin.'),
    MyItems(
        header: 'Header 2',
        body:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam leo lorem, iaculis et egestas sed, ultricies vel ligula. Suspendisse potenti. Donec ac elit dui. Aliquam molestie mattis risus quis posuere. Nulla sodales, metus vel interdum fringilla, ligula dolor porttitor velit, quis gravida augue eros faucibus lectus. Donec consectetur dictum sem nec egestas. Mauris molestie tortor metus, non faucibus purus sodales ac. Vivamus laoreet elit sed sapien commodo fringilla sed id erat. Donec varius ex at lectus aliquam varius. Etiam nec auctor velit. Quisque rhoncus lorem at ex auctor tempus. Morbi ut enim in elit euismod gravida ut eget velit. Mauris at velit eros. Donec maximus elit at rutrum scelerisque. Vivamus auctor eget lacus ac sollicitudin.'),
  ];

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: myItems.map((MyItems item) {
        return Padding(
          padding: const EdgeInsets.all(20.0),
          child: Card(
            elevation: 10,
            child: ExpansionPanelList(
              ///The animationDuration property can be used to set the duration of the animation when the
              ///ExpansionPanelList expands and collapses.
              animationDuration: Duration(milliseconds: 500),
                ///expansionCallback is the callback that gets called whenever one of the expand/collapse buttons is pressed.
                ///Note - this works only when the buttons (arrows are pressed) not when the panel is pressed. To overcome
                ///this, set the canTapOnHeader property of the ExpansionPanel to true.
                expansionCallback: (int index, bool expansionPanelListState) {
                  setState(() {
                    item.isExpanded = !item.isExpanded;
                  });
                },
                children: [
                  ExpansionPanel(
                    ///Set the canTapOnHeader property to true to enable tapping on the header
                      canTapOnHeader: true,
                      headerBuilder: (BuildContext context, bool expansionPanelState) {
                        return Padding(
                          padding: const EdgeInsets.all(10.0),
                          child: Text(
                            item.header,
                            textAlign: TextAlign.left,
                            style: TextStyle(fontSize: 20, color: Colors.black),
                          ),
                        );
                      },
                      isExpanded: item.isExpanded,
                      body: Padding(
                        padding: const EdgeInsets.all(20.0),
                        child: Text(item.body, textAlign: TextAlign.justify),
                      ))
                ]),
          ),
        );
      }).toList(),
    );
  }
}

///Model used to generate a List of items
class MyItems {
  bool isExpanded;
  String header;
  String body;

  MyItems({this.isExpanded: false, this.header, this.body});
}
```

#### Screenshots

[ExpansionPanelExpansionPanelListWidget01](Screenshots/ExpansionPanelExpansionPanelListWidget01.png)  
[ExpansionPanelExpansionPanelListWidget02](Screenshots/ExpansionPanelExpansionPanelListWidget02.png)