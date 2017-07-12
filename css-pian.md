# HTML & CSS 篇

##### CSS 三列布局的实现方案（左右两列宽度固定，中间自适应）：

* 圣杯布局 Holy Grail Layout

这种布局源于一篇文章：[https://alistapart.com/article/holygrail。它利用](https://alistapart.com/article/holygrail。它利用) CSS 负边距（Negative Margin）强行将左右两边的盒子移动到中间盒子的左右两边。

```
<div class="container">
    <div class="middle"></div>
    <div class="left"></div>
    <div class="right"></div>
</div>
```

```
.left {
    margin-left: -100%;
```

* 双飞翼布局

这种布局源于淘宝的 UED

```

```

* Flex 布局

```

```

##### 如何用 Flex 画出一个直径 100px 的圆，并放在屏幕中间？

##### CSS 如何实现垂直居中？

##### CSS 的怪异盒模型

##### CSS 新增了哪些特性和用法，其好处是什么？



