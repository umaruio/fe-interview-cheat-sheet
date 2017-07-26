# 算法、数据结构与设计模式篇

##### 常见的排序算法及其时间复杂度

推荐一篇文章：[http://www.jianshu.com/p/7d037c332a9d](http://www.jianshu.com/p/7d037c332a9d)

![](/assets/sort.png)

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



