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

  对flex现在还不是很熟悉，很多属性还没有搞明白，所以等温习完再补充；

### 三栏布局(左中右)

