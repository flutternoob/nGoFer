# Gist of Flutter

## TextField Widget

#### Code
```Java
import 'package:flutter/material.dart';

///TextField Widget
///The TextField Widget is used take an input from the user and perform some actions on it. The major properties are the
///controller, decoration and a function (such as the onChanged() function). The controller takes a TextEditingController
///whose value may or may not be set to a default value (using the TextEditingController.fromValue(TextEditingValue(text: ''))
///constructor). The controller and function are mandatory. If no decoration is provided, the TextField defaults to the
///platform specific decoration for the TextField.

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        ///Set the primaryColor value to apply the change to the TextField's border
          primaryColor: Colors.blue[900],
          cursorColor: Colors.black,
          textSelectionHandleColor: Colors.black
      ),
      home: Scaffold(
        appBar: AppBar(
          elevation: 10,
          backgroundColor: Colors.blue[900],
          title: Text('Demo App'),
          centerTitle: true,
        ),
        body: TextFieldWidget(),
      ),
    );
  }
}

class TextFieldWidget extends StatefulWidget {
  @override
  _TextFieldWidgetState createState() => _TextFieldWidgetState();
}

class _TextFieldWidgetState extends State<TextFieldWidget> {

  TextEditingController nameTextController = TextEditingController();
  TextEditingController emailTextController = TextEditingController();
  TextEditingController addressTextController = TextEditingController();
  TextEditingController phoneNumberTextController = TextEditingController();

  List<TextEditingController> textControllerList;

  @override
  void initState() {
    super.initState();
    textControllerList = [nameTextController, emailTextController, addressTextController, phoneNumberTextController];
    textFieldModel = [
      TextFieldModel(
          labelText: 'Name',
          hintText: 'Text',
          textEditingController: nameTextController,
          textStatus: nameTextController.text
      ),
      TextFieldModel(
          labelText: 'E-mail Address',
          hintText: 'Text',
          textEditingController: emailTextController,
          textStatus: emailTextController.text
      ),
      TextFieldModel(
          labelText: 'Address',
          hintText: 'Text',
          textEditingController: addressTextController,
          textStatus: addressTextController.text
      ),
      TextFieldModel(
          labelText: 'Phone Number',
          hintText: 'Number',
          textEditingController: phoneNumberTextController,
          textStatus: phoneNumberTextController.text
      ),
    ];
  }

  String textStatus = '';

  List<TextFieldModel> textFieldModel;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(10.0),
      ///Using the GestureDetector Widget with the following properties of Widget allows dismissing the keyboard, on
      ///tapping anywhere in the Viewport.
      child: GestureDetector(
        behavior: HitTestBehavior.opaque,
        onTap: () {
          FocusScope.of(context).requestFocus(FocusNode());
        },
        child: ListView(
          children: textFieldModel.map((textFieldModelParameter) =>
              Column(
                mainAxisAlignment: MainAxisAlignment.spaceAround,
                children: [
                  Padding(
                    padding: const EdgeInsets.all(10.0),
                    child: TextField(
                      maxLines: textFieldModelParameter.labelText == 'Address'? null: 1,
                      controller: textFieldModelParameter.textEditingController,
                      decoration: InputDecoration(
                          labelText: textFieldModelParameter.labelText,
                          labelStyle: TextStyle(color: Colors.black),
                          hintStyle: TextStyle(color: Colors.black),
                          hintText: textFieldModelParameter.hintText,
                          border: OutlineInputBorder(
                              borderRadius: BorderRadius.all(Radius.circular(10))
                          )
                      ),
                      onChanged: (String value) {
                        setState(() {
                          textFieldModelParameter.textStatus = value;
                        });
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(10.0),
                    child: Text('${textFieldModelParameter.labelText}: ${textFieldModelParameter.textStatus}'),
                  )
                ],
              )).toList(),
        ),
      ),
    );
  }
}

class TextFieldModel {
  String labelText;
  String hintText;
  TextEditingController textEditingController;
  String textStatus;

  TextFieldModel({this.textEditingController, this.labelText, this.hintText, this.textStatus});
}
```

#### Screenshots
[TextFieldWidget01](Screenshots/TextFieldWidget01.png)  
[TextFieldWidget02](Screenshots/TextFieldWidget02.png)