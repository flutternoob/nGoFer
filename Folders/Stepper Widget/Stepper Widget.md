# Gist of Flutter

## Stepper Widget

#### Code
```Java
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

///Stepper Widget
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
          body: Center(child: StepperWidget()),
        ),
      ),
    );
  }
}

class StepperWidget extends StatefulWidget {
  @override
  _StepperWidgetState createState() => _StepperWidgetState();
}

class _StepperWidgetState extends State<StepperWidget> {

  int currentStep;
  int previousStep;

  ///List variable that sets the current state of the isActive property of the Step widgets (in the Stepper widget) to false
  List<bool> isActiveState = [false, false, false, false, false, false, false, false, false, false];

  ///List variable that sets the current state of the state property of the Step widgets (in the Stepper widget)
  List<StepState> stepState = [
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed,
    StepState.indexed
  ];

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    currentStep = 0;
    previousStep = 0;
    isActiveState[0] = true;
    stepState[0] = StepState.editing;
  }

  ///Cycling through the steps in sequence functions
  ///Goes to next step in the Stepper widget
  void next() {
    setState(() {
      ///First set the previousStep to the currentStep
      previousStep = currentStep;

      ///Then increment the currentStep
      currentStep++;

      ///Call the indexState function to set the state of the isActive property of the previous and the next step
      indexState(currentStep, previousStep);
    });
  }

  ///Goes to previous step in the Stepper widget
  void cancelPrevious() {
    setState(() {
      if (currentStep > 0) {
        ///First set the previousStep to the currentStep
        previousStep = currentStep;

        ///Then decrement the currentStep
        currentStep--;

        ///Call the indexState function to set the state of the isActive property of the previous and the next step
        indexState(currentStep, previousStep);
      }
    });
  }

  ///End of cycling through the steps in sequence functions

  ///Goes to any step chosen by the user
  void goTo(int step) {
    setState(() {
      ///First set the previousStep to the currentStep
      previousStep = currentStep;

      ///Then set the currentStep to the step which the user has navigated to
      currentStep = step;

      ///Call the indexState function to set the state of the relevant properties of the step
      indexState(currentStep, previousStep);
    });
  }

  ///Setting the isActive property and state property of the step index
  void indexState(int currentStep, int previousStep) {
    isActiveState[previousStep] = false;
    isActiveState[currentStep] = true;
    if (isActiveState[previousStep] == false) stepState[previousStep] = StepState.indexed;
    if (isActiveState[currentStep] == true) stepState[currentStep] = StepState.editing;
  }

  @override
  Widget build(BuildContext context) {
    return Stepper(

        ///The type property sets the orientation of the Stepper widget. If there are many steps, use vertical orientation.
        ///Using a horizontal orientation causes a RenderFlex error when there are too many steps. If there are very few
        ///steps, then use horizontal orientation.
        type: StepperType.vertical,

        ///Th controlsBuilder property is used to define custom widgets that will be used to cycle through the steps. The VoidCallBack
        ///onStepCancel function calls the onStepCancel function of the Stepper widget to go to the previous step. The
        ///VoidCallBack onStepContinue function calls the onStepContinue function of the Stepper widget to go to the
        ///next step of the Stepper widget.
        controlsBuilder: (BuildContext context, {VoidCallback onStepCancel, VoidCallback onStepContinue}) {
          return Padding(
            padding: const EdgeInsets.all(10.0),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                MaterialButton(
                  elevation: 10,
                  color: Colors.blue[900],
                  onPressed: onStepContinue,
                  child: Text('Next', style: TextStyle(color: Colors.white)),
                ),
                MaterialButton(
                  elevation: 10,
                  color: Colors.blue[900],
                  onPressed: onStepCancel,
                  child: Text('Previous', style: TextStyle(color: Colors.white)),
                )
              ],
            ),
          );
        },

        ///This property is an int and works like an index to cycle through the steps
        currentStep: currentStep,

        ///This function lets the user navigate to any step in the Stepper widget without cycling through all the steps
        onStepTapped: (step) => goTo(step),

        ///This function lets the user cycle through all the steps from beginning to end
        onStepContinue: next,

        ///This function lets the user cancel the current step and go to the previous step
        onStepCancel: cancelPrevious,
        steps: <Step>[
          Step(
              title: Text('Step 1'),
              content: Text('This is Step 1', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[0],
              state: stepState[0]),
          Step(
              title: Text('Step 2'),
              content: Text('This is Step 2', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[1],
              state: stepState[1]),
          Step(
              title: Text('Step 3'),
              content: Text('This is Step 3', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[2],
              state: stepState[2]),
          Step(
              title: Text('Step 4'),
              content: Text('This is Step 4', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[3],
              state: stepState[3]),
          Step(
              title: Text('Step 5'),
              content: Text('This is Step 5', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[4],
              state: stepState[4]),
          Step(
              title: Text('Step 6'),
              content: Text('This is Step 6', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[5],
              state: stepState[5]),
          Step(
              title: Text('Step 7'),
              content: Text('This is Step 7', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[6],
              state: stepState[6]),
          Step(
              title: Text('Step 8'),
              content: Text('This is Step 8', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[7],
              state: stepState[7]),
          Step(
              title: Text('Step 9'),
              content: Text('This is Step 9', style: TextStyle(fontSize: 20)),
              isActive: isActiveState[8],
              state: stepState[8]),
          Step(
              title: Text('Step 10'),
              content: Text('This is Step 10'),
              isActive: isActiveState[9],
              state: stepState[9]),
        ]);
  }
}
```

Refer this link [https://medium.com/flutteropen/flutter-widgets-16-stepper-485ad8d1a248](https://medium.com/flutteropen/flutter-widgets-16-stepper-485ad8d1a248)  
Refer this link [https://www.youtube.com/watch?v=_NmzFsPgP2g](https://www.youtube.com/watch?v=_NmzFsPgP2g)  
Refer this link [https://developer.school/flutter-how-to-use-the-stepper-widget/](https://developer.school/flutter-how-to-use-the-stepper-widget/)  

#### Screenshots
[StepperWidget01](Screenshots/StepperWidget01.png)  
[StepperWidget02](Screenshots/StepperWidget02.png)  