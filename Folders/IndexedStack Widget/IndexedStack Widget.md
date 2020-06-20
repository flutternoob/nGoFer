# Gist of Flutter

## IndexedStack Widget

#### Code
```Java
import 'package:flutter/material.dart';

///IndexedStack Widget
///With this widget, the children widget can be accessed based on their index of occurrence in the Stack's list of
///children widgets. Except for the widget that has been accessed using its index, all other widgets are invisible. Only
///the Widget that has been accessed with its index of occurrence in the stack, is visible. The main property of the
///IndexedStack Widget is the index property.

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: WillPopScope(
        onWillPop: () => Future.value(false),
        child: Scaffold(
          appBar: AppBar(
            elevation: 10,
            backgroundColor: Colors.blue[900],
            title: Text('Demo App'),
            centerTitle: true,
          ),
          body: Center(child: IndexedStackWidget()),
        ),
      ),
    );
  }
}

class IndexedStackWidget extends StatefulWidget {
  @override
  _IndexedStackWidgetState createState() => _IndexedStackWidgetState();
}

class _IndexedStackWidgetState extends State<IndexedStackWidget> {
  int index = 0;
  List<dynamic> color = [Colors.black, Colors.blue[900], Colors.grey[700], Colors.red[900]];
  double width = 125;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Container(
          width: 200,
          height: 200,
          child: IndexedStack(
            alignment: AlignmentDirectional.center,
            index: index,
            children: [
              for (int i = 0; i < color.length; i++)...[
                Container(
                    width: width,
                    height: width,
                    color: color[i],
                    child: Center(
                      child: Text(
                        'Size:\n${width.toInt()} x ${width.toInt()}', textAlign: TextAlign.center,
                        style: TextStyle(color: Colors.white),
                      ),
                    ),
                ),
              ]
            ],
          ),
        ),
        Row(
          mainAxisAlignment: MainAxisAlignment.spaceAround,
          children: [
            ///Goes to previous item in the IndexedStack Widget
            IconButton(
              icon: Icon(Icons.navigate_before),
              onPressed: () {
                setState(() {
                  if (index > 0) {
                    index--;
                    width -= 25;
                  }
                });
              },
            ),
            ///Goes to next item in the IndexedStack Widget
            IconButton(
              icon: Icon(Icons.navigate_next),
              onPressed: () {
                setState(() {
                  if (index < color.length - 1) {
                    index++;
                    width += 25;
                  }
                });
              },
            )
          ],
        )
      ],
    );
  }
}
```

Refer this link [https://fluttercentral.com/Articles/Post/1159/IndexedStack_in_Flutter_with_Example](https://fluttercentral.com/Articles/Post/1159/IndexedStack_in_Flutter_with_Example)

#### Screenshots
[IndexedStack01](Screenshots/IndexedStack01.png)  
[IndexedStack02](Screenshots/IndexedStack02.png)  
[IndexedStack03](Screenshots/IndexedStack03.png)  
[IndexedStack04](Screenshots/IndexedStack04.png)