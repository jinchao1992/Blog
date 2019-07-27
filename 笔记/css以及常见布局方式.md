## CSS是什么？

CSS，层叠样式表(英语：**C**ascading **S**tyle **S**heets)，是一种用来为结构化文档 (如：HTML文档) 添加样式 (字体、颜色、间距等) 的计算机语言，由 W3C 定义和维护。当前最新的版本是 CSS2.1，为W3C的推荐标准。CSS3(2011年) 已经被现代浏览器支持。

### CSS发展历史

1. 1994年哈肯.维姆.莱提出了CSS的最初建议。伯特.波斯加入一起设计CSS。
2. 1997年初，W3C内组织了专门管CSS的工作组，其负责人是克里斯.里雷。
3. 1998年5月W3C发表了CSS2，CSS2.1修改了CSS2中的一些错误，删除了其中不被支持的内容和增加了一些已有浏览器的扩展内容。
4. 从2001年开始CSS被分为了多个单独的模块，统称为CSS3。这些模块有：
   * CSS 选择器 level  3
   * CSS 媒体查询 level 3
   * CSS Color level 3
   * ……

周边工具

* Less CSS 一种简化、功能更多的 CSS 语言
* SASS 一种简化、功能更多的 CSS 语言
* Post CSS 一种 CSS 处理程序

## CSS 学习资源

1. MDN 查询关键字，遇到不会的 CSS 属性就去查阅MDN
2. [CSS Tricks](https://css-tricks.com/)，可以根据属性搜索很多好看的CSS效果；
3. [Google: 阮一峰 css](https://www.google.com/search?q=阮一峰+css) 
4. [张鑫旭的 240 多篇 CSS 博客](http://www.zhangxinxu.com/wordpress/category/css/page/25/) 
5. [Codrops 炫酷 CSS 效果](https://tympanus.net/codrops/category/playground/)
6. [CSS揭秘](http://www.ituring.com.cn/book/1695)
7. [CSS 2.1 中文 spec](http://cndevdocs.com/)
8. Google 搜索 CSS Generator ，可以生成css样式

## CSS 开始写

**引入 CSS 的几种方式**

* 行间 `<div style="color:red;"></div>`
* 内联 `<style>div{color: red}</style>`
* 外部 `<link href="index.css" rel="stylesheet">`
* `import引入` `@import url(./index.css)`

**布局小技巧**

* `HTML` 除 `div` 与 `span` 外，都有默认样式，所以在布局之前我们通常会清除一些标签的默认样式，如：

  ```css
  body,p,h1,h2,dl,dt {
    margin: 0;
  }
  ul,ol {
    list-style: none;
    padding: 0;
    margin: 0
  }
  /* 通常不建议这么写 *{margin: 0; margin: 0} */
  ```

* 清除浮动，如子级用浮动布局，则**需给父级**添加浮动清除代码，代码通常写法，给父级添加 `clearfix` 类选择器：

  ```css
  .clearfix::after{
    content: '';
    clear: both;
    display: block;
  }
  ```

* `chrome` 浏览器默认字体大小 16px，默认间距 8px

* 一个元素的高度是由其内部 `文档流` 的高度总和决定的

* `文档流`就是文档内元素的流动方向

  * 内联元素从左往右流动，如果流动遇到阻碍则换行继续，从左向右流动

  * 块级元素，每一个块级元素独占一行，从上往下流动

  * CSS 属性值 `word-break:break-all`， 可以将单词打断点，会把整个词分开断点，如下代码预览：

    https://jsbin.com/ketaxum/2/edit?html,css,output

  * CSS `float:left; positon:fixed; position:absolute` 都能使元素脱离文档流

* 为什么内联元素中间会有一个空格的距离，因为内联元素之间如果有换行符或者空格存在，浏览器会解析为一个空格
* 每一个字体都有一个建议行高，默认的 `line-heigth` 由字体设计师决定
* CSS 中 `width` 的默认值是 `auto`
* `box-sizing:content-box` 的 `width` 不包含 `padding` 与 `border`，元素默认
* `box-sizing:border-box` 的 `width` 包含 `padding` 与 `border`
* 在布局时，尽量不要给元素定义宽度和高度，会有很多不确定性，妙用 `max-width` 与 `min-width` 

## CSS 经典布局方式

### 两栏布局

* 方法一：浮动布局

  ```html
  <div class="aside"></div>
  <div class="main"></div>
  ```

  ```css
  div {
    height: 500px;
  }
  .aside {
    width: 300px;
    background-color: #f60;
    float: left;
  }
  .main {
    background-color: green;
    margin-left: 300px;
  }
  ```

  左侧栏固定宽度向左浮动，右侧主要内容用 `margin-left` 留出左侧栏的宽度，默认宽度是`auto`, 自动填满剩下宽度  [demo](https://jsbin.com/ketaxum/4/edit?html,css,output)

  右侧固定宽度，左侧自适应则是同理，只要将固定栏右浮动，使用 `margin-right` 即可，

  ```css
  div {
    height: 500px;
  }
  .aside {
    width: 300px;
    background-color: #f60;
    float: right;
  }
  .main {
    background-color: green;
    margin-right: 300px;
  }
  ```

* 方法二：浮动布局 + 负外边距

  ```html
  <div class="clearfix">
    <div class="aside">
    </div>
    <div class="main">
      <div class="content"></div>
    </div>
  </div>
  ```

  ```css
  .clearfix::after {
    content: '';
    display: block;
    clear: both;
  }
  div {
    height: 500px;
  }
  .aside {
    width: 300px;
    float: left;
    margin-right: -100%;
    background-color: #f60;
  }
  .main {
    width: 100%;
    float: left;
  }
  .main .content {
    background-color: green;
    margin-left: 300px;
  }
  ```

  左侧固定栏指定一个右侧的100%的负边距，为整个屏幕的宽度，这就使得main的最左侧与屏幕的最左侧对齐，此时的main的宽度是100%，因此需要其子内容content指定一个左侧的外边距空出左侧栏的位置，即左侧栏的宽度300px；适应一侧宽度为100%的布局 [demo](https://jsbin.com/ketaxum/8/edit?html,css,output)

* 方法三：绝对定位

  ```html
  <div class="box">
    <div class="aside">
    </div>
    <div class="main">
    </div>
  </div>
  ```

  ```css
  body {
    margin: 0;
  }
  div {
    height: 500px;
  }
  .aside {
    width: 300px;
    position: absolute;
    left: 0;
    top: 0;
    background-color: #f60;
  }
  .main {
    background-color: green;
    margin-left: 300px;
  }
  ```

  采用绝对定位，根据绝对定位脱离文档流的特性，[demo](https://jsbin.com/ketaxum/edit?html,css,output)

* 方法四： flex 布局

  ```html
  <div class="cainter">
    <div class="aside"></div>
    <div class="main"></div>
  </div>
  ```

  ```css
  div {
    height: 500px;
  }
  .cainter {
    display: flex;
  }
  .aside {
    flex: 0 0 300px;
    background-color: #f60;
  }
  .main {
    flex: 1 1;
    background-color: green;
  }
  ```

  弹性盒模型的方式是最简单的，如果不考虑浏览器兼容性的话，则可以使用此方法 [demo](https://jsbin.com/ketaxum/13/edit?html,css,output)

### 三栏布局(左中右)

**三栏布局的特点：两边定宽，然后中间的 `width` 是 `auto`, 可以自适应内容**

* 方法一：用绝对定位的方法

  原理则是，左侧和右侧布局用绝对定位分别定位在左侧和右侧，中间的布局则用 `margin-left`  和 `margin-right` 空出左右栏位置来，[demo](https://jsbin.com/ketaxum/14/edit?html,css,output)

```html
<div class="cainter">
  <div class="left"></div>
  <div class="center"></div>
  <div class="right"></div>
</div>
```

```css
div {
  height: 500px;
}
.cainter {
  position: relative;
}
.left {
  position: absolute;
  top: 0;
  left: 0;
  width: 100px;
  background: red;
}
.right {
  position: absolute;
  top: 0;
  right: 0;
  width: 100px;
  background: green;
}
.center {
  background: yellow;
  margin-left: 100px;
  margin-right: 100px;
}
```

由于采用了绝对定位，所以在布局上三者的位置可以随意更换；

* 方法二 使用 `float` 属性

  >  左右两栏使用 `float` 属性，中间栏使用 `margin` 属性撑开；[demo](https://jsbin.com/ketaxum/18/edit?html,css,output)

  ```html
  <div class="cainter clearfix">
    <div class="left"></div>
    <div class="right"></div>
    <div class="center"></div>
  </div>
  ```

  ```css
  .clearfix::after {
    content: '';
    display: block;
    clear: both;
  }
  div {
    height: 500px;
  }
  .cainter {
    position: relative;
  }
  .left {
    width: 100px;
    background: red;
    float: left;
  }
  .right {
    width: 100px;
    background: green;
    float: right;
  }
  .center {
    background: yellow;
    margin-left: 100px;
    margin-right: 100px;
  }
  ```

  > 缺点：1. 当宽度小于左右两边宽度之和时，右侧栏会被挤下去；2. html结构不正确

* 方法三，浮动 + 负外边距 (双飞翼布局)

  * 三栏都采用左浮动
  * 中间栏也是左浮动，默认情况下由于前面中间栏 占据了 100% 的宽度，因此左侧是在另起一行显示，为左侧栏设置 `margin-left: -100%;` 即整个屏幕的宽度100%，这就令左侧栏布局到中间栏的最左侧
  * 右侧栏也是左浮动，此时默认的情况下也是在中间栏的下一行，同样利用 `margin-left: -300px;`  `300px` 为右侧模块宽度，使其到上一行最右侧位置
  * 中间栏内容部分则需要利用分别等于左右栏宽度外边距来空出它们的位置

  ```html
  <div class="cainter clearfix">
    <div class="center">
      <div class="main"></div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
  </div>
  ```

  ```css
  .clearfix::after {
    content: '';
    display: block;
    clear: both;
  }
  div {
    height: 500px;
  }
  .cainter {
    position: relative;
  }
  .center {
    float: left;
    width: 100%;
    background: yellow;
  }
  .left {
    float: left;
    width: 200px;
    margin-left: -100%;
    background: green;
  }
  .right {
    float: left;
    width: 300px;
    background: red;
    margin-left: -300px;
  }
  .main {
    margin-left: 200px;
    margin-right: 300px;
  }
  ```

  > 这种方法的好处就是主体内容可以在前面优先加载；缺点：结构不正确，且多了一层标签 [demo](https://jsbin.com/ketaxum/19/edit?html,css,output)

* 方法四： flex布局

  ```html
  <div class="container">
    <div class="left"></div>
    <div class="middle"></div>
    <div class="right"></div>
  </div>
  ```

  ```css
  div {
    height: 500px;
  }
  .container {
    width: 100%;
    display: flex;
  }
  
  .left {
    width: 100px;
    background: green;
  }
  .middle {
    width: 100%;
    background: yellow;
  }
  .right {
    width: 100px;
    background: red;
  }
  ```

  > 不考虑兼容性的话，最靠谱的一种方式 [demo](https://jsbin.com/lerozex/2/edit?html,css,output)



## CSS 垂直居中，水平居中方式

### 一、水平居中

#### 1. 行内元素水平居中

**`text-align:center;`** 可以实现块级元素内部的行内元素的的水平居中，此方法只对 `display:inline-block display:inlie; display:inline-table 和 display:inline-flex 元素水平居中有效`，并且是给父级设置样式：

```css
.parent {
  text-align: center;
}
```

> 小技巧：如果是一个块级元素，我们可以先改变为 `display:inline-block;` 就可以使用 `text-align:center;`

#### 2. 块级元素的水平居中

* 将该元素的左右外边距设置为 `auto` , 此方法必须是块级元素有宽度才可以，否则不起作用；

  ```css
  .box {
    width: 100px; // 宽度属性是必须的
    margin: 0 auto;
  }
  ```

* 使用 `table + margin` 先将子元素设置为块级表格显示，再将其居中，`display:table` 在表现上类似 `block` 元素，但是宽度为内容宽;

  ```html
  <div class="parent">
    <div class="child">Demo</div>
  </div>
  <style>
  	.parent {
      border: 1px solid #ddd;
      height: 100px;
    }
    .child {
      display: table;
      margin: 0 auto;
      background: red;
    }
  </style>
  ```

* 使用 `absolute + transform`  先将父元素设置为相对定位，然后子元素设置为绝对定位，`left` 值设置为 50% , 然后通过移动子元素的一半宽度即可

  ```html
  <div class="parent">
    <div class="child">Demo</div>
  </div>
  <style>
  	.parent {
      border: 1px solid #ddd;
      height: 100px;
      position: relative;
    }
    .child {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
    }
  </style>
  ```

  `transform` 属于 `css3` 内容，存在兼容性问题，高版本浏览器需加上前缀

* 使用 flex + justify-content 给父级加

  ```html
  <div class="parent">
    <div class="child">Demo</div>
  </div>
  <style>
  	.parent {
      display: flex;
      justify-content: center;
    }
  </style>
  ```

* 使用flex+margin，通过flex将父容器设置为 `flex` 布局，再设置子元素居中

  ```html
  <div class="parent">
    <div class="child">Demo</div>
  </div>
  <style>
  	.parent {
      display: flex;
    }
    .child {
      margin: 0 auto;
    }
  </style>
  ```

#### 3. 多块级元素水平居中

* 利用弹性布局(flex)，实现水平居中，其中 `justify-content` 用于设置弹性盒模型子元素在主轴(默认横屏)方向上的对齐方式,

  ```html
  <div class="parent">
    <div class="child">demo1</div>
    <div class="child">demo2</div>
    <div class="child">demo3</div>
  </div>
  <style>
  	.parent {
      border: 1px solid #ddd;
      height: 100px;
      display: flex;
      justify-content: center;
    }
    .child {
      background: red;
      padding: 10px;
      margin: 10px;
    }
  </style>
  ```

  [demo](https://jsbin.com/luhokeh/3/edit?html,css,output)

* 利用inline-block ，子级全部设置为 `display:inline-block;` 父级设置 `text-align:center;`

  ```html
  <div class="parent">
    <div class="child">demo1</div>
    <div class="child">demo2</div>
    <div class="child">demo3</div>
  </div>
  <style>
  	.parent {
      border: 1px solid #ddd;
      height: 100px;
      text-align: center;
    }
    .child {
      background: red;
      padding: 10px;
      margin: 10px;
      display: inline-block;
    }
  </style>
  ```

  [demo](https://jsbin.com/luhokeh/11/edit?html,css,output)

#### 4. 浮动元素水平居中

* 定宽的浮动元素，通过设置子元素 `relative + 负margin`，原理如图：

  ![gitHub](https://camo.githubusercontent.com/bc627dc8ad85de3662ce91ba23e3eec78d69c164/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f31302f31332f313636366466333831323761343830623f773d36353626683d33373226663d706e6726733d3134383336) 

 [demo](https://jsbin.com/luhokeh/12/edit?html,css,output)  **注意：样式设置在浮动元素的本身**

* 不定宽的浮动元素，原理如图：

  ![](https://camo.githubusercontent.com/a7d9c24ab2a0ad79aad1b8184711fd1e99d41c61/68747470733a2f2f757365722d676f6c642d63646e2e786974752e696f2f323031382f31302f31322f313636363930303334623338373665663f773d39333226683d32343526663d706e6726733d3235313630)

[demo](https://jsbin.com/luhokeh/20/edit?html,css,output)

* 通用办法 `flex` 布局

  ```html
  <div class="parent">
    <span class="chlid">水平居中</span>
  </div>
  <style>
  	.parent {
      display:flex;
      justify-content:center;
    }
    .chlid{
      float: left;
      width: 200px;// 有无宽度不影响居中
    }
  </style>
  ```

#### 5. 绝对定位元素水平居中

通过子元素绝对定位，加上 `marging:0 auto` 实现；

[demo](https://jsbin.com/luhokeh/22/edit?html,css,output)

### 垂直居中

#### 1. 单行内联元素重置居中

```html
<div class="box">
  <span>单行文本元素垂直居中</span>
</div>
<style>
	.box {
    height: 100px;
    line-height: 100px;
    border: 1px solid #ddd;
  }
</style>
```

#### 2. 多行内联元素垂直居中

* 利用 flex 布局，实现垂直居中，其中 `flex-direction: column;` 定义主轴方向为纵向

  ```html
  <div class="parent">
    <p>多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中，    
      多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中，    
      多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中</p>
  </div>
  <style>
    .parent { 
      height: 140px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      border: 2px solid #ddd;
    }
  </style>
  ```

  [demo](https://jsbin.com/kojipaq/1/edit?html,css,output)

* 利用表格布局， `vertical-align: middle` 可以实现子元素的垂直居中

  ```html
  <div class="parent"> 
  	<p>多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中，    
      多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中，    
      多行文本实现居中，多行文本实现居中，多行文本实现居中，多行文本实现居中</p>
  </div>
  <style>
    .parent { 
      height: 140px;
      border: 2px solid #ddd;
      display: table;
    }
    .child {
      display: table-cell;
      vertical-align: middle;
    }
  </style>
  ```

#### 3. 块级元素垂直居中

* 使用 `absolute + 负 maring`  前提是已知模块的宽度和高度, 与绝对定位的水平居中遥相呼应，是平时用的多的布局方式；

  ```html
  <div class="parent">
      <div class="child">固定高度的块级元素垂直居中。</div>
  </div>
  <style>
  	.parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      height: 100px;
      margin-top: -50px;
    }
  </style>
  ```

* 使用 `absolute + transform` 此方法适用于高度和宽度未知时

  ```html
  <div class="parent">
      <div class="child">固定高度的块级元素垂直居中。</div>
  </div>
  <style>
  	.parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
    }
  </style>
  ```

* 使用 `flex + alig-items` 与做水平居中的 `flex + justify-content:center;` 对应，是目前布局经常用的，有兼容性问题；

  ```html
  <div class="parent">
     <div class="child">未知高度的块级元素垂直居中。</div>
  </div>
  <style>
   .parent {
     display:flex;
     align-items:center;
   }
  </style>
  ```

### 三、水平垂直居中

常用的适合没有兼容问题或者没有定宽高的布局

#### 方法1：绝对定位与负边距实现 (已知宽高)

```html
<div id='container'>
  <div id='center' style="width: 100px;height: 100px;background-color: #666">center</div>
</div>
<style>
  #container {
    position: relative;
  }
  #center {
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -50px 0 0 -50px;
  }
</style>
```

#### 方法2： 绝对定位与 margin:auto (已知宽高)

```html
<div id='container'>
  <div id='center' style="width: 100px;height: 100px;background-color: #666">center</div>
</div>
<style>
  #container {
    position: relative;
  }
  #center {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto; // 此处是重要写法
  }
</style>
```

#### 方法3： 绝对定位 + CSS3 (未知宽高) 不考虑兼容性的话 此方法非常舒服

```html
<div id='container'>
  <div id='center' style="background-color: #666">center</div>
</div>
<style>
  #container {
    position: relative;
  }
  #center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate3d(-50%, -50%, 0);
  }
</style>
```

#### 方法4： flex 布局 移动端常用，pc不考虑兼容可用

```html
<div id='container'>
  <div id='center' style="width: 100px;height: 100px;background-color: #666">center</div>
</div>
<style>
  #container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
```

## 后记

以上就是总结的css 常见布局的一些方法，以及水平居中的一些主要方法，以后会学习到 `grid` 布局，以及经常用的 css 小技巧，都统一会补充到文章里，或者其他文章中，也是站在一些前辈(大神)的基础上总结的一些技巧，以后多向大神们学习了！加油！

 ## 参考文章

[如何居中一个元素(终结版)](https://github.com/ljianshu/Blog/issues/29)

[CSS 两栏布局，三栏布局](https://blog.csdn.net/crystal6918/article/details/55224670)

[CSS 布局说](https://segmentfault.com/a/1190000011358507#articleHeader6)