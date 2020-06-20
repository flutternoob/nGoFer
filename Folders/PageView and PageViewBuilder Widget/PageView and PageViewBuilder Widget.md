# Gist of Flutter

## PageView and PageViewBuilder Widget

#### Code
```Java
import 'package:flutter/material.dart';

///PageView and PageView.builder Widgets
///The PageView Widget takes a list of widgets and scrolls them page by page. Its main properties are the controller and
///scrollDirection properties. Both these properties are optional. A PageController object can be used to determine the
///PageView Widget's behaviour w.r.t the starting page and the fraction of the viewport that each page should occupy. The
///allowImplicitScrolling property should not be null, otherwise the PageView Widget will behave like a ListView Widget.
///By default, this property (allowImplicitScrolling) is false.
///Similar to the ListView.builder constructor, the PageView Widget also has a PageView.builder constructor. The main
///property is the itemBuilder property which uses an anonymous function (that takes a BuildContext and an int index) as
///arguments and returns a widget. Like the ListView.builder constructor, the PageView.builder constructor is best used
///for an infinite growable list.

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {

  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool widgetSwitcher = false;

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
            leading: Builder(
              builder: (context) => IconButton(
                icon: Icon(Icons.swap_vert),
                onPressed: () {
                  setState(() {
                    widgetSwitcher = !widgetSwitcher;
                  });
                },
              )
            ),
          ),
          body: widgetSwitcher? PageViewBuilderWidget(): PageViewWidget(),
        ),
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

class PageViewWidget extends StatelessWidget {

  ///Initializing the PageController
  final PageController _pageController = PageController(
    initialPage: 0,
    viewportFraction: 2
  );

  @override
  Widget build(BuildContext context) {
    print('Switched to PageViewWidget');
    return PageView(
      physics: BouncingScrollPhysics(),
      controller: _pageController,
      ///Set pageSnapping to true to allow each page to snap in the viewport while swiping through each page
      pageSnapping: true,
      children: [
        for(String imagePath in imagePaths)...[
          Padding(
            padding: const EdgeInsets.all(20.0),
            child: Container(
              child: Image.asset(imagePath),
            ),
          )
        ]
      ],
    );
  }
}

class PageViewBuilderWidget extends StatelessWidget {

  ///Initializing the PageController
  final PageController _pageController = PageController(
      initialPage: 0,
      viewportFraction: 1
  );

  @override
  Widget build(BuildContext context) {
    print('Switched to PageViewBuilderWidget');
    return PageView.builder(
      physics: BouncingScrollPhysics(),
      ///If the length of the list is unknown (such as an infinite list), the itemCount property is not needed
      itemCount: imagePaths.length,
        itemBuilder: (BuildContext context, index) {
          return Padding(
            padding: const EdgeInsets.all(20.0),
            child: Container(
              child: Image.asset(imagePaths[index]),
            ),
          );
        }
    );
  }
}
```

#### Screenshots

[PageViewPageViewBuilderWidget01](Screenshots/PageViewPageViewBuilderWidget01.png)  
[PageViewPageViewBuilderWidget02](Screenshots/PageViewPageViewBuilderWidget02.png)  
[PageViewPageViewBuilderWidget03](Screenshots/PageViewPageViewBuilderWidget03.png)  
[PageViewPageViewBuilderWidget04](Screenshots/PageViewPageViewBuilderWidget04.png)