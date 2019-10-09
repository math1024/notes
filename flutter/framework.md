[TOC]

* Flutter 仅接管了渲染层，真正涉及到存储等操作系统底层还需要调用原生， 跨平台的开发框架
* Dart 采用事件循环的机制来运行任务

#### UI 渲染

* CPU 负责图像数据计算，GPU 负责图像数据渲染，显示器则负责最终图像显示

  1. CPU 把计算好的、需要显示的内容交给 GPU

  2. GPU 完成渲染后放入帧缓冲区

  3. 视频控制器根据垂直同步信号（VSync）以每秒 60 次的速从帧缓冲区读取帧数据交由显示器完成图像显示
  4. Skia 是CPU向 GPU 提供视图数据的帮手
* 测量 》约束 》 布局 》 绘制 （布局边界）》合成渲染
* Widget -> Element -> RenderObject - >skia
* 约束沿着树向下传递，尺寸向上传递
* 与React相似，声明式的视图开发，而android、ios、js则是命令式视图开发，前者整体输出、后者精细控制
  * 尽量flutter可以在Element层减少真实渲染视图的修改，但widgte对象的实例创建销毁是不可避免的

#### Skia

* Skia 是跨平台的，因此它作为 Flutter iOS 渲染引擎被嵌入到 Flutter 的 iOS SDK 中，替代了 iOS 闭源Core Graphics/Core Animation/Core Text,  所以ios的包要大一些

#### 生命周期

* 创建视图（插入视图树） -》更新（更新视图树） -》销毁（从视图树中移除）

  * 创建：构造方法(1次) -> initState(1次) widget尚未建立-> didChangeDependencies -> build，随后完成页面渲染
  * 更新：3 个方法触发：setState、didChangeDependencies（locale change）、didUpdateWidget（hot load）
  * 销毁：系统会调用 deactivate 和 dispose (1次)

* 应用生命周期 WidgetsBindingObserver

  * resumed：可见的，并能响应用户的输入。
  *  inactive：处在不活动状态，无法处理用户响应。 
  * paused：不可见并不能响应用户的输入，但是在后台继续活动中

  iOS 开发中，我们可以通过 dispatch_async(dispatch_get_main_queue(),^{…}) 方法，让操作在下一个 RunLoop 执行；Android 开发中，我们可以通过 View.post()来保证在组件渲染后进行相关操作

  

#### Channel

* 解决逻辑复用问题
* BinaryMessage

#### 平台视图

* 解决原生视图复用问题
  * 地图、webview、相机

#### 单线程模型

* 单线程和异步不冲突  Future是对异步任务的封装
* MicroTask高优先级、EventTask （scheduleMicrotask）
* 事件队列会按照加入事件队列的顺序（即声明顺序），依次取出事件，最后同步执行 Future 的函数体及后续的 then
  * 如果Future没有事件循环，then会被加入微队列，已保证快速执行
* await async同步等待，否则then

#### 多线程模型

* isolate  `Isolate.spawn(doSth, "Hi");`

* isolate 回传消息

```dart
Isolate isolate;

start() async {
  ReceivePort receivePort= ReceivePort();// 创建管道
  // 创建并发 Isolate，并传入发送管道
  isolate = await Isolate.spawn(getMsg, receivePort.sendPort);
  // 监听管道消息
  receivePort.listen((data) {
    print('Data：$data');
    receivePort.close();// 关闭管道
    // 杀死并发 Isolate
    isolate?.kill(priority: Isolate.immediate);
    isolate = null;
  });
}
// 并发 Isolate 往管道发送一个字符串
getMsg(sendPort) => sendPort.send("Hello");

```

* 双向通信 compute 函数

#### 网络

* 定位、传输、解析
* 为什么不支持，没有gson fastjson
  * 运行时反射会增加二进制文件大小。
  * 反射后会默认使用所有代码构建应用程序，导致编译器无法优化编译期间未使用的代码
  * 应用安装包体积无法进一步缩小

#### 原生混编

* 统一管理  原生工程嵌入Flutter工程
* 混合管理  Flutter工和散入原生工程
  * 打包成aar或pod

#### 混合栈

* 原生单容器单页面
* Flutter单窗口多页面
  * FlutterView、FlutterViewController
* 应尽量避免与原生频繁界面切换、Flutter实例初始化成本高
  * 目前有FlutterBoost、Flutter共享isolate两种

#### 状态管理

* 封装数据、存放数据、开放获取方法
* 官方provider `ChangeNotifierProvider.value or MultiProvider`
* Consumer 保证只刷新需要变更的控件

#### Hot load

* 热重载的流程可以分为扫描工程改动、增量编译、推送更新、代码合并、Widget 重建 5 个步骤：
  * 刷新指定UI树，而不是整个界面
* 以下情况hot load 无效
  * 状态变化、初始化 lessWidget -> fulWidget
  * 全局变量、静态变量的修改
  * main方法、initState方法

#### 性能指标

* 页面异常率  异常次数/界面打开次数 NavigatorObserver
* 页面帧率 onReportTimings FPS=60* 实际渲染的帧数 / 本来应该在这个时间内渲染...
* 页面加载时长 addPostFrameCallback

#### 组件化&平台化

* 独立的组件可单独维护、升级、替换，可以依赖其它组件，只要保持功能不变，对外服务就没有影响
* 功能单一、抽象、稳定和尽可能不依赖其它模块
* UI属性、业务属性划分四象限，单向依赖，
* 平台化注重分层，如遇到跨层调用，可考虑用中间层来联接，如eventbus、provider\，route

#### 持续集成

* Travis CI install、script 和 deploy

#### 混合开发

* 总体思路：结合持续集成方法，flutter与native工程混合应该是可重复可配置的
* 将flutter模块嵌入到原生工程，以aa或framework的形式提供给native工程使用
* 跨技术栈的组件依赖