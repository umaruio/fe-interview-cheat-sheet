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

```HTML
<body>
    <div class="vertical"></div>
</body>
```

```css
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
.vertical {
    width: 100px;
    height: 100px;
    background: red;
    margin: 0 auto; /* 最简单的水平居中方式 */
    /* 以下是垂直居中的代码： */
    position: relative;
    top: 50%;
    margin-top: -50px;
}
```

当然，CSS3 还提供了另一种垂直居中的方案：`transform` 。这个属性用来修改 CSS 视觉格式模型的坐标空间，说白了就是移动当前元素。代码如下：

```css
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
.vertical {
    width: 300px;
    height: 300px;
    background: orange;
    margin: 0 auto;
    position: relative;
    top: 50%;
    transform: translateY(-50%); /* 将元素沿 Y 轴方向移动自身的 50% */
}
```

##### CSS 的怪异盒模型

这个话题有点大，待我慢慢扩充。

##### CSS 新增了哪些特性和用法，其好处是什么？

这个问题太大了，简单列举几个：

* grid layout
* flex layout
* transition
* calc 属性
* transform 属性

##### 什么是 BFC？

BFC 是 Block Formatting Context 的缩写，中文名叫块级格式化上下文。它的 MDN 链接：[https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block\_formatting\_context](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

这个概念落脚点在上下文，即一个包含环境。换言之就是我们创建了一个块级元素，而这个元素又属于 BFC 规定的那几种元素之一，那它就和它的子元素一起构成了一个块级格式化上下文。要注意的是：一个块格式化上下文包括创建它的元素内部所有内容，**除了**被包含于创建新的块级格式化上下文的后代元素内的元素。\(这个概念我也不是很清楚，需要进一步扩充。\)

##### CSS 的盒子模型（IE 和 W3C）

这是一个很老的知识点了，是 CSS 很早的一个布局概念。之所以分成 IE 和 W3C 两种，是因为某些历史原因导致了其相互的差异。

* W3C 的 CSS 盒模型
* IE 的 CSS 盒模型

##### CSS3 transition 属性的用法：

这是 CSS3 新提供的一个用来制作元素过度动效的属性，通常定义在 CSS 伪类中，也可以配合 `transform` 等动画属性一起使用。大致的用法如下：

```css
a:hover {
    transition: all 0.5s ease-out;
}
```

transition 本身是一个比较复杂和强大的属性，所以关于它的详细用法，可以查看文档：

[https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)

##### rem 和 em 的区别

在 CSS 中，em 和 rem 都属于灵活的单位，都会由浏览器根据实际情况转换成 px 值。

* 任何浏览器的默认字体高度都是 16px 。当然我们可以通过设置 font-size 强行改变这个高度。

* em 是相对长度单位。相对于当前对象内文本的字体尺寸。em 会继承父级元素的字体大小。

* rem 是 CSS3 新增的一个相对长度单位，r 是 root 的缩写。使用 rem 为元素设定字体大小时，仍然是相对大小，**但相对的只是 HTML根元素**。

##### CSS 中有哪些长度单位？

* 绝对长度单位
  * px 像素
  * in 英寸 （1 in = 96px）
  * cm 厘米 （1 cm = 37.8px）
  * mm 毫米
* 相对字体长度
  * em
  * rem
  * points （默认 1 point = 1/72 in）



