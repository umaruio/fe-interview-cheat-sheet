# 算法、数据结构与设计模式篇

## 常见的排序算法及其时间复杂度

推荐一篇文章：[http://www.jianshu.com/p/7d037c332a9d](http://www.jianshu.com/p/7d037c332a9d)

![](../assets/sort.png)

这是我对这些算法的 JS 实现：[https://github.com/lcx960324/fe-interview-cheat-sheet-demo/tree/master/Algorithm/Sort](https://github.com/lcx960324/fe-interview-cheat-sheet-demo/tree/master/Algorithm/Sort)

## 常见的查找算法及其时间复杂度

## 什么是完全二叉树？

若设二叉树的深度为 h，除第 h 层外，其它各层 \(1 ～ h-1\) 的结点数都达到最大个数，第 h 层所有的结点都连续集中在最左边，这就是完全二叉树。

## 堆排序的原理

利用大顶堆（小顶堆）根元素最大（最小）的特性，每次都构建大顶堆（小顶堆）然后再去除根元素重新构建大顶堆（小顶堆），即可完成排序。

## Fibonacci 数列的实现方法

### 循环法

```javascript
function fibonacci(n) {
  var prevA = 1,
    prevB = 1;
  if (n === 0) return 0;
  if (n === 1 || n === 2) return 1;
  var curr;
  for (i = 2; i < n; i++) {
    curr = prevA + prevB;
    prevA = prevB;
    prevB = curr;
  }
  return curr;
}
```

### 递归法

```javascript
function fibonacci(n) {
  if (n === 1 || n === 2) {
    return 1;
  }
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## 找出 n 个数中第 k 大的数

使用 BFPRT 算法（线性查找法），时间复杂度 O\(n\) 。  
推荐两篇关于 BFPRT 的文章：

- [https://segmentfault.com/a/1190000008322873](https://segmentfault.com/a/1190000008322873)
- [https://github.com/lawlite19/AlgorithmExercises/blob/master/零、算法说明/BFPRT.md](https://github.com/lawlite19/AlgorithmExercises/blob/master/零、算法说明/BFPRT.md)

我的 BFPRT 代码：[https://github.com/lcx960324/fe-interview-cheat-sheet-demo/blob/master/Algorithm/Top K Problem.js](https://github.com/lcx960324/fe-interview-cheat-sheet-demo/blob/master/Algorithm/Top%20K%20Problem.js)

## 从 100 万个数中找出最大的 100 个数

这道题可以这么解：先找出第 100 大的数，然后再找出所有比这个数大的数。  
找出第 100 大的数是一个 Top K 问题，可以使用 BFPRT 求解。  
找出所有比这个数大的数，遍历就好啦~

## 两个房间，分别有三个开关和三个灯，每个房间只能进去一次，如何判断出开关对应的灯？

进入第一个房间，打开全部的三盏灯，如果都亮了，那很容易判断对应的灯是哪个了。  
如果亮了两盏，先在这个房间确定两盏的对应关系，然后再去另一个房间确认另一个房间两盏的对应管系。  
如果亮了一盏，先确定一盏的对应关系，然后把剩下找不到的两盏灯的其中一盏打开，然后去另一个房间确定剩下的关系。但是这只能确定一个房间的对应关系。  
如果一盏都没亮，那要不让那个灯开一会儿，然后过个五分钟再开另一盏灯，关掉第一盏，然后去另一个房间摸一下温度？但是这只能确定一个房间的对应关系。

## DOM 树的深度优先遍历与广度优先遍历

### 深度优先

```javascript
function interactor(node) {
  console.log(node);
  if (node.children.length) {
    for (let i in node.children) {
      interactor(node.children[i]);
    }
  }
}
```

### 广度优先

```javascript
function interactor(node) {
  const arr = [];
  arr.push(node);
  while (arr.length > 0) {
    node.arr.shift();
    console.log(node);
    if (node.children.length) {
      for (let i in node.children) {
        arr.push(node.children[i]);
      }
    }
  }
}
```

## JS 有哪些常用的设计模式

其实传统软件开发的设计模式很多都可以直接套用到前端项目上，比如：单例模式、工厂模式、观察者模式、适配器模式、代理模式。  
推荐一篇文章：[http://www.alloyteam.com/2012/10/common-javascript-design-patterns/](http://www.alloyteam.com/2012/10/common-javascript-design-patterns/)

强烈建议大家认真学习一下前端提的最多的设计模式：**观察者模式**。
