[TOC]



#### UI

##### StatuflulWidget SatelessWidget

##### themeData

```dart
MaterialApp(
  title: 'Flutter Demo',// 标题
  theme: ThemeData(// 设置主题
      brightness: Brightness.dark,// 设置明暗模式
      accentColor: Colors.black,//前景色为黑色
      primaryColor: Colors.cyan,// 主色调
      iconTheme:IconThemeData(color: Colors.yellow),// 设置 icon 主题色为黄色
      textTheme: TextTheme(body1: TextStyle(color: Colors.red))// 设置文本颜色为红色
  ),
  home: MyHomePage(title: 'Flutter'),
);

Theme.of(context).copyWith
```

##### Text

* 控制布局的参数(对齐、截断)、控制文本样式的参数style
* 分段显示TextSpan\ android spannedbuilder\ios NSAttributedString 

##### Image

* image.network\image.assets\image.file

* FadeInImage 提供占位图片 placeholder
* [CachedNetworkImage](https://pub.dev/packages/cached_network_image/)

##### Button

* RaisedButton ：凸起的按钮，其实就是Android中的Material
* Design风格的Button ，继承自MaterialButton
* FlatButton ：扁平化的按钮，继承自MaterialButton
* OutlineButton	：带边框的按钮，继承自MaterialButton
* shape属性可以定制样式

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

* android listview\recycleView.  ios UItableView

* ListTile 适合固定数量的文本
* ListView.builder 常用
  * itemExtent 指定高度或宽度
* ListView.separated 带分隔线的
  * separatorBuilder
* ListView的标准构造函数会将所有item一次性创建，而ListView.builder会创建滚动到屏幕上显示的item
* CustomScrollView 用来保证列表的滚动方向一致 比如同时嵌套GridView, ListView 视差滚动
* ScrollController\ScrollNotification

##### CheckBox

#####  FittedBox、AspectRatio、ConstrainedBox

* FittedBox 填充方式
* AspectRatio 宽高比

#####  ExpansionPanel

* 可扩展布局、类似二级菜单

##### Offstage

* 需要控制一个区域显示或者隐藏的时候用，比如loading

##### Layout

* [offical layout](https://flutter.dev/docs/development/ui/widgets/layout)

* column、row 常用的布局，继承自Flex弹性布局
  * mainAxisSize: MainAxisSize.min
* wrap 自适应宽度的布局
* Flow 灵活的布局，需要自定义布局策略或性能要求较高，注意FlowDelegate的`paintChildren()`方法
* Stack 类似Android FrameLayout

##### CustomPaint Canvas

* ios/android  drawRect/onDraw
* shouldRepaint true重绘 
* RepaintBoundary 绘制隔离

##### Semantics

* 帮助控件 

#### SafeArea

* 处理异形屏

#### widget间共享数据

* InheritedWidget 要和 StatefulWidget 中的 State 配套使用，数据由父控件到子控件
* Notification 数据子控件到父控件
* eventbus  发布订阅模式

#### 监听事件

* 原始 listener 

* GestureDetector

* RawGestureDetector 和 GestureFactory

  ```dart
  class MultipleTapGestureRecognizer extends TapGestureRecognizer {
    @override
    void rejectGesture(int pointer) {
      acceptGesture(pointer);
    }
  }
  ```

* 如果子控件有实现监听事件，父控件同类监听不会收到响应
* 事件向下传递、响应向上传递

----





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

* 相比kotlin swift等语言，同样可以用？处理null的判断，还有??=  `a??=value`如果a=null 则赋值为value，a??b类似三目运算符`(a != null)? a : b`

* 运算符重载关键字 operate

* await async Future

  * async 异步标识 await只能在async标记的函数中运行 Future 链式调用

    https://segmentfault.com/a/1190000014396421
  
* 以下划线_ 开头为私有变量，Dart没有public、private、protect关键字

* **级联运算符“…”，在同一个对象上连续调用多个函数以及访问成员**

* 线程模型，Dart单线程模型？

* Stream

#### 资源管理

* 放在assets目录下，在pubspec.yaml声明即可

* pubspec.yaml 包的元数据（比如，包的名称和版本）、运行环境（也就是 Dart SDK 与 Fluter SDK 版本）、外部依赖、内部配置（比如，资源管理）

  * pubspec.yaml 下什么 pubspec.lock 从哪下  .package 下完了放哪

* 目录批量指定并不递归，只有在该目录下的文件才可以被包括，

  如果需要指定其子目录，需要单独填写

* 替换应用图标、启动页

  * android/app/src/main/res/mipmap
  * ios/Runner/Assets.xcassets/AppIcon.appiconset  LaunchImage.imageset

* 优先使用当前像素密度相近的资源，没有资源时由低向高找

* 复用引用包中的资源

```dart
Image.asset('assets/placeholder.png', package: 'package4');
AssetImage('assets/placeholder.png', package: 'package4');
```



#### 路由

* Route 是页面的抽象 可构造页面名称、参数

  * 基本路由 MaterialPageRoute

  * 命名路由. 模块化基础

    ```左手
    MaterialApp(
        ...
        // 注册
        routes:{
          "second_page":(context)=>SecondPage(),
        },
        onUnknownRoute: (RouteSettings setting) => MaterialPageRoute（builder: (context) => UnknownPage())
    );
    Navigator.pushNamed(context,"second_page", arguments: "Hey");
    
    ```

    

#### 打包集成

* 去除 右上角 debug标识 debugShowCheckedModeBanner: false
* 四种模式
  * Debug 打开所有断言、debugging信息，flutter run
  * Release 只能直机运行 flutter run —realease
  * Profile 只能真机运行 与Release基本一致 flutter run —profile
  *  Test 桌面运行与Debug基本一致 flutter test

#### 命名规范

* 文件名小写、下划线连接   eg. app_main.dart

#### 运行调试

* flutter emulator --launch

#### Trouble shoot

##### 工程协作

* 固定版本号，避免api不兼容  可以考虑提交pubspec.yaml\pubspec.lock

##### 工程导入集成

- 导入已有工程，File -》open 选中已有工程所在目录即可
- 为工程配置代理 AndroidStudio -》Preference -》Proxy 即可

##### 工程新建

- Creating flutter Project loading 时间过长，kill IDE进程 换镜像 
- flutter doctor 时 brew update 请耐心等待