[TOC]

[dart style](https://dart.dev/guides/language/effective-dart/style)

#### 标识命名

##### 文件名\lib库名\包名

* lowercase_with_underscores

```dart
library lib_test.test_one;
import 'file_list.dart';
import 'dart.json' as json;
```

##### 类名

* UpperCamelCase

```dart
class NameExample
```

##### 变量名\常量名

* lowerCamelCase

```dart
var name;
var urlStr;
const pi = 3.14
```

#### 导包顺序

* "dart:"导入放在其它导入语句之前
* "package:" 导入语句放到相对导入语句之前
* 将自己的导入与其它包的导入用空行分开
* "export" 放在所有导入语句之后

#### 格式化工具

* dartfmt

#### 注释

* 生成文档的注释 "///"，首行注释应简洁

* 尽量避免使用单行注释 "//"，块注释 "/**/"
* 注释放在注解之前
* 推荐使用 [变量名]描述入参

```dart
// new 关键字可链接至构造函数
Throws a [StateError] if call [new Point] 
```





