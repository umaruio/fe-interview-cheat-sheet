# JavaScript 篇

##### JS 的基本类型有哪些，引用类型有哪些？

六种原始类型（基本类型）：Undefined，Null，Boolean，Number，String，Symbol（ES6新增）

引用类型：Object，Array，Date，RegExp，Function，基本包装类型（Boolean，Number，String 这是三种特殊的引用类型，也可以算作基本类型）

##### 哪些类型是存在于栈上的，哪些是存在于堆上的？

基本类型保存在栈上。

![](/assets/基本类型.png)

引用类型的引用保存在栈上，其对象保存在堆中。

![](/assets/引用类型.png)

##### null 和 undefined 的区别

1. 含义不同：

##### JS 的继承有哪几种，分别有什么特点。

在面向对象语言中，继承分为两种：

* 接口继承：只继承方法签名
* 实现继承：继承实际的方法

因为 JavaScript 没有继承关键字，所以 JavaScript 实现继承的方法很特殊，大致有以下几种：

* 原型链继承（最常见）
* 构造继承
* 实例继承
* 拷贝继承



