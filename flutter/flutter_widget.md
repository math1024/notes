[TOC]

#### Button

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

```dart
FlatButton(
  onPressed: () {
    Navigator.push(context,
                   MaterialPageRoute(builder: (context) => ListBuilderDemo()));
  },
  child: Text('List Builder')
),

// more style
 FlatButton(
   color: Colors.blue,
   textColor: Colors.white,
   disabledColor: Colors.grey,
   disabledTextColor: Colors.black,
   padding: EdgeInsets.all(8.0),
   splashColor: Colors.blueAccent,
   // onPressed: null
   onPressed: () {
   },
   child: Text('List Tile',
               style: TextStyle(color: Colors.white, fontSize: 16))
 ),
```



- [DropdownButton](https://api.flutter.dev/flutter/material/DropdownButton-class.html), a button that shows options to select from.
- [FloatingActionButton](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html), the round button in material applications.
- [IconButton](https://api.flutter.dev/flutter/material/IconButton-class.html), to create buttons that just contain icons.
- [InkWell](https://api.flutter.dev/flutter/material/InkWell-class.html), which implements the ink splash part of a flat button.
- [RawMaterialButton](https://api.flutter.dev/flutter/material/RawMaterialButton-class.html), the widget this widget is based on.
- [material.io/design/components/buttons.html](https://material.io/design/components/buttons.html)

#### TextField

```dart
new TextField(
  controller: _textController,
  onSubmitted: _handleSubmitted,
  decoration:
  new InputDecoration.collapsed(hintText: "Send a message"),
  onChanged: (String text) {
  setState(() {
    _isComposing = text.length > 0;
  });                               
 },
),	
```

#### list

##### listView.builder

```dart
ListView.builder(
  padding: const EdgeInsets.all(16.0),
  itemBuilder: (context, i) {
  if (i.isOdd) return Divider();
  final index = i ~/ 2;
  if (index >= _suggestions.length) {
  _suggestions.addAll(generateWordPairs().take(5));
  }
  return _buildRow(_suggestions[index]);
});
```

listTile

```dart
Widget _buildRow(WordPair pair) {
  final bool alreadySaved = _saved.contains(pair);
  return ListTile(
    title: Text(
      pair.asPascalCase,
      style: TextStyle(fontSize:18.0),
    ),
    trailing: Icon(
      alreadySaved ? Icons.favorite : Icons.favorite_border,
      color: alreadySaved ? Colors.red : null,
    ),
    // onTap
    onTap: () {
      setState(() {
        if (alreadySaved) {
          _saved.remove(pair);
        } else {
          _saved.add(pair);
        }
      });
    },
  );
```

#### Flexible

```dart
 new Flexible(
   child: new ListView.builder(
     padding: new EdgeInsets.all(8.0),
     // start from bottom
     reverse: true,
     itemBuilder: (_, int index) => _messages[index],
     itemCount: _messages.length,
   ),
 ),
```



#### Padding & Margin

```dart
margin: const EdgeInsets.symmetric(horizontal: 8.0),
padding: new EdgeInsets.all(8.0), 
```

#### Column & Row



#### [BoxDecoration](https://docs.flutter.io/flutter/painting/BoxDecoration-class.html) 



#### Animation

##### AnimationController

```dart
class ChatScreenState extends State<ChatScreen> with TickerProviderStateMixin
animationController: new AnimationController(
        duration: new Duration(milliseconds: 700),
        vsync: this,
      ),
```



##### SizeTransition

```dart
new SizeTransition(
  sizeFactor: new CurvedAnimation(
    //new
    parent: animationController,
    curve: Curves.easeOut),
  axisAlignment: 0.0,
  child: Container()
```

