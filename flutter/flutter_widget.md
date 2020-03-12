[TOC]

##### [RaisedButton](https://api.flutter.dev/flutter/material/RaisedButton-class.html)

```dart
/// 默认效果 default
RaisedButton(
  child: Text('basic RasiedButton',),
  color: Colors.grey,
  textColor: Colors.greenAccent,
  onPressed: () {
    print("object");
  },),

/// 禁止点击 no click 
RaisedButton(
  child: Text('Disable Button', style: TextStyle(fontSize: 12)),
  onPressed: null,
)
  
/// 更多样式 more style
RaisedButton(
  child: Container(
    decoration: const BoxDecoration(
      gradient: LinearGradient(
        colors: <Color>[
          Color(0xFF0D47A1),
          Color(0xFF1976D2),
          Color(0xFF42A5F5),
        ],
      ),
    ),
    child: Text('Rich Style', style: TextStyle(fontSize: 18)),
  ),
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(12),
  ),
  padding: const EdgeInsets.all(20.0),
  onPressed: (){})
```

- [FlatButton](https://api.flutter.dev/flutter/material/FlatButton-class.html), a material design button without a shadow.
- [DropdownButton](https://api.flutter.dev/flutter/material/DropdownButton-class.html), a button that shows options to select from.
- [FloatingActionButton](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html), the round button in material applications.
- [IconButton](https://api.flutter.dev/flutter/material/IconButton-class.html), to create buttons that just contain icons.
- [InkWell](https://api.flutter.dev/flutter/material/InkWell-class.html), which implements the ink splash part of a flat button.
- [RawMaterialButton](https://api.flutter.dev/flutter/material/RawMaterialButton-class.html), the widget this widget is based on.
- [material.io/design/components/buttons.html](https://material.io/design/components/buttons.html)

