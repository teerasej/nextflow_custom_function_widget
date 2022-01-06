# nextflow_custom_function_widget


## Getting Started

```dart
// main.dart 

// Using CustomCheckbox widget,
// you can specify valueId, icon widget, tile string
//and also a function that can get value from inside the widget
CustomCheckBox(
    valueId: 1,
    icon: Icon(Icons.plus_one),
    title: 'One',
    onCheck: (value) {
        // get value from inside the widget
        //please check line 11 for declaration and line 39 for invoking this function
        print(value);
    },
),
```

## custom_checkbox.dart

```dart
import 'package:flutter/material.dart';

class CustomCheckBox extends StatefulWidget {
  CustomCheckBox(
      {Key? key, this.icon, this.onCheck, this.title = '', this.valueId = 1})
      : super(key: key);

  // Setup property to be customed from developer when using this widget
  String title;
  Widget? icon; // icon for custom icon
  ValueSetter<int>?
      onCheck; // this is a type of function, so you can pass value to outside this widget

  // define a special value to be pass via ValueSetter, onCheck.
  int valueId;

  @override
  _CustomCheckBoxState createState() => _CustomCheckBoxState();
}

class _CustomCheckBoxState extends State<CustomCheckBox> {
  bool isCheck = false;

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Row(
        children: [
          widget.icon!,
          Text(widget.title),
          Checkbox(
            value: isCheck,
            onChanged: (value) {
              setState(() {
                this.isCheck = value!;

                // 'widget' refer to widget class who owns this state class
                // you can pass a value to ValueSetter property
                widget.onCheck!(widget.valueId);
              });
            },
          )
        ],
      ),
    );
  }
}

```
