## 前言

`CSS` 里有一个重要的东西，叫 `CSS` 盒模型，它几乎能贯穿我们学习 `CSS` 的整个阶段，如下图所示，就是我们所说的盒子模型：

[!![CSS Box model](https://mdn.mozillademos.org/files/8685/boxmodel-(3).png)]()

(注：图片来源 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model) )

"盒模型"中最外层透明的区域就是 `margin`所在，它会将其他区域从盒子模型内容中推开。

`margin` 一共有四个属性值， `margin-top` 、`margin-right` 、`margin-bottom` 和 `margin-left` 属性，也可以设置简写属性 `margin`。

`margin` 看起来比较简单，但是，它其实有自己的奥妙所在，比如我们在布局中经常遇到 `margin` 重叠效果等，接下来我们来看看 `margin` 究竟有什么神奇所在吧。

## margin 重叠

`margin` 重叠指的是垂直重叠，重叠的意思是，当我们规定一个模块的 `margin-bottom` 与 紧邻着的下一个模块的 `margin-top` 它们会发生重叠，它们之间不会出现较大的空白。因为代码会取两个值之间较大的那个，比如 第一个模块设置`margin-bottom: 50px` ，第二个模块设置 `margin-top: 100px` 那么第一个模块的 `margin-bottom` 则不会起作用，起作用的则是 第二个模块的 `margin-top` 也就是说他们之间的空白间距是 `100px` ，可能会有疑问，那 `50px` 跑哪里去了，其实是被包含在 `100px` 里面了 这就是所谓的 `margin` 重叠。

以下情况下，`margin` 会发生重叠：

* **相邻**的兄弟元素
* 完全空盒子
* 父元素与它的第一个或最后一个子元素

## 相邻的兄弟元素重叠

上述我们所描绘的情况就是相邻兄弟之间的 `margin` 重叠。

如下示例，有三个 `div` 元素。第一个 `div` 的顶部与底部的 `margin` 分别是 `50px` 第二个 `div` 的顶部与底部 `margin` 分别是 `20px` ，第三个 `div` 的顶部与底部 `margin` 是 `3em`。 那么出现的重叠情况是，第一个与第二个的间距是 `50px`, 因为第二个元素的顶部小于第一个底部的 `margin`，取两者之间较大的。第二个元素与第三个元素之间的间距则是 `3em` ，同理 `3em` 大于第二个元素的 底部 `20px`。

```html
<div class="box1">模块一</div>
<div class="box2">模块二</div>
<div class="box3">模块三</div>
```

```css
div {
  border: 1px solid #ddd;
  height: 200px;
}
.box1 {
  margin: 50px 0;
}
.box2 {
  margin: 20px 0;
}
.box3 {
  margin: 3em 0;
}
```

在线 [demo](https://jsbin.com/majavev/2/edit?html,css,output)

## 完全空盒子

什么是完全空盒子，就是盒子里面什么也没有就是完全的空盒子，没有内容也没有子元素，它顶部与底部的 `margin` 可能会相互重叠，如下示例，一个 `class` 为 `empty` 的元素顶部与底部的 `margin` 分别为 `50px` , 但是第一个元素与第三个元素之间的间距并没有 `100px` ，而是 `50px` 。这就是空盒子造成的 `margin` 重叠，如果我们在空盒子里面写入内容就会阻止 `margin` 合并。

```html
<div class="wrap">
    <div class="box1">模块一</div>
    <div class="box2 empty"></div>
    <div class="box3">模块三</div>
</div>
```

```css
.wrap {
  border: 5px dotted #000;
}
.box1, .box3 {
  height: 100px;
  background: #f60;
}
.empty {
  margin: 50px 0;
}
```

在线 [demo](https://jsbin.com/majavev/3/edit?html,css,output)

## 父元素和第一个或最后一个子元素

一开始接触布局时，我们可能会经常碰到这样的问题，我们给子级设置一个`margin-top` 值，如果没有清除 `BFC` 的话，常常看到的错觉是这样的：

![WX20190803-143924.png](https://i.loli.net/2019/08/03/MSaHkUWzL29hpRo.png)

从图上可以看到，第一项与最后一项与父元素的 `margin` 齐平，好像是子元素与父元素之间没有 `20px` 的 `margin` 一样。

```html
<div class="box">
  <div class="child"></div>
  <div class="child"></div>
</div>
```

```css
.box {
  background: green;
}

.child {
  height: 100px;
  background: red;
  margin: 20px;
}
```

这是因为子节点上的 `margin` 会随着父元素上的任何一边 `margin` 相互重叠，从而最终位于父元素的外部，造成的错觉像是父元素向下 `margin` 或者向上 `margin` 一样。

**注意：在 CSS 中，只指定了重置方向的 `margin` 重叠，即元素的顶部和底部的 `margin` 重叠。左右是不会发生重叠的。**

> 还有一点就是，margin 只在块的方向上发生重叠，比如段落之间。

## 阻止 margin 发生重叠

如果一个元素是绝对定位，或者是浮动的， 它的 `margin` 永远不会发生重叠， 因为他已经脱离文档流了。

如果是一个完全空的盒子，给它设置一个 `border` 或者 `padding` ，那么这个空盒子的 `margin` 则不会发生重叠。

```html
<div class="wrap">
  <div class="box1">模块一</div>
  <div class="box2 empty"></div>
  <div class="box3">模块三</div>
</div>
```

```css

.wrap {
  border: 5px dotted #000;
}
.box1, .box3 {
  height: 100px;
  background: #f60;
}
.empty {
  margin: 50px 0;
  /* border: 1px solid transparent; */
  padding: 1px;
}
```

在线 [demo](https://jsbin.com/majavev/5/edit?html,css,output)

那么为什么加上 `border` 或 `padding` 就可以了呢？ 那是因为如果一个空盒子加上 `border` 或者 `padding` 后就有高度了就变成非空盒子了。如果我们在代码布局上，我们标记一个为空的段落元素，如果不想让他造成与其他模块较大的空白，这时候我们做的 `margin` 重叠就有了一定的意义。

对于父元素和第一个或者最后一个子元素的 `margin` 重叠，如果我们向父级添加 `border`  或者  `padding` 那么子级上的 `margin` 则会保留。

## 创建格式化上下文（BFC）

**BFC (Block Formatting Context) 格式化上下文** ，是 Web 页面中盒模型布局的css渲染模式，是一个独立的渲染区域或者是一个隔离的独立容器。

BFC 可以阻止边距的重叠。我们可以在父级元素上添加BFC，从而可以避免与子级元素的 `margin` 重叠。

```html
<div class="box">
  <div class="child"></div>
  <div class="child"></div>
  <div class="child"></div>
</div>
```

```css
.box {
  background: green;
  overflow: hidden; /* 创建BFC */
  /*overflow: auto*/
  /*display: flow-root*/
}

.child {
  height: 100px;
  background: #f60;
  margin: 20px;
}
```

![WX20190803-154431.png](https://i.loli.net/2019/08/03/WsYOwLH6aESAk2X.png)

`display: flow-root` 是 CSS3 新出来的一个属性，用来创建一个无副作用的 BFC。将 `overflow` 的属性的值设置为 `auto` 或者 `hidden` 也会产生同样的效果，只不过有时候这俩属性值会带来一些副作用。

## 布局时的 margin 策略

由于我们知道上下 `margin`会发生重叠，所以我们在网站布局时，会采用单独给一边加 `margin` 值的策略，要么是 `margin-top` 要么是 `margin-bottom` 这两个在布局时最好是一个元素上别同时存在，当然指的是相邻的元素。那如果是父子级身上的 `margin` 重叠的情况下，我们最好还是采用上述清除 `margin` 的办法，当然现代浏览器的发展以及一些布局方法的更新，我们可以采用 `flex` 布局 和 `grid` 布局 抛除掉 `margin` 的使用。当前具体问题还得具体分析，我相信我们做的例子多了 会有更深刻的认识。

## 百分比 margin

在 CSS 中使用百分比的时候，它必须是某个元素的百分比，也就是说我们必须有一个参考元素。使用百分比设置的 `margin(或者padding)` 始终是父元素内联大小（水平写入模式下单宽度）的百分比。 

```html
<div class="wrapper">
  <div class="box">
    I have a margin of 10%.
  </div>
</div>
```

```css
 * {
   box-sizing: border-box;
 }
 .wrapper {
   border: 5px dotted black;
   width: 200px;
   height: 400px;
 }
 .box {
   background-color: rgb(55, 55, 110);
   color: white;
   padding: 20px;
   border-radius: .5em;
   margin: 10%;
 }
 body {
   font: 1.4em/1.3 "Gill Sans", "Gill Sans MT", Calibri, sans-serif;
   margin: 2em 3em;
 }
```

在线 [demo](https://jsbin.com/jajacam/1/edit?html,css,output)

## 后记

只是简单的介绍了下，平时遇到 `margin` 重叠的几种情况，以及我们该如何处理。还是那句话， CSS 博大精深，虽然容易入门但是后期的东西真的是让我们随时随地的去学习了，所以我们在平时的学习过程中，要记得多加练习，多多总结。

## 参考资料

[关于 CSS margin，你需要知道的一切](https://juejin.im/post/5d40dc46e51d4561cf15df4a#heading-6)