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

#### 语法

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

    

* await async Future

  * async 异步标识 await只能在async标记的函数中运行 Future 链式调用

    https://segmentfault.com/a/1190000014396421

#### 打包集成

* 去除 右上角 debug标识 debugShowCheckedModeBanner: false
* 四种模式
  * Debug 打开所有断言、debugging信息，flutter run
  * Release 只能直机运行 flutter run —realease
  * Profile 只能真机运行 与Release基本一致 flutter run —profile
  *  Test 桌面运行与Debug基本一致 flutter test

#### 命名规范

* 文件名小写、下划线连接   eg. app_main.dart