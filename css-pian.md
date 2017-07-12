# HTML & CSS 篇

##### CSS 三列布局的实现方案（左右两列宽度固定，中间自适应）：

* 圣杯布局 Holy Grail Layout

这种布局源于一篇文章：[https://alistapart.com/article/holygrail。它利用](https://alistapart.com/article/holygrail。它利用) CSS 负边距（Negative Margin）强行将左右两边的盒子移动到中间盒子的左右两边。

```HTML
<body>
    <div class="container">
        <div class="middle"></div>
        <!-- 因为要先渲染 .middle，所以 .middle 一定要写在第一个 -->
        <div class="left"></div>
        <div class="right"></div>
    </div>
</body>
```

```css
.container {
    /* 压缩左右内边距，留出 .left 和 .right 的距离 */
    padding: 0 200px;
}
.container > div {
    height: 200px;
    float: left;
}
.middle {
    width: 100%;
    background: blue;
}
.left {
    margin-left: -100%; /* 用 -100% 吃掉 .middle 的宽度 */
    position: relative; /* 相对 .container -200px */
    left: -200px;
    width: 200px;
    background: red;
}
.right {
    margin-left: -200px; /* 用 -200px 吃掉 .right 自己的宽度 */
    position: relative; /* 相对 .container -200px */
    right: -200px;
    width: 200px;
    background: green;
}
```

* 双飞翼布局 Flying Swing Layout

这种布局源于淘宝的 UED

```HTML
<body>
    <div class="container">
        <div class="middle">
            <div class="middle-container"></div>
        </div>
        <div class="left"></div>
        <div class="right"></div>
    </div>
</body>
```

```css
.container > div {
    float: left;
    height: 200px;
}
.middle {
    width: 100%;
    background: red;
}
.middle-container { /* 添加 .middle-container 包裹内容 */
    height: 200px;
    margin: 0 200px;
    background: darkred;
}
.left {
    width: 200px;
    margin-left: -100%;
    background: blue;
}
.right {
    width: 200px;
    margin-left: -200px;
    background: green;
}
```

* Flex 布局

Flex Layout 是 CSS3 提供的新的布局方式。

```

```

##### 如何用 Flex 画出一个直径 100px 的圆，并放在屏幕中间？

##### CSS 如何实现垂直居中？

##### CSS 的怪异盒模型

##### CSS 新增了哪些特性和用法，其好处是什么？



