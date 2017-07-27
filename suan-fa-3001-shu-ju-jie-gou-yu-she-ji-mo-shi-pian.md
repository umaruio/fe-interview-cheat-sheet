# 算法、数据结构与设计模式篇

##### 常见的排序算法及其时间复杂度

推荐一篇文章：[http://www.jianshu.com/p/7d037c332a9d](http://www.jianshu.com/p/7d037c332a9d)

![](/assets/sort.png)

这是我对这些算法的 JS 实现：[https://github.com/lcx960324/fe-interview-cheat-sheet-demo/tree/master/Algorithm/Sort](https://github.com/lcx960324/fe-interview-cheat-sheet-demo/tree/master/Algorithm/Sort)

##### 常见的查找算法及其时间复杂度

##### Fibonacci 数列的实现方法

###### 循环法

```js
function fibonacci (n) {
    var prevA = 1, prevB = 1
    if (n === 0) return 0
    if (n === 1 || n === 2) return 1
    var curr
    for (i = 2; i < n; i++) {
        curr = prevA + prevB
        prevA = prevB
        prevB = curr
    }
    return curr
}
```

###### 递归法

```js
function fibonacci (n) {
    if (n === 1 || n === 2) {
        return 1
    }
    return fibonacci(n - 1) + fibonacci(n - 2)
}
```

##### 从 100 万个数中找出最大的 100 个数

##### DOM 树的深度优先遍历与广度优先遍历

###### 深度优先

```js
function interactor (node) {
    console.log(node)
    if (node.children.length) {
        for (let i in node.children) {
            interactor(node.children[i])
        }
    }
}
```

###### 广度优先

```js
function interactor (node) {
    const arr = []
    arr.push(node)
    while (arr.length > 0) {
        node.arr.shift()
        console.log(node)
        if (node.children.length) {
            for (let i in node.children) {
                arr.push(node.children[i])
            }
        }
    }
}
```

##### JS 有哪些常用的设计模式

推荐一篇文章：http://www.alloyteam.com/2012/10/common-javascript-design-patterns/

