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
```

* 单元测试

```dart
flutter test
```

