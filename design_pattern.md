

#### 预备

* 领域设计
* 充血与贫血模式

#### SRP

* 业务、需求背景来判断是否满足单一原则
* 单一职责原则是为了实现代码高内聚、低耦合，提高代码的复用性、可读性、可维护性

#### Open Close

为了尽量写出扩展性好的代码，我们要时刻具备扩展意识、抽象意识、封装意识。这些“潜意识”可能比任何开发技巧都重要。

在写代码的时候后，我们要多花点时间往前多思考一下，这段代码未来可能有哪些需求变更、如何设计代码结构，事先留好扩展点，以便在未来需求变更的时候，不需要改动代码整体结构、做到最小代码改动的情况下，新的代码能够很灵活地插入到扩展点上，做到“对扩展开放、对修改关闭”。

还有，在识别出代码可变部分和不可变部分之后，我们要将可变部分封装起来，隔离变化，提供抽象化的不可变接口，给上层系统使用。当具体的实现发生变化的时候，我们只需要基于相同的抽象接口，扩展一个新的实现，替换掉老的实现即可，上游系统的代码几乎不需要修改。

#### LISP

多态是面向对象编程的一大特性，也是面向对象编程语言的一种语法。它是一种代码实现的思路。而里式替换是一种设计原则，是用来指导继承关系中子类该如何设计的，子类的设计要保证在替换父类的时候，不改变原有程序的逻辑以及不破坏原有程序的正确性。



#### IOC&DI

“控制”指的是对程序执行流程的控制，而“反转”指的是在没有使用框架之前，程序员自己控制整个程序的执行。在使用框架之后，整个程序的执行流程可以通过框架来控制。流程的控制权从程序员“反转”到了框架

那到底什么是依赖注入呢？我们用一句话来概括就是：不通过 new() 的方式在类内部创建依赖类对象，而是将依赖的类对象在外部创建好之后，通过构造函数、函数参数等方式传递（或注入）给类使用

#### KISS&YANGI

YAGNI 原则的英文全称是：You Ain’t Gonna Need It 不要去设计当前用不到的功能；不要去编写当前用不到的代码。实际上，这条原则的核心思想就是：不要做过度设计。

####  LOD

不该有直接依赖关系的类之间，不要有依赖；有依赖关系的类之间，尽量只依赖必要的接口（也就是定义中的“有限知识”）



#### Refactor

#### 命名&注释

* 可读可搜索、借助上下文缩短命名
* 做什么、怎么做、为什么

#### Review

* 通用
* 功能

### 创建型 ：将创建和使用代码解耦

#### 单例

#### 工厂

* 工厂模式是用来创建不同但是相关类型的对象（继承同一父类或者接口的一组子类），由给定的参数来决定创建哪种类型的对象。建造者模式用来创建一种类型的复杂对象，通过设置不同的可选参数，“定制化”地创建不同的对象
  * 顾客走进一家餐馆点餐，我们利用工厂模式，根据用户不同的选择，来制作不同的食物，比如披萨、汉堡、沙拉。对于披萨来说，用户又有各种配料可以定制，比如奶酪、西红柿、起司，我们通过建造者模式根据用户选择的不同配料来制作不同的披萨

#### 建造者

#### 原型

### 结构型 将不同功能代码解耦

#### 代理

* 它在不改变原始类（或叫被代理类）代码的情况下，通过引入代理类来给原始类附加功能

  

#### 桥接

* 第一种 GoF 的理解方式，弄懂定义中“抽象”和“实现”两个概念，是理解它的关键。定义中的“抽象”，指的并非“抽象类”或“接口”，而是被抽象出来的一套“类库”，它只包含骨架代码，真正的业务逻辑需要委派给定义中的“实现”来完成。而定义中的“实现”，也并非“接口的实现类”，而是一套独立的“类库”。“抽象”和“实现”独立开发，通过对象之间的组合关系，组装在一起

#### 装饰

* 代理类附加的是跟原始类无关的功能，而在装饰器模式中，装饰器类附加的是跟原始类相关的增强功能。
* 

#### 组合模式

* 组合模式的设计思路，与其说是一种设计模式，倒不如说是对业务场景的一种数据结构和算法的抽象。其中，数据可以表示成树这种数据结构，业务需求可以通过在树上的递归遍历算法来实现

### 享元模式

### 行为型 ：将不同的行为代码解耦

#### 观察者

* 框架的作用有：隐藏实现细节，降低开发难度，做到代码复用，解耦业务与非业务代码

#### 模版

* 模板方法模式在一个方法中定义一个算法骨架，并将某些步骤推迟到子类中实现。模板方法模式可以让子类在不改变算法整体结构的情况下，重新定义算法中的某些步骤
* 异步回调比较像观察者模式， 同步回调从应用场景上很像模板模式

#### 策略模式

#### 责任链

#### 状态模式

* 分支法、查表法、状态转换

#### 迭代器

* 完整的迭代器模式，一般会涉及容器和容器迭代器两部分内容

#### 访问者

* Double Dispatch 指的是执行哪个对象的方法，根据对象的运行时类型来决定；执行对象的哪个方法，根据方法参数的运行时类型来决定
* Single Dispatch，指的是执行哪个对象的方法，根据对象的运行时类型来决定；执行对象的哪个方法，根据方法参数的编译时类型来决定。所谓 Double Dispatch

### 备忘录

* 低频全量备份，高频增量备份

#### 命令模式

* 看起来与策略模式类似

  每个设计模式都应该由两部分组成：第一部分是应用场景，即这个模式可以解决哪类问题；第二部分是解决方案，即这个模式的设计思路和具体的代码实现。不过，代码实现并不是模式必须包含的

### 中介模式



### 大型复杂项目开发

#### 设计原则和思想的角度

#### 研发管理和开发技巧的角度

#### 聚焦在 Code Review

### TIPS

#### 不变模式

* 只有get没有set，多线程开发

#### 有状态无状态

```java
// 有状态函数: 执行结果依赖b的值是多少，即便入参相同，多次执行函数，函数的返回值有可能不同，因为b值有可能不同。
int b;
int increase(int a) {
  return a + b;
}

// 无状态函数：执行结果不依赖任何外部变量值，只要入参相同，不管执行多少次，函数的返回值就相同
int increase(int a, int b) {
  return a + b;
}
```

