[TOC]



#### UI

##### StatuflulWidget SatelessWidget

##### primarySwatch 主题颜色 

```dart
 return MaterialApp(
      theme: ThemeData(
        primarySwatch: Colors.green,
      ),
      ......
    );
```

##### Button

* RaisedButton ：凸起的按钮，其实就是Android中的Material

* Design风格的Button ，继承自MaterialButton
* FlatButton ：扁平化的按钮，继承自MaterialButton
* OutlineButton	：带边框的按钮，继承自MaterialButton

##### MaterialApp Scaffold

* MaterialApp设置App 整体theme， Scaffold 包含AppBar、bottomNavigationBar，隐藏的侧边栏drawer

##### Form

* Expanded 相当weight =1 在Row 或 Column中生效
* crossAxisAlignment: CrossAxisAlignment.center,
* mainAxisAlignment: MainAxisAlignment.spaceEvenly

##### Radio & RadioListTie 

* Radio 需要自行添加文本

*  RadioListTie 有文本

##### ListView

* ListTile 适合固定数量的文本
* ListView.builder 常用
* ListView.separated 带分隔线的
* ListView的标准构造函数会将所有item一次性创建，而ListView.builder会创建滚动到屏幕上显示的item
* CustomScrollView 用来保证列表的滚动方向一致 比如同时嵌套GridView, ListView

##### CheckBox

#####  FittedBox、AspectRatio、ConstrainedBox

* FittedBox 填充方式
* AspectRatio 宽高比

#### Layout

* column、row 常用的布局，继承自Flex弹性布局

* wrap 自适应宽度的布局

* Flow 灵活的布局，需要自定义布局策略或性能要求较高，注意FlowDelegate的`paintChildren()`方法
* Stack 类似Android FrameLayout



#### Dart语法

* 所有类型都是对象 继承Object， 未初始化的变量都是null,  数值、布尔值也是如此

* 内嵌表达式

  ```dart
  var s = 'haha';
  var s1 = 'this is a uppercased string: ${s.toUpperCase()}';
  ```

* 没有重载，可选参数{}，可忽略参数[]

* ```dart
// 要达到可选参数的用法，加上 {}
  void enableFlags({bool bold, bool hidden}) => print("$bold , $hidden");

  // 可忽略参数在函数定义时用 [] 符号指定
void enableFlags(bool bold, [bool hidden]) => print("$bold ,$hidden");
  
  // 可忽略参数时增加默认值
  void enableFlags(bool bold, [bool hidden = false]) => print("$bold ,$hidden");
  ```
  
* 没有public private protected 加下划线_即是私有

* extends\implements\with

  * 三种关系可以同时存在，但是有前后顺序：extends -> mixins -> implements

  * mixins(with) 可以混合多个类  *it is compatible with single-inheritance because it is linear*.  

  * ```dart
    class A {
      String content = 'A Class';
    
      void a(){
        print("a");
      }
    }
    
    class B with A{
    
    }
    
    B b = new B();
    print(b.content);
    b.a();
    ```

* 相比kotlin swift等语言，同样可以用？处理null的判断，还有 ??=  `a??=value`如果a=null 则赋值为value，a??b类似三目运算符`(a != null)? a : b`

* 运算符重载关键字 operate

* await async Future

  * async 异步标识 await只能在async标记的函数中运行 Future 链式调用

    https://segmentfault.com/a/1190000014396421
  
* 以下划线_ 开头为私有变量，Dart没有public、private、protect关键字

* **级联运算符“…”，在同一个对象上连续调用多个函数以及访问成员**

#### 打包集成

* 去除 右上角 debug标识 debugShowCheckedModeBanner: false
* 四种模式
  * Debug 打开所有断言、debugging信息，flutter run
  * Release 只能直机运行 flutter run —realease
  * Profile 只能真机运行 与Release基本一致 flutter run —profile
  *  Test 桌面运行与Debug基本一致 flutter test

#### 命名规范

* 文件名小写、下划线连接   eg. app_main.dart

#### Trouble shoot

##### 工程导入集成

- 导入已有工程，File -》open 选中已有工程所在目录即可
- 为工程配置代理 AndroidStudio -》Preference -》Proxy 即可

##### 工程新建

- Creating flutter Project loading 时间过长，kill IDE进程 换镜像 
- flutter doctor 时 brew update 请耐心等待