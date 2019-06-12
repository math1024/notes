[TOC]



#### UI

* StatuflulWidget SatelessWidget

* primarySwatch 主题颜色 

  ```dart
   return MaterialApp(
        theme: ThemeData(
          primarySwatch: Colors.green,
        ),
        ......
      );
  ```

* 按钮

  * RaisedButton ：凸起的按钮，其实就是Android中的Material
  * Design风格的Button ，继承自MaterialButton
  * FlatButton ：扁平化的按钮，继承自MaterialButton
  * OutlineButton	：带边框的按钮，继承自MaterialButton

* await async Future

  * async 异步标识 await只能在async标记的函数中运行 Future 链式调用

    https://segmentfault.com/a/1190000014396421



#### 命名规范

* 文件名小写、下划线连接   eg. app_main.dart