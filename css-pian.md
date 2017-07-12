HTML & CSS 篇

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

* Flex 布局 Flex Layout

Flex Layout 是 CSS3 提供的新的布局方式。

```HTML
<body>
    <div class="container">
        <div class="col-1"></div>
        <div class="col-2"></div>
        <div class="col-3"></div>
    </div>
</body>
```

```css
.container {
    display: flex;
    width: 100%;
}
.container > div {
    height: 100px;
    border: 1px solid #000;
    flex: 1;
    position: relative;
}
```

##### 如何用 Flex 画出一个直径 100px 的圆，并放在屏幕中间？

这个问题要分成两部分：画出一个直径 100px 的圆 & 将某个 div 置于屏幕中间。

* 画出一个直径 100px 的圆：使用 `border-radius` 就好。
* 将一个 div 放置于屏幕中间：使用 CSS3 Flex 提供的两个新特性：`align-items` 和 `justify-content`
* 完整代码如下：

```HTML
<body>
    <div class="circle"></div>
</body>
```

```css
/* 以下 CSS 代码并没有考虑兼容性的问题 */
html {
    height: 100%;
    width: 100%;
}
body {
    /* 使用 CSS3 flex layout 使元素垂直居中 */
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 0;
    height: 100%;
}
.circle {
    /* 使用 border-radius 画出一个圆形 */
    width: 100px;
    height: 100px;
    border-radius: 50px;
    background: red;
}
```

* 建议大家了解以下  CSS3 的 Flex Layout。如果有精力的话，可以再去看看 CSS3 的最新布局系统 Grid Layout 。

##### CSS 如何实现垂直居中？

在我的理解中，垂直居中有两类：文本垂直居中和标签元素的垂直居中。

* 文本的垂直居中很简单，只需要在他的父标签上指定高度（`height`）与相同的行高（`line-height`）即可。
* 标签元素的居中方式比较多，也比较复杂。首先，我们可以使用 CSS3 的 Flex Layout 实现（见上一题），但是这种方法明显存在兼容性问题。所以，我们绕个弯路，用传统的方法实现以下垂直居中：

```

```

##### CSS 的怪异盒模型

##### CSS 新增了哪些特性和用法，其好处是什么？

这个问题太大了，简单列举几个：

* grid layout
* flex layout
* transition



