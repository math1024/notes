[TOC]



#### 测试题

1. widget 描述

   widget是flutter里对视图的一种轻量化描述，不可变，每次变更都会驱动渲染更新， RenderObject负责渲染

2. widget 生命周期

   State 是widget生命周期承载者，widget不变，state变；initState在State对象插入树时调用

   setState主动刷新 didchangeDependencies didUpdateWidget 被动触发， widget被移除时调用deactivate和dispose方法

3. ListView

   ListView通过外部Controller获取滚动状态、StatelessWidget、嵌套滚动时需使用CustomScrollView

   *可以一次全部创建ListView，也可以需要时才创建子widget ListView.Builder* 

4. 自定义widget

   可以组装也可CustomPaint，还可以继承

5. InheritedWidget\Notification\EventBus\Provider 都可以传递数据 

6. a??b  ==  (a!=null)?a:b 

7. Isolate

   Dart通过Isolate并发、Isolate有自己的事件循环独占资源、

   Future是基于事件循环实现的异步、Isolate之前通过管道实现双向通信

8. Future顺序

9. 持久化数据 

   文件适用于字符串或二进制对象持久化、sharedPreferences适用于持久化小型键值对

   数据库适用于持久化一个格式化对句 *Embedder?*

10. Flutter 动画

    动画的状态、控制与渲染是分享的，会频繁刷新、AnimatedWidget可以缩小动画的刷新范围

    AnimateBuider继承AnimatedWidget，可以实现渲染与动画解耦

11. 原生方法调用

    原生接口的封装与调用是在FlutterView注册实现的，Dart和原生代码之间的通信是通过方法通道

    实现、调用过程可以通过try-catch实现的

12. Dart类实例初始化

    支持初始化列表，可提前对变量赋值，*同类构造函数可以进行重写向转发？*，通过mixin解决多继承问题

    对于同一个父类，子类可以分别采用继承、接口实现和mixin的方式实现类的复用

13.  依赖管理

    pubspec.yaml用于管理flutter工程资源依赖、运行环境和代码依赖

    pubspec.yaml\pubspec.lock都要纳个版本管理

    pubspec.lock所描述的组件依赖会以缓存形式下载到本地 在.package文件

14. Hot Reload

    main函数、initState、全局变量的改动是不支持Hot Reload

15.  编译模式

    断言只在Debug模式下生效 Debug模式支持JIT，DartVm提供运行时变量可以获取当前的编译模式kReleaseMode

16.  自动化测试 ？

    测试用例需要在pubspec.yaml的dev_devpendencies声明依赖，对于外部依赖可以通过Mock方式返回数据 

17.  异常处理

    Isolate中的异常无法在主Isolate中获取、Zone可以集中处理应用的未处理异常、FlutterError可以集中处理Flutter框架中的异常

18.  FPS

    帧更新绘制依靠vsync信号驱动、丢帧是在绘制时间内占用多个vsync周期

19.  App架构设计

    组件关系通过分层划分实现，边界和弹性都需要考虑

20. 工程混编

    Fluttter原生组件的封装 aar（Android）和Framework（Pod）

    .flutter-plugins文件记录了插件所对应的原生组件封装

    FlutterView可以用于展示 Flutter模块工程的页面

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
  
// 设置背景 
Scaffold(
   appBar: AppBar(
     title: Text('State Select Entrance'),
     backgroundColor: Colors.cyan,
     brightness: Brightness.dark,),
   backgroundColor: Colors.amberAccent,)
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

##### SafeArea

* 处理异形屏

#### 动画

* 三要素
  *  Animation 动画什么样 规律、只负责动画，不管渲染
  * AnimationCortroller 周期
  * Listener 执行回调
* vsync 不可见时暂停动画
* AnimatedWidget 与 AnimatedBuilder
* hero 共享动画
* lerp 插值

* PositionedTransition
* DecoratedBoxTransition

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

* Map

  * HashMap是无序的，这意味着它迭代的顺序是不确定的
  * LinkedHashMap按key的插入顺序进行迭代
  * SplayTreeMap按key的排序顺序进行迭代

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

// 通过then接收返回值
  Navigator.of(context)
                          .push(MaterialPageRoute(builder: (context) {
                        return EventFind(pageSource: EventPageSource.fromMainPage);
                      })).then((value) => print(value));
```


#### 横竖屏

* OrientationBuilder，需要针对横竖屏也两套布局
* MediaQueryData 获取屏幕尺寸

```dart
padding: const EdgeInsets.all(10.0),
width: MediaQuery.of(context).size.width,
height: 300,
```



#### 打包集成

* 去除 右上角 debug标识 debugShowCheckedModeBanner: false
* 四种模式
  * Debug 打开所有断言、debugging信息，flutter run
  * Release 只能直机运行 flutter run —realease 关闭了所有断言 assert
    * kReleaseMode
  * Profile 只能真机运行 与Release基本一致 flutter run —profile
    * GPU 红色为异常，出现在GPU表示渲染复杂，
    * UI 性能 出现UI表示代码过于复杂， Flame chart
  *  Test 桌面运行与Debug基本一致 flutter test
* 三个阶段
  - 开发-尽可能提供上下文信息
  - 测试-覆盖全面，不同配置的切换
  - 发布-去除测试代码、精简测试信息

* 四个步骤
  * 分离可配置部分
  * 不同配置对应不同应用入口
  * 运行期借用数据共享InheritedWidget将配置应用到对应入口
  * 打包提供不同环境的测试包

#### 命名规范

* 文件名小写、下划线连接   eg. app_main.dart

#### 运行调试

* flutter emulator --launch

* debugPrint

* 布局调试
  
  * Debug Painting
  
  ```dart
  void main() {
    debugPaintSizeEnabled = true; // 打开 Debug Painting 调试开关
    runApp(new MyApp());
  }
  ```
  
  * inspector

* checkerboardOffscreenLayers 检查多视图叠加开关，checkerboardRasterCacheImages

  检查缓存的图像开关
  
* pubspec.yaml test包mockito包，

  ```dart
  dev_dependencies:
    test: 
    mockito:// 模拟网络
    flutter_test: 
      sdk: flutter// UI
  ```

  	* 测试用例三部分，定义、执行、验证
	* 包装在test内部 test是Flutter提供的测试类
  	* 多个test可以放同一组group
  
  ```dart
group('name1', () {
  	test('name2', (){});
  	test('name3', (){})
  })
  ```
  
  * testWidgets widgetTester

  ```
testWidgets('name', (Widgettester tester) async {
     await test.pumpWidget(MyApp())
     expect(find.text('0'))
  })
  ```
  
* 异常处理

  * 同步异常 try-catch

  * 异步异常 catchError

  * Zone.runZoned 自己管理异常

    ```dart
    runZoned<Future<Null>>(() async {
      runApp(MyApp());
    }, onError: (error, stackTrace) async {
     //Do sth for error
    });
    
    ```

  * Framework 异常 ErrorWidget.builder

    ```dart
    FlutterError.onError = (FlutterErrorDetails details) async {
      Zone.current.handleUncaughtError(details.exception, details.stack);
    };
    
    runZoned<Future<Null>>(() async {
      runApp(MyApp());
    }, onError: (error, stackTrace) async {
     //Do sth for error
    });
    
    ```

    

#### print debugPrint log

* [debug logs](https://flutter.dev/docs/testing/code-debugging
* debugPrint()
  If you output too much at once, then Android sometimes discards some log lines. To avoid this, use debugPrint(), from Flutter’s foundation library. This is a wrapper around print that throttles the output to a level that avoids being dropped by Android’s kernel.

```dart
// developer log
import 'dart:developer' as developer;

void main() {
  developer.log('log me', name: 'my.app.category');

  developer.log('log me 1', name: 'my.other.category');
  developer.log('log me 2', name: 'my.other.category');
}

// std out
stderr.writeln('print me');

// debugPrint
```



#### Trouble shoot

##### 工程协作

* 固定版本号，避免api不兼容  可以考虑提交pubspec.yaml\pubspec.lock

##### 工程导入集成

- 导入已有工程，File -》open 选中已有工程所在目录即可
- 为工程配置代理 AndroidStudio -》Preference -》Proxy 即可

##### 工程新建

- Creating flutter Project loading 时间过长，kill IDE进程 换镜像 
- flutter doctor 时 brew update 请耐心等待