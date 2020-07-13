* VSCode config

```shell
sdk path
1. /Users/XXXX/xxxx/flutter/bin/cache/dart-sdk // flutter捆绑安装
2. /usr/local/Cellar/dart/ // brew 安装
3. 添加环境变量
```

* App

```shell
flutter devices
flutter doctor
flutter upgrade
```

* 多模拟器

```shell
// 多个模拟器
flutter emulators
// 启动模拟器
flutter emulators --launch apple_ios_simulator
```

* 多设备 web&mobile

```shell
flutter run -d chrome
flutter run -d mobileXXX 序列号
```

* 清理cache

```shell
flutter precache
```

* 切换渠道

```
flutter channel
flutter channel master
```

* 生成json解析
  * 先内后外、
  * 写实体类、添加注解、part .g.daa、执行以下命令生成文件

```dart
flutter packages pub run build_runner build
```

* Trouble
  *  Invalid `Podfile` file: cannot load such file --

```shell
flutter clean
flutter pub get
进入ios目录pod install
```

* 创建新工程

```dart
flutter create xxapp
//指定语言，安卓使用Kotlin，iOS使用Swift
flutter create -i swift -a kotlin xxapp
  
// Flutter平台插件工程，包含Dart层与Native平台层的实现
flutter create --template=plugin xxapp_plugin
// 混入原生工程
flutter create -t module xxapp_module
// 定义公共widget 
flutter create --template=package xxapp_package
  
Flutter对于平台级的包是plugin，比如主要是和平台相关的功能，如path_provider、sqlfilte,
用纯Dart的开发的包是package，这和平台无关，可以跨平台使用，比如bloc、provider、flutter_star
```

* 单元测试

```dart
flutter test
```

* 打包

```dart
// 默认realease包
flutter build apk
flutter build apk --debug

// clean
flutter clean
```

* 性能

```dart
// 衡量启动时间
flutter run --trace-startup --profile
* relayoutSubtreeRoot=up8，这意味着当它RenderParagraph被标及为”dirty”时，它的八个祖先也必须被标记为”dirty”
```

