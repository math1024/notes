[TOC]



#### 在线编程

* https://try.kotlinlang.org

#### 语言特性

* ?, !!非空判断
* var val 要么指定初始、要么指定类型
* kotlin中都是引用类型，默认不接受null, 如果为需要指定为null,需要使用？描述
* typealias 类型别名

#### 运算符、表达式

* 运算符会以方法的形式来实现 比如 a++  a.inc 所以可以重载运算符
* 闭区间 a..b [a, b]   开区间 a until b (a, b]   反向闭区间 b downTo a 
* 重载