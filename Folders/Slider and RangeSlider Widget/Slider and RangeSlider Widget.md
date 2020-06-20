# Gist of Flutter

## Slider and RangeSlider Widget

#### Code
```Java
import 'package:flutter/material.dart';
import 'dart:math' show pi;

void main() => runApp(MyApp());

///Slider and RangeSlider Widget
///The Slider Widget is use to set a value based on user input. The value can be anything - such as price (in an
///e-commerce app), volume control (in a music app), progress control (of a song in a music app), or changing the shade
///of a given color used in an app (based on available color integer values). There are two main types of Sliders -
///Continuous Sliders and Discrete Sliders. A Slider Widget is typically wrapped in a SliderTheme Widget. Changing the
///properties of SliderThemeData changes the behaviour of its child Slider Widget.

///For correct functioning of the Slider Widget, the onChangeStart callback function property must be set (can be empty,
///but must be set), the onChangeEnd callback function property must be set (can be empty, but must be set). The
///onChanged callback function must also be set (usually to changing value of the Slider Widget).

///A RangeSlider widget is used to set values within a given range

class MyApp extends StatelessWidget {
  String appTitle;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      theme: ThemeData(),
      home: SafeArea(
        child: Builder(builder: (BuildContext context) {
          return Scaffold(
            appBar: AppBar(
              elevation: 10,
              backgroundColor: Colors.blue[900],
              title: Text('Demo App'),
              centerTitle: true,
            ),
            body: Center(child: SliderWidget()),
          );
        }),
      ),
    );
  }
}

class SliderWidget extends StatefulWidget {
  @override
  _SliderWidgetState createState() => _SliderWidgetState();
}

class _SliderWidgetState extends State<SliderWidget> {

  TextStyle textStyle = TextStyle(fontSize: 18, fontWeight: FontWeight.w500);

  ///Initial values of the Continuous and Discrete Sliders
  double sliderOne = 0;
  double sliderTwo = 0;
  double sliderThree = 0;

  ///RangeValues for a RangeSlider Widget
  RangeValues sliderFour = RangeValues(10, 20);

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: <Widget>[
        Container(
          height: 150,
          width: 250,
          decoration: BoxDecoration(
            shape: BoxShape.rectangle,
            borderRadius: BorderRadius.circular(20),
            border: Border.all(color: Colors.black)
          ),
          child: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Text('Continuous Slider', style: textStyle,),
                Text('Slider value: ${sliderOne.toInt()}', style: textStyle,),
                SliderTheme(
                    data: SliderThemeData(
                      activeTrackColor: Colors.blue,
                      thumbColor: Colors.blue[900],
                    ),
                    ///Continuous Slider Widget
                    child: Slider(
                      value: sliderOne,
                      min: 0,
                      max: 100,
                      onChangeStart: (startVal){},
                      onChangeEnd: (endVal){},
                      ///Updating the value of the Slider
                      onChanged: (changedVal) => setState(() => sliderOne = changedVal),
                    )
                )
              ],
            ),
          ),
        ),
        Container(
          width: 250,
          height: 150,
          decoration: BoxDecoration(
              shape: BoxShape.rectangle,
              borderRadius: BorderRadius.circular(20),
              border: Border.all(color: Colors.black)
          ),
          child: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Expanded(flex: 1,
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                    children: <Widget>[
                      Text('Vertical Slider', textAlign: TextAlign.center, style: textStyle,),
                      Text('Slider value:\n${sliderTwo.toInt()}', textAlign: TextAlign.center, style: textStyle,),
                    ],
                  ),
                ),
                Expanded(flex: 1,
                  child: Container(
                    height: 150,
                    child: SliderTheme(
                        data: SliderThemeData(
                            activeTrackColor: Colors.blue,
                            thumbColor: Colors.blue[900],
                          trackShape: RoundedRectSliderTrackShape(),
                          trackHeight: 10,
                          thumbShape: RoundSliderThumbShape(enabledThumbRadius: 7.5)
                        ),
                        ///Continuous Slider Widget arranged vertically using the Transform.rotate constructor
                        child: Transform.rotate(
                          ///Slider is rotated through an angle of -90 degrees
                          angle: -pi/2,
                          child: Slider(
                            value: sliderTwo,
                            min: 0,
                            max: 10,
                            onChangeStart: (startVal){},
                            onChangeEnd: (endVal){},
                            ///Updating the value of the Slider
                            onChanged: (changedVal) => setState(() => sliderTwo = changedVal),
                          ),
                        )
                    ),
                  ),
                )
              ],
            ),
          ),
        ),
        Container(
          height: 150,
          width: 250,
          decoration: BoxDecoration(
              shape: BoxShape.rectangle,
              borderRadius: BorderRadius.circular(20),
              border: Border.all(color: Colors.black)
          ),
          child: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Text('Discrete Slider', style: textStyle,),
                SliderTheme(
                    data: SliderThemeData(
                        activeTrackColor: Colors.blue,
                        thumbColor: Colors.blue[900],
                        trackShape: RoundedRectSliderTrackShape(),
                        trackHeight: 10,
                        thumbShape: RoundSliderThumbShape(enabledThumbRadius: 7.5),
                    ),
                    ///Discrete Slider Widget. To make a Slider discrete, set a number of divisions. Using this property
                    ///will also allow the use of the label property to indicate the value on the Slider thumb's paddle.
                    ///To make a Discrete Slider appear Continuous, set the number of divisions to be equal to the
                    ///maximum value of the Slider.
                    child: Slider(
                      value: sliderThree,
                      divisions: 10,
                      label: ('${sliderThree.toInt()}'),
                      min: 0,
                      max: 100,
                      onChangeStart: (startVal){},
                      onChangeEnd: (endVal){},
                      ///Updating the value of the Slider
                      onChanged: (changedVal) => setState(() => sliderThree = changedVal),
                    )
                )
              ],
            ),
          ),
        ),
        Container(
          height: 150,
          width: 250,
          decoration: BoxDecoration(
              shape: BoxShape.rectangle,
              borderRadius: BorderRadius.circular(20),
              border: Border.all(color: Colors.black)
          ),
          child: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Text('Range Slider', style: textStyle,),
                SliderTheme(
                    data: SliderThemeData(
                      activeTrackColor: Colors.blue,
                      thumbColor: Colors.blue[900],
                      trackShape: RoundedRectSliderTrackShape(),
                      trackHeight: 10,
                      thumbShape: RoundSliderThumbShape(enabledThumbRadius: 7.5),
                    ),
                    ///RangeSlider Widget used to select a range of values using the type RangeValues
                    child: RangeSlider(
                      ///Setting the range of values
                      values: sliderFour,
                      ///Assigning the number of divisions
                      divisions: 25,
                      ///The labels that appear in the thumb's paddle indicator
                      labels: RangeLabels('${sliderFour.start.toInt()}', '${sliderFour.end.toInt()}'),
                      min: 0,
                      max: 100,
                      onChangeStart: (startVal){},
                      onChangeEnd: (endVal){},
                      ///Updating the value of the Slider
                      onChanged: (changedVal) => setState(() => sliderFour = changedVal),
                    )
                )
              ],
            ),
          ),
        ),
      ],
    );
  }
}
```

Refer this link [https://medium.com/flutter-community/flutter-sliders-demystified-4b3ea65879c](https://medium.com/flutter-community/flutter-sliders-demystified-4b3ea65879c)  
Refer this link [https://medium.com/flutter/material-range-slider-in-flutter-a285c6e3447d](https://medium.com/flutter/material-range-slider-in-flutter-a285c6e3447d)  

#### Screenshots
[SliderWidget01](Screenshots/SliderWidget01.png)  
[SliderWidget02](Screenshots/SliderWidget02.png)  