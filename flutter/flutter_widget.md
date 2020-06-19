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
  
  
// shape 种类
BeveledRectangleBorder 带斜角的长方形边框
CircleBorder 圆形边框
RoundedRectangleBorder 圆角矩形
StadiumBorder 两端是半圆的边框
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

[DropdownButton](https://api.flutter.dev/flutter/material/DropdownButton-class.html), a button that shows options to select from.

```dart
@override
Widget build(BuildContext context) {
    String dropdownValue = '版本';
....
  
DropdownButton<String>(
  value: dropdownValue,
  icon: Icon(Icons.arrow_drop_down),
  iconSize: 24,
  elevation: 16,
  style: TextStyle(color: Colors.blue),
  onChanged: (String newValue) {
    setState(() {
      dropdownValue = newValue;
    });
  },
  items: <String>['版本', 'One', 'Two', 'Free', 'Four']
  .map<DropdownMenuItem<String>>((String value) {
    return DropdownMenuItem<String>(
      value: value,
      child: Text(value),
    );
  }).toList(),
),
```

- [FloatingActionButton](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html), the round button in material applications.
- [IconButton](https://api.flutter.dev/flutter/material/IconButton-class.html), to create buttons that just contain icons.
- [InkWell](https://api.flutter.dev/flutter/material/InkWell-class.html), which implements the ink splash part of a flat button.
- [RawMaterialButton](https://api.flutter.dev/flutter/material/RawMaterialButton-class.html), the widget this widget is based on.
- [material.io/design/components/buttons.html](https://material.io/design/components/buttons.html)

#### [TextField](https://api.flutter.dev/flutter/material/TextField-class.html)

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

// password
TextField(
  obscureText: true, // 不显示
  decoration: InputDecoration(
    border: OutlineInputBorder(),
    labelText: 'Password',
  ),
)
```

####TextFormField 

* TextField 封装类，方便做表单验证

```dart
 TextFormField(
   decoration: InputDecoration(
     fillColor: Colors.white,
     hintText: '请输入事件名',
     filled: true,
     prefixIcon: Icon(
       Icons.search,
       size: 28.0,
     ),
     suffixIcon: IconButton(
       icon: Icon(Icons.clear),
       onPressed: () {
         debugPrint('222');
       })),
 ),
)
```

#### ListView & GridView

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

##### list.generate

```dart
List.generate(_listItemCount(products.length), (int index) {
      double width = .59 * MediaQuery.of(context).size.width;
      Widget column;
      if (index % 2 == 0) {
        /// Even cases
        int bottom = _evenCasesIndex(index);
        column = TwoProductCardColumn(
            bottom: products[bottom],
            top: products.length - 1 >= bottom + 1
                ? products[bottom + 1]
                : null);
        width += 32.0;
      } else {
        /// Odd cases
        column = OneProductCardColumn(
          product: products[_oddCasesIndex(index)],
        );
      }
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

##### GridView.count

```dart
body: GridView.count(
  crossAxisCount: 2,
  padding: EdgeInsets.all(16.0),
  childAspectRatio: 8.0 / 9.0,
  children: <Widget>[Card()],
),
```



##### Align

```dart
const Align({
    Key key,
    this.alignment: Alignment.center,
    this.widthFactor,
    this.heightFactor,
    Widget child
  })
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

#### Card

```dart

```



#### Padding & Margin

```dart
margin: const EdgeInsets.symmetric(horizontal: 8.0),
padding: new EdgeInsets.all(8.0), 
```

#### Column & Row

#### AppBar

```dart
 appBar: AppBar(
   // LTR-left
   leading: IconButton(
     icon: Icon(
       Icons.menu,
       semanticLabel: 'menu',
     ),
     onPressed: () {
       print('Menu button');
     },
   ),
   title: Text('Home Page'),
   // LTR-right
   actions: <Widget>[
     IconButton(
       icon: Icon(
         Icons.search,
         semanticLabel: 'search',
       ),
       onPressed: () {
         print('Search button');
       },
     ),
     IconButton(
       icon: Icon(
         Icons.tune,
         semanticLabel: 'filter',
       ),
       onPressed: () {
         print('Filter button');
       },
     ),
   ],
 ),
```

#### LayoutBuilder

```dart

```



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

#### RadioListTile

```dart
 Row(
   children: [
     Flexible(
       child: RadioListTile(
         value: 1,
         groupValue: this.deviceType,
         title: Text('IOS'),
         onChanged: (value) {
           setState(() {
             this.deviceType = value;
           });
         },
       )),
     Flexible(
       child: RadioListTile(
         value: 2,
         groupValue: this.deviceType,
         title: Text('ANDROID'),
         onChanged: (value) {
           setState(() {
             this.deviceType = value;
           });
         },
       ),
     )
   ],
 ),
```

#### Table DataTable PaginatedDataTable



* PaginatedDataTable 带分页

```dart

```

#### SliverList

```dart

```

##### WillPopScope

```dart
DateTime _lastPressedAt; //上次点击时间 
Widget build(BuildContext context) {
  return new WillPopScope(
    onWillPop: () async {
      if (_lastPressedAt == null ||
          DateTime.now().difference(_lastPressedAt) > Duration(seconds: 1)) {
        //两次点击间隔超过1秒则重新计时
        _lastPressedAt = DateTime.now();
        return false;
      }
      return true;
    },
    child: Container(
      alignment: Alignment.center,
      child: Text("1秒内连续按两次返回键退出"),
    )
  );
}
```

#### FutureBuilder

```dart

```

