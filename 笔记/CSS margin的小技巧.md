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

