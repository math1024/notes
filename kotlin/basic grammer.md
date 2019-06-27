[TOC]



#### 在线编程

* https://try.kotlinlang.org

#### 语言特性

* ?, !!非空判断
* var val 要么指定初始、要么指定类型
* kotlin中都是引用类型，默认不接受null, 如果为需要指定为null,需要使用？描述
* typealias 类型别名
* 扩展函数  比如String.lastChar

#### 关键字

* let 作用域包裹

#### 运算符、表达式

* 运算符会以方法的形式来实现 比如 a++  a.inc 所以可以重载运算符
* 闭区间 a..b [a, b]   开区间 a until b (a, b]   反向闭区间 b downTo a 
* 重载

#### 流程控制

* when代替java中的switch
* break continue 后可以添加标签直接跳出for

#### 集合

* mutable

#### 权限控制

* internal 同目录下访问，不能跨包访问
* 次构造器 constructor 必须以：this委托调用
* 数据类所有参数必须用val、var声明

#### 抽象类、密封类

* seal 

#### 伴生对象、委托

* 属性委托

#### Kotlin与java 相互调用

* JvmField @file:JvmName("Hello")
* @JvmOverLoaders

####  开发环境

* library 需要单独引入kotlin plugin
* kotlin可能通过字节码Decompile回至java
* Anka

#### 踩坑

* 重写java方法时，可空对象一定要加入问号
* aroute kapt注解

#### 

