## CSS 全解

如果我们把 `HTML` 理解为一栋房子的主体结构（毛坯房），那么 `CSS` 就是我们用来装修房子的材料，我们可以用 `CSS` 装修出各种华丽、大体、美观的房子（网页）。所以 `CSS` 对于前端开发者来说也是必不可缺的一项软技能了，学好 `CSS` 就显得尤为重要了。废话不多说一起来看看 `CSS` 的一些重要知识点吧。

### CSS 盒模型

`CSS` 盒模型是 `CSS` 的基础，也是我们在工作中会经常遗忘的点，基本上面试时都会被提及，那么什么是 `CSS` 盒模型呢？一起来看。

我们知道网页是由 `html` 标签组成的，我们可以认为每个 `html` 标签都是一个小方块，小方块里面又套着小方块，就像是盒子一层层包裹一样，这就是所谓的盒模型了。也可以理解一个小模块就具备一个小盒模型。

#### 盒模型的组成

盒模型是由外边距(margin)、边框（border）、内边距（padding）、内容（content）组成的，如下图：

![item1](../images/item1.png)

上图就是一个基本的 `CSS` 盒模型的构成。

盒模型又可分为  **内容盒模型(content-box)** 和 **边框盒模型(border-box)** 。其中内容盒模型是浏览器默认的解析的盒模型。它们有什么区别呢？

1. content-box 宽度组成 , 如下代码：

```css
.content-box {
  width: 100px;
  height: 100px;
  padding: 20px;
  border: 5px solid #f00;
  margin: 20px;
  box-sizing: content-box;
}
/*浏览器解析出来的宽度为 width + padding + border */
```

图解上述代码：

![item2](../images/item2.png)

2. border-box 宽度组成，如下代码：

```css
.content-box {
  width: 100px;
  height: 100px;
  padding: 20px;
  border: 5px solid #f00;
  margin: 20px;
  box-sizing: border-box;
}
/*浏览器解析出来的宽度为，宽度写了多少就是多少，padding 与 border 会解析在写的width里 */
```

图解上述代码

![item3](../images/item3.png)

高度跟宽度原理同理，只需要把左右换为上下即可。两个盒子模型的切换可以通过 `css` 属性 `box-sizing` 来修改。

**注意：盒子模型的宽度是由 `padding` 、`border`、`content(内容)` 构成的，其并不包含 `margin`大小。但是 `css` 盒模型是由 `content(内容)`、`padding(内边距)`、`border（边框）`、`margin(外边距)`组成的 ；**

在现代布局中，通常是会把 `box-sizing` 设置为 `border-box` 方便我们进行宽度计算这样不会造成宽度错乱问题。

### CSS margin合并问题

关于 `margin` 合并问题可以参照我写的这篇文章 [css-margin布局技巧]([https://jinchao1992.github.io/post/css-margin-%E5%B8%83%E5%B1%80%E6%8A%80%E5%B7%A7/](https://jinchao1992.github.io/post/css-margin-布局技巧/)) 这里就不列举了！

### 页面文档流

文档流（英文名：Normal Flow）简单来说就是文档流动方向。内联元素从左向右流动，走到行尾进行折行继续走，块级元素从上到下排列，一行只有一个块级元素。如下图：

![item4](../images/item4.png)

可以看到内联元素遇到行尾之后会自动折行，块级元素不管设置宽度多少是一定会独占一行的。

#### 模块元素

* `inline` 内联元素，从左向右流动，会自动折行，如果一行放不下的话会把行尾的内联元素切分，如上图所示。

* `block` 块元素，从上到下流动，不管宽度多大只要是块就会一直独占一行。

* `inline-block` 内联块元素，从左到右流动，但是又具备块级元素的特性。如果在一行的行尾放不下时，元素会整体下移。如下图：

  ![item5](../images/item5.png)

如上图所示，我们把 `span` 变为了内联块，在行尾时第6个 `span` 是换行显示的。

**注意：HTML模块并不是只有这三种，只是我们可以通过修改css样式变为这三种模块； 内联元素里不能加入块级元素**

#### 宽度

* 内联元素的宽度是由元素本身里内联元素的宽决定的，不能用 `width` 设置；
* 块级元素的默认宽度是 `auto`；表示能有多宽占多宽，块级元素宽度最好别写 `100%`；
* 内联块元素的宽度跟内联元素一样，但是可以使用 `width` 进行设置；

#### 高度

* 内联元素的高度是由 `line-height` 行高间接确定，跟 `height` 无关，跟字体有关系；
* 块级元素的高度是由里面所有**文档流元素**的高度总和决定的；一定注意是文档流元素，因为一个一旦脱离文档流就会造成高度塌陷。也可以通过 `height` 设置高度。
* 内联块跟块级元素一样，可以设置高度；

#### 文档溢出（overflow）

* overflow: visible; 默认写法 超出文档内容默认显示
* overflow: hidden; 超出文档内容隐藏
* overflow: scroll; 超出部分用滚动条显示，但是如果不超出也会显示滚动条
* overflow: auto; 超出部分自动选择滚动条

注意：如果有滚动条，内联元素默认在第一屏显示（特指overflow-x 方向）`overflow` 可以分为 `overflow-x` 与 `overflow-y`。

### 脱离文档流

