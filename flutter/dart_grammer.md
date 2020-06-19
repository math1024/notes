[TOC]

##### [dart grammer](https://dart.dev/samples)

###### print

```dart
print('print log')
```

###### with

###### 类型转换

```dart
// int->String String ->int
int.parse("100");
123.toString();
// String to int
var one = int.parse('1');
print(one);

// String to double
var onePointOne = double.parse('1.1');
print(onePointOne);

// int to String
String twenty = 20.toString();
print(twenty);

// double to String
String pi= 3.14316.toStringAsFixed(2);
print(pi);
```

###### show

```dart
// 只导入库的部分代码
import 'dart:ui' show lerpDouble;
```

###### async\await

* [offical doc](https://dart.cn/guides/language/language-tour)

###### list

```dart
// 不定长list
var testList = List();
print(testList.length);//输出0
// 定长
var testList2 = List(2);
print(testList.length); // 2
// 固定类型
var testList3 = List<String>();
// 直接赋值
var testList4 = [124,12,212,55];
print(testList4.first); // 124
print(testList4.last); // 55
print(testList4[2]); // 212
print(testList4.isEmpty);
print(testList.isNotEmpty);
// 添加
// 删除
testList4.removeLast();
testList4.removeAt(1)
testList4.removeRange(0,1);

```

##### factory

* 实现构造函数但是不想每次都创建该类的一个实例的时候使用
* 不能通过this

```dart
 factory ClassName.method() {
    return new ClassName(
      param1, param2...
    );
  }
```

##### runtimeType  

* 查看对象类型

```dart
List list = SystemUtility.getVersionList();
print(list);
print(list.runtimeType.toString());
```

##### map

```dart
xList = ['2020-3-4', '2020-3-5', '2020-3-6'];
yList = [ "500", "1000", "1500", "2000", "2500"];
print('xList: $xList  yList:$yList times $times');
times = {"7.0.0": [100, 400, 300],'7.1.0':[100,200,300]};
List<String> versions = times.keys.toList();
List<List<int>> count = times.values.toList();
print('versions$versions count$count');
```

##### import\show\hide\part

* import 完全导入
* show 导入部分
* hide 隐藏部分
* part 拆分库，如果使用part来构建库，那么库必须要命名 
  * import 导入不共享，part导入是共享的