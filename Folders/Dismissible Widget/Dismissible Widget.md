# Gist of Flutter

## Dialog Widgets

#### Code
```Java
import 'package:flutter/material.dart';

///Dismissible Widget
///This widget is used to dismiss its child in a direction that is determined by the DismissDirection enum

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
        body: DismissibleWidget(),
      ),
    );
  }
}

class DismissibleWidget extends StatefulWidget {
  @override
  _DismissibleWidgetState createState() => _DismissibleWidgetState();
}

class _DismissibleWidgetState extends State<DismissibleWidget> {

  final List<String> _albumList = [
    "Capitol Punishment-The Megadeth Years (2000)",
    "Countdown to extinction",
    "Cryptic Writings",
    "Dystopia (Deluxe Edition) (2016)",
    "Endgame (2009)",
    "Hidden Treasures",
    "Killing Is My Business... And Business Is Good!",
    "Peace Sells... But Who's Buying",
    "Risk",
    "Rust In Peace",
    "So Far, So Good... So What!",
    "TH1RT3EN",
    "The Carving",
    "The World Needs A Hero",
    "Youthanasia",
    "The System Has Failed",
    "United Abominations"
  ];

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(20.0),
      child: ListView.builder(
        itemCount: _albumList.length,
        itemBuilder: (BuildContext context, int index) {
          return Dismissible(
            key: Key(_albumList[index]),
            ///The background widget is shown when sliding from left to right
            background: _primaryBackgroundWidget(),
            ///The secondary background widget is shown when sliding from right to left
            secondaryBackground: _secondaryBackgroundWidget(),
            ///The confirmDismiss property is used to carry out some action that requires user confirmation on a given
            ///dismiss direction. This property should be used when user confirmation is required for an action. If no
            ///confirmation is required, the onDismissed property should be used.
            confirmDismiss: (dismissDirection) async {
              bool result;
              ///Condition bock to determine the action carried out based on dismiss direction. Note: for demonstration,
              ///the same function is carried out for deleting and archiving. Any kind of action can be carried out for a
              ///given dismiss direction depending on the app's use case.
              if (dismissDirection == DismissDirection.endToStart)
                ///If the dismiss direction is from end to start, then delete the item
                result = await showDialogFunction(context, "Delete?", index);
              if (dismissDirection == DismissDirection.startToEnd)
                ///If the dismiss direction is from start to end, then archive the item.
                result = await showDialogFunction(context, "Archive?", index);
              return result;
            },
            child: InkWell(
              onTap: (){},
              child: ListTile(
                title: Text(_albumList[index]),
              ),
            ),
          );
        },
      ),
    );
  }

  ///This widget is called as the secondaryBackground Widget
  Widget _secondaryBackgroundWidget() {
    return Container(
      color: Colors.black87,
      child: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.end,
          children: [
            Text("Delete ", style: TextStyle(color: Colors.red)),
            Icon(
              Icons.delete_outline,
              color: Colors.red,
            ),
          ],
        ),
      ),
    );
  }

  ///This widget is called as the background Widget
  Widget _primaryBackgroundWidget() {
    return Container(
      color: Colors.black87,
      child: Padding(
        padding: const EdgeInsets.all(10.0),
        child: Row(
          mainAxisAlignment: MainAxisAlignment.start,
          children: [
            Icon(
              Icons.archive,
              color: Colors.green,
            ),
            Text(" Archive", style: TextStyle(color: Colors.green)),
          ],
        ),
      ),
    );
  }

  ///The showDialogFunction is called asynchronously, as an action has to be carried out on the dismissible item based on
  ///user input
  Future showDialogFunction(BuildContext context, String dialogTitle, int index) async {
    await showDialog(
        context: context,
        builder: (BuildContext context) => AlertDialog(
          title: Text(dialogTitle),
          content: Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              ///Item is removed from the list for deleting and archiving using this button
              FlatButton(
                onPressed: () {
                  setState(() {
                    _albumList.removeAt(index);
                  });
                  Navigator.pop(context);
                },
                child: Text("Ok"),
              ),
              ///Dismiss action is cancelled using this button.
              FlatButton(
                onPressed: () {
                  Navigator.pop(context);
                },
                child: Text("Cancel"),
              ),
            ],
          ),
        )
    );
  }
}
```

Refer this link [https://medium.com/@blog.padmal/flutter-dismissible-widget-swipe-both-ways-a696a1edb67b](https://medium.com/@blog.padmal/flutter-dismissible-widget-swipe-both-ways-a696a1edb67b)

#### Screenshots

[DismissibleWidget01](Screenshots/DismissibleWidget01.png)  
[DismissibleWidget02](Screenshots/DismissibleWidget02.png)  
[DismissibleWidget03](Screenshots/DismissibleWidget03.png)  
[DismissibleWidget04](Screenshots/DismissibleWidget04.png)  