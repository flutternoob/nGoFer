# Gist of Flutter

## BottomSheet and ModalBottomSheet Widget

#### Code
```Java
import 'package:flutter/material.dart';

///BottomSheet and ModalBottomSheet
///The BottomSheet and ModalBottomSheet Widgets are a convenient way of showing small Widgets which require minor
///interactions with the app. The major difference between the BottomSheet and ModalBottomSheet Widgets are the way their
///methods are called and their behaviour for dismissing them.
///The BottomSheet Widget can be called using either the ScaffoldState Scaffold.of(context).showBottomSheet or by using
///a PersistentBottomSheetController variable to call the showBottomSheet method. The latter provides greater control
///over the behaviour of say, a FAB, which can be visible or not depending, on whether the BottomSheet is open. Also, the
///BottomSheet Widget has to be dismissed by swiping it down. The showBottomSheet Widget uses an anonymous function that
///takes a BuildContext as an argument and returns the Widget that is used as a BottomSheet.
///The ModalBottomSheet behaves more like an AlertDialog for dismissing it, i.e, it can be dismissed by tapping anywhere
///in the Viewport. Additionally, it can also be dismissed by swiping it down. The ModalBottomSheet is called using the
///showModalBottomSheet method. The ModalBottomSheet Widget's main properties are the context and the builder properties.
///The builder property uses an anonymous function (which takes a BuildContext as an argument) and returns the Widget to
///be used as a ModalBottomSheet

void main() => runApp(MyApp());

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  bool isButtonTapped = false;

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
          leading: Builder(
              builder: (context) => IconButton(
                    icon: Icon(Icons.menu),
                    onPressed: () {
                      ///Setting the state of the menu IconButton
                      setState(() {
                        isButtonTapped = !isButtonTapped;
                      });
                      ///If the menu IconButton is true, then a BottomSheet is shown, else a ModalBottomSheet is shown.
                      isButtonTapped?
                      Scaffold.of(context).showBottomSheet((BuildContext context) => CustomBottomSheetWidget(),
                          backgroundColor: Colors.transparent):
                      showModalBottomSheet(
                          backgroundColor: Colors.transparent,
                          context: context,
                          builder: (BuildContext context) => CustomBottomSheetWidget());
                    },
                  )),
        ),
        body: Center(
          child: Text(
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam leo lorem, iaculis et egestas sed, '
            'ultricies vel ligula. Suspendisse potenti. Donec ac elit dui. Aliquam molestie mattis risus quis '
            'posuere. Nulla sodales, metus vel interdum fringilla, ligula dolor porttitor velit, quis gravida '
            'augue eros faucibus lectus. Donec consectetur dictum sem nec egestas. Mauris molestie tortor metus, '
            'non faucibus purus sodales ac. Vivamus laoreet elit sed sapien commodo fringilla sed id erat. Donec '
            'varius ex at lectus aliquam varius. Etiam nec auctor velit. Quisque rhoncus lorem at ex auctor tempus. '
            'Morbi ut enim in elit euismod gravida ut eget velit. Mauris at velit eros. Donec maximus elit at '
            'rutrum scelerisque. Vivamus auctor eget lacus ac sollicitudin.'
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam leo lorem, iaculis et egestas sed, '
            'ultricies vel ligula. Suspendisse potenti. Donec ac elit dui. Aliquam molestie mattis risus quis '
            'posuere. Nulla sodales, metus vel interdum fringilla, ligula dolor porttitor velit, quis gravida '
            'augue eros faucibus lectus. Donec consectetur dictum sem nec egestas. Mauris molestie tortor metus, '
            'non faucibus purus sodales ac. Vivamus laoreet elit sed sapien commodo fringilla sed id erat. Donec '
            'varius ex at lectus aliquam varius. Etiam nec auctor velit. Quisque rhoncus lorem at ex auctor tempus. '
            'Morbi ut enim in elit euismod gravida ut eget velit. Mauris at velit eros. Donec maximus elit at '
            'rutrum scelerisque. Vivamus auctor eget lacus ac sollicitudin.',
            textAlign: TextAlign.justify,
          ),
        ),
        floatingActionButton: Builder(
          builder: (BuildContext context){
            return MyFloatingActionButton();
          }
        ),
      ),
    );
  }
}

///Custom FAB Widget
class MyFloatingActionButton extends StatefulWidget {
  const MyFloatingActionButton({
    Key key,
  }) : super(key: key);

  @override
  _MyFloatingActionButtonState createState() => _MyFloatingActionButtonState();
}

class _MyFloatingActionButtonState extends State<MyFloatingActionButton> {
  ///The bool value used to set the visibility state of the FAB
  bool showFab = true;

  @override
  Widget build(BuildContext context) {
    ///If showFab is true, the bottomSheetController can be shown. If showFab is false, neither the FAB nor the
    ///bottomSheetController is shown.
    return showFab? FloatingActionButton(
      backgroundColor: Colors.black,
      child: Icon(Icons.add),
      onPressed: (){
        ///This is the bottomSheetController set to show the bottomSheet
        PersistentBottomSheetController bottomSheetController = showBottomSheet(
          backgroundColor: Colors.transparent,
                context: context,
          builder: (context) => CustomBottomSheetWidget()
        );
        ///This function is called to set the visibility state of the FAB. It is false if the bottomSheetController is open
        showFloatingActionButton(false);

        ///If the bottomSheetController is closed, then the FAB is shown
        bottomSheetController.closed.then((value) => showFloatingActionButton(true));
      },
    ): Container();
  }

  ///This function is defined to set the state the visibility state of the FAB
  void showFloatingActionButton(bool value){
    setState(() {
      showFab = value;
    });
  }
}

///Custom BottomSheet Widget
class CustomBottomSheetWidget extends StatelessWidget {
  double paddingValue = 50;

  @override
  Widget build(BuildContext context) {
    MediaQueryData mediaQueryData = MediaQuery.of(context);
    if (mediaQueryData.orientation == Orientation.portrait) paddingValue = 50;
    if (mediaQueryData.orientation == Orientation.landscape) paddingValue = 200;
    return Padding(
      padding: EdgeInsets.symmetric(horizontal: paddingValue),
      child: Container(
        height: 290,
        child: Opacity(
          opacity: 0.7,
          child: Container(
            decoration: BoxDecoration(
              color: Colors.black,
              shape: BoxShape.rectangle,
              border: Border.all(color: Colors.black, width: 2),
              borderRadius: BorderRadius.only(
                topRight: Radius.circular(30.9016994),
                topLeft: Radius.circular(30.9016994),
              ),
              boxShadow: [
                BoxShadow(
                    color: Colors.black45,
                    //offset: new Offset(0, -7.0),
                    blurRadius: 5.0,
                    spreadRadius: 5.0)
              ],
            ),
            child: Column(
              children: [
                for (int index = 0; index < 5; index++) ...[
                  ListTile(
                    title: Text(
                      'Index: $index',
                      style: TextStyle(color: Colors.white),
                    ),
                    trailing: Icon(Icons.list, color: Colors.white),
                    onTap: () {},
                  )
                ]
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

##### Refer this link [https://medium.com/flutter-community/flutter-beginners-guide-to-using-the-bottom-sheet-b8025573c433](https://medium.com/flutter-community/flutter-beginners-guide-to-using-the-bottom-sheet-b8025573c433) 
##### and this link [https://medium.com/flutterpub/flutter-5-bottom-sheet-2d56bf9f3bc](https://medium.com/flutterpub/flutter-5-bottom-sheet-2d56bf9f3bc)

#### Screenshots  
[BottomSheetModalBottomSheetWidget01](Screenshots/BottomSheetModalBottomSheetWidget01.png)  
[BottomSheetModalBottomSheetWidget02](Screenshots/BottomSheetModalBottomSheetWidget02.png)  
[BottomSheetModalBottomSheetWidget03](Screenshots/BottomSheetModalBottomSheetWidget03.png)