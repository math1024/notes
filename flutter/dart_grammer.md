[TOC]

##### [dart grammer](https://dart.dev/samples)

###### print

```dart
print('print log')
```

###### extends\with\implements

```dart

```



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

##### String split

```dart
// 单字符分割
split('') 
// 正则表达 多分割符
RegExp re = RegExp(':|,|}');
String.split(re)
```

##### time&date

```dart
var now = new DateTime.now();
print(now);
print(now.add(new Duration(minutes: 10))); //加10分钟 
print(now.add(new Duration(minutes: -10))); //减10分钟

print(now.add(new Duration(hours: 2))); //加2小时
print(now.add(new Duration(hours: -2))); //减2小时 

print(now.add(new Duration(days: 2))); //加2天
print(now.add(new Duration(hours: -2))); //减2天  

/*
  如需要只获取日期需要'import package:intl/intl.dart';
  DateFormat('yyyy-MM-dd').format(DateTime.now()
  */
```

##### future

* 多个future按创建顺序先行，多个then嵌套，先执行外面再执行里面的

* then 成功消息 catchError   完成状态、未完成状态（网络请求过程中）

* 微任务队列、事件队列，前者高于后者
* then的函数体要分成三种情况：
  * 情况一：Future没有执行完成（有任务需要执行），那么then会直接被添加到Future的函数执行体后；
  * 情况二：如果Future执行完后就then，该then的函数体被放到如微任务队列，当前Future执行完后执行微任务队列；
  * 情况三：如果Future世链式调用，意味着then未执行完，下一个then不会执行；

```dart
// future_1加入到eventqueue中，紧随其后then_1被加入到eventqueue中
Future(() => print("future_1")).then((_) => print("then_1"));

// Future没有函数执行体，then_2被加入到microtaskqueue中
Future(() => null).then((_) => print("then_2"));

// future_3、then_3_a、then_3_b依次加入到eventqueue中
Future(() => print("future_3")).then((_) => print("then_3_a")).then((_) => print("then_3_b"));

void main() {
  print("main start");

  Future(() => print("task1"));

  final future = Future(() => null);

  Future(() => print("task2")).then((_) {
    print("task3");
    scheduleMicrotask(() => print('task4'));
  }).then((_) => print("task5"));

  future.then((_) => print("task6"));
  scheduleMicrotask(() => print('task7'));

  Future(() => print('task8'))
      .then((_) => Future(() => print('task9')))
      .then((_) => print('task10'));

  print("main end");
}

result:
main start
main end
task7
task1
task6
task2
task3
task5
task4
task8
task9
task10
```

##### async

```dart
void main() async {
  methodA();
  await methodB();
  await methodC('main');
  methodD();
}

methodA(){
  print('A');
}

methodB() async {
  print('B start');
  await methodC('B');
  print('B end');
}

methodC(String from) async {
  print('C start from $from');

  // await Future 你最初希望示例代码中仅在所有代码末尾执行 methodD()
  Future((){               
    print('C running Future from $from');
  }).then((_){
    print('C end of Future from $from');
  });

  print('C end from $from');
}

methodD(){
  print('D');
}
```

* 先同步再异步

##### await for\listen

```dart

```

