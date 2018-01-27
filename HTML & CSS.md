# HTML & CSS 篇

##### CSS 三列布局的实现方案（左右两列宽度固定，中间自适应）： {#css-3-col-layout}

* 圣杯布局 Holy Grail Layout

这种布局源于一篇文章：[https://alistapart.com/article/holygrail](https://alistapart.com/article/holygrail) 。它利用CSS 负边距（Negative Margin）强行将左右两边的盒子移动到中间盒子的左右两边。

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

##### 如何用 Flex 画出一个直径 100px 的圆，并放在屏幕中间？ {#flex-circle-center}

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

* 建议大家了解一下  CSS3 的 Flex Layout。如果有精力的话，可以再去看看 CSS3 的最新布局系统 Grid Layout 。

##### CSS 如何实现垂直居中？ {#css-vertical-center}

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

##### CSS 的怪异盒模型 {#css-weird-box}

由于某些历史遗留问题，CSS 的盒子模型有两种标准：W3C 和 IE 。怪异盒模型主要表现在 IE 上，当不对 Doctype 进行定义时，会触发怪异模式。  
标准盒模型中，一个 block 的总宽度 = `width` + `margin-left` + `margin-right` + `padding-left` + `padding-right` + `border-left` + `border-right`  
而怪异盒模型中，一个 block 的总宽度 = `width` + `margin-left` + `margin-right` ，`width` 包含了 `padding` 和 `border` ；高度也是一样的区别。  
在 CSS3 中，`box-sizing` 指定为 `border-box` 时，会采用怪异盒计算。

##### CSS3 新增了哪些特性和用法，其好处是什么？ {#css3-new-feature}

这个问题太大了，简单列举几个：

###### 新增的布局方式：

* grid layout
* flex layout

###### 新增的动画属性

* transition
* transform

###### 新增的计算属性

* calc 属性

好处的话，一个是布局更灵活快速了，还有就是提供了丰富的动画接口，可以更简洁高效的实现动画效果了。

##### 什么是 BFC？ {#bfc}

BFC 是 Block Formatting Context 的缩写，中文名叫块级格式化上下文。它的 MDN 链接：[https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block\_formatting\_context](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

这个概念落脚点在上下文，即一个包含环境。换言之就是我们创建了一个块级元素，而这个元素又属于 BFC 规定的那几种元素之一，那它就和它的子元素一起构成了一个块级格式化上下文。要注意的是：一个块格式化上下文包括创建它的元素内部所有内容，**除了**被包含于创建新的块级格式化上下文的后代元素内的元素。\(这个概念我也不是很清楚，需要进一步扩充。\)

##### CSS 的盒子模型（IE 和 W3C） {#css-box-model}

这是一个很老的知识点了，是 CSS 很早的一个布局概念。之所以分成 IE 和 W3C 两种，是因为某些历史原因导致了其相互的差异。主要的差异就是上边提到的**怪异盒模型**的问题。  
MDN 盒子模型文档：[https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Box\_Model/Introduction\_to\_the\_CSS\_box\_model](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

##### CSS3 transition 属性的用法： {#css3-transition}

这是 CSS3 新提供的一个用来制作元素过度动效的属性，通常定义在 CSS 伪类中，也可以配合 `transform` 等动画属性一起使用。大致的用法如下：

```css
a:hover {
    transition: all 0.5s ease-out;
}
```

transition 本身是一个比较复杂和强大的属性，所以关于它的详细用法，可以查看文档：

[https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)

##### rem 和 em 的区别 {#rem-em}

在 CSS 中，em 和 rem 都属于灵活的单位，都会由浏览器根据实际情况转换成 px 值。

* 任何浏览器的默认字体高度都是 16px 。当然我们可以通过设置 font-size 强行改变这个高度。

* em 是相对长度单位。相对于当前对象内文本的字体尺寸。em 会继承父级元素的字体大小。

* rem 是 CSS3 新增的一个相对长度单位，r 是 root 的缩写。使用 rem 为元素设定字体大小时，仍然是相对大小，**但相对的只是 HTML根元素**。

##### CSS 中有哪些长度单位？ {#css-length-unit}

* 绝对长度单位
  * px 像素
  * in 英寸 （1 in = 96px）
  * cm 厘米 （1 cm = 37.8px）
  * mm 毫米
* 相对字体长度单位
  * em
  * rem
  * points （默认 1 point = 1/72 in）
  * pica （1 pc = 12 pt）
  * ex 一个基于当前字体 x 的高度度量的属性
  * ch 基于 0 的宽度
* 可视区百分比长度单位
  * vw 可视区宽度
  * vh 可视区高度
  * vmin 取 vw 和 vm 的最小值
  * vmax 取二者最大值
* 特殊的单位
  * 百分比

##### 如何实现一个矩形的椭圆边角 {#css-border-radius}

方法一：使用 `border-radius`（IE9+）  
方法二：使用贴图方式，在矩形的四个角进行贴图。

##### 移动端布局方案 {#mobile-layout}

由于移动端的屏幕比例不固定，所以布局时大多采用流式布局。当然，目前也有一些实践使用了固定布局。移动端布局要注意的几点：

* 指定好 `viewport`
  * `width`: 设置 `viewport` 的宽度（即之前所提及到的，浏览器的宽度详），这里可以为一个整数，又或者是字符串`"width-device"`
  * `initial-scale`: 页面初始的缩放值，为数字，可以是小数
  * `minimum-scale`: 允许用户的最小缩放值，为数字，可以是小数
  * `maximum-scale`: 允许用户的最大缩放值，为数字，可以是小数
  * `height`: 设置 `viewport` 的高度（我们一般而言并不能用到）
  * `user-scalable`: 是否允许用户进行缩放，`'no'` 为不允许，`'yes'` 为允许
* 善用 `rem`

我没有经历过移动端开发，所以这方面的知识仅限于了解，欢迎扩充。

##### canvas 切图的原理 {#canvas-cropper}

这个问题问的是如何使用 canvas 进行图片裁切的操作，比如对头像的裁切上传。  
思路不难，先把图片渲染到 `canvas` 画布上，在将一个 `div` 蒙版置于 `canvas` 上，然后获取 div 包裹的部分。  
代码：[https://github.com/lcx960324/easycropper](https://github.com/lcx960324/easycropper)

##### 常见的 CSS Selector {#unpopular-css-selector}

[https://www.w3schools.com/cssref/css\_selectors.asp](https://www.w3schools.com/cssref/css_selectors.asp)  
[http://www.runoob.com/cssref/css-selectors.htm](http://www.runoob.com/cssref/css-selectors.html)

| 选择器 | 例子 | 描述 |
| :--- | :--- | :--- |
| element+element | div+p | 选择紧接在&lt;div&gt;元素后的所有&lt;p&gt;元素 |
| \[attribute\] | \[target\] | 选择有target属性的所有元素 |
| \[attribute=value\] | \[target=\_blank\] | 选择target属性为"\_blank"的所有元素 |
| \[attribute~=value\] | \[title~=flower\] | 选择title属性包含"flower"的所有元素 |
| \[attribute&brvbar;=value\] | \[lang&brvbar;=en\] | 选择lang属性以"en"开头的元素 |
| \[attribute^=value\] | a\[src^="https"\] | 选择src属性以"https"开头的每个&lt;a&gt;元素 |
| \[attribute$=value\] | a\[src$=".pdf"\] | 选择src属性以".pdf"结尾的每个&lt;a&gt;元素 |
| \[attribute\*=value\] | a\[src\*="abc"\] | 选择src属性中包含"abc"的每个&lt;a&gt;元素 |
| :link | a:link | 选择所有未被访问的每个&lt;a&gt;元素 |
| :visited | a:visited | 选择所有已被访问的每个&lt;a&gt;元素 |
| :active | a:active | 选择激活状态（按下）的&lt;a&gt;元素 |
| :hover | a:hover | 选择鼠标指针位于其上的&lt;a&gt;元素 |
| :focus | input:focus | 选择获得焦点的 input 元素 |
| :first-letter | p:first-letter | 选择每个&lt;p&gt;元素的首字母 |
| :first-line | p:first-line | 选择每个&lt;p&gt;元素的首行 |
| :first-child | p:first-child | 选择属于父元素的第一个子元素的每个&lt;p&gt;元素 |
| :before | p:before | 在每个&lt;p&gt;元素的内容之前插入内容 |
| :after | p:after | 在每个&lt;p&gt;元素之后插入内容 |
| element1~element2 | p~ul | 选择同级元素中&lt;p&gt;元素后的每个&lt;ul&gt;元素 |
| :not\(selector\) | :not\(p\) | 选择非&lt;p&gt;元素的每个元素 |

##### display: none 和 visibility: hidden 的区别

`display: none` 不会保留元素空间，会触发 reflow。  
`visibility: hidden` 会保留元素空间，只是视觉效果上不显示而已，不会触发 reflow，但是会触发 repaint。

##### 解释一下 reflow （回流）与 repaint（重绘）

元素的外观被改变，但是布局未改变时，会触发 repaint。它不会影响到 DOM 结构的渲染。  
元素布局发生改变的时候会触发 reflow ，它会影响到 DOM 结构。

##### HTML5 新增了哪些元素？

HTML5 新增了许多元素，使得 HTML Tag 的语义更加明确化，内容形式更加丰富。具体的信息可以参考我的一篇翻译：

[http://www.jianshu.com/p/8ca24717f09b](http://www.jianshu.com/p/8ca24717f09b)

##### 移动端适配方案

[https://github.com/riskers/blog/issues/17](https://github.com/riskers/blog/issues/17)  
[https://github.com/riskers/blog/issues/18](https://github.com/riskers/blog/issues/18)

##### 一个 Input 一个 Button，Button 里的文字长度不确定，怎么在一行内实现两个元素的自适应？

参考一篇文章：[https://segmentfault.com/a/1190000004424442](https://segmentfault.com/a/1190000004424442)

###### 使用 Table 布局

```HTML
<body>
    <div class="container">
        <div class="left">
            <input type="text" class="input">
        </div>
        <div class="right">
            <input type="button" value="this is a button" class="button">
        </div>
    </div>
</body>
```

```css
.contaienr {
    display: table;
    table-layout: fixed;
}
.left {
    display: table-cell;
    width: 100%;
}
.input {
    width: 100%;
    display: block;
}
.right {
    width: 100%;
    display: table-cell;
}
.button {
    margin-left: 10px; /* 避免重叠 */
}
```

###### 使用 Flex 布局

```HTML
<body>
    <div class="container">
        <div class="left">
            <input type="text" class="input">
        </div>
        <div class="right">
            <input type="button" value="a button!">
        </div>
    </div>
</body>
```

```css
.container {
    display: flex;
}
.left {
    margin-right: 10px;
    width: 100%;
}
.input {
    width: 100%;
}
```

###### 使用 Float & BFC

```HTML
<body>
    <div class="container">
        <div class="right">
            <input type="button" value="a button" class="button">
        </div>
        <div class="left">
            <input type="text" class="input">
        </div>
    </div>
</body>
```

```css
.left {
    overflow: hidden; /* Activate BFC */
    padding-right: 10px; /* 避免重叠 */
}
.input {
    display: block;
    width: 100%;
}
.right {
    float: right;
}
```

##### 关于CSS边距折叠的问题

[https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS\_Box\_Model/Mastering\_margin\_collapsing](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)

