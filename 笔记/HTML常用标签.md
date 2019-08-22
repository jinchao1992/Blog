## 前言

最新的 `HTML5` 里标签大概有 110 个，但是如果让我们学完 110 个的话，对于大多数人来说可能还是比较困难的。工作中常用的也就那么几个，接下来我们介绍下几个常用的 HTML 标签。

## 常用标签

### a 标签

超链接元素，也可称为锚元素，可以通过此标签链接整个互联网，包括电子邮件、拨打电话、联通其他网页、文件以及同一页面内其他的位置，几乎互联网上的资源，都可以通过超链接访问。

1. 跳向其他 `URL` 点击之后浏览器会跳转到指定的网址，如下：

   ```html
   <a href="https://www.baidu.com">百度</a>
   ```

   点击如上的 「百度」字样即可跳转到我们经常访问的百度网页上，`href` 填写的是我们需要跳转的网页地址。

   `a` 标签不是一个单标签，里面可以放置任何内容，包括图片，文字等，如下：

   ```html
   <a href="https://www.baidu.com">
   	<img src="假如这是百度的logo.jpg">
   </a>
   ```

2. `<a>` 标签属性（常用）

   * `href` 链接指向的网址，值可以是一个 `URL` 或者锚点，如下代码：

     ```html
     <div class="box" style="border:1px solid #ddd; height: 8000px;">
       <a href="#demo">点击锚点</a>
     </div>
     <span id="demo">我是demo锚点</span>
     ```

     `#` 加上锚点名称，点击时会自动滚动到锚点所在位置。

     **注意：`href` 可以是本地的相对路径或者绝对路径**

     * `href` 链接指向邮件地址，使用 `mailto` 协议。用户点击后，浏览器会默认打开本机的邮件程序，可以向指定的地址发送邮件，如下：

       ```html
       <a href="mailto:jinchaophp@126.com">给我发发发！！！</a>
       ```

     * `href` 链接指向电话号码，使用 `tel` 协议，用户点击后，可以唤起电话，进行电话拨号，当然只是在移动端比较适合。如下：

       ```html
       <a href="tel:13312345678">拨打电话给我</a>
       ```

     * `href` 链接指向伪协议，主要作用，点击 `a` 链接后没有后续动作的操作，如下：

       ```html
       <a href="javascript:;">点击玩玩</a>
       ```

   * `target` 属性指定如何展开打开的链接。它可以指定的窗口打开，也可以在 `iframe` 打开

     ```html
     <a href="https://www.baidu.com" target="xxx">百度</a>
     <a href="https://www.qq.com" target="xxx">qq</a>
     ```

     上述代码中，两个链接都在名叫 `xxx` 的窗口打开。首先点击 `百度` 浏览器发现没有一个叫 `xxx` 的窗口，就会新建一个窗口，起名字为 `xxx` 。然后又点击 `qq` 由于已经有 `xxx` 窗口，就会取代之前打开的 `百度`，变为了 `qq`。

     `target` 属性有四个取值：

     * `_self` 当前窗口打开，默认写法；
     * `_blank` 新窗口打开；
     * `_parent` 上层窗口打开，主要用于 `iframe` 。如果当前窗口没有上层窗口，这个值就等于 `_self`；
     * `_top` 顶层窗口打开。如果当前窗口就是顶层窗口，那么写法跟 `_self` 一样；

   * `download` 属性表明当前链接用于下载，而不是跳转到其他网页，如下:

     ````html
     <a href="demo.txt" download>下载</a>
     ````

     **注意：`download` 属性只在链接与网址同源时，才会生效，链接必须与网址是同一个网站**

     `download` 设置了属性值，下载时文件名称就是规定的 `download`属性值:

     ```html
     <a href="demo.txt" download="demo.txt"></a>
     ```

### `img` 标签

 `img` 是图像标签，图片是互联网的重要组成部分，它可以让网页变的丰富多彩。一起来看看吧。

#### `<img>`

标签是单独使用的，没有闭合标签。也可以叫做单标签、空标签、可替换标签。如下：

   ```html
<img src="logo.jpg">
   ```

`src` 指定的是图片路径，可以是相对路径、绝对路径以及一个网址。

 `<img>` 标签默认是一个行内元素，但是与行内元素又不太一样，因为它可以设置宽高，如下：

```html
<p>Hello<img src="logo.jpg">World</p>
```

图片的默认大小是以图像原始大小为基准，就是说图像有多大在 `<img>` 标签里就显示多大。如果图片很大，又与文字处在同一行，那么图片将把当前行的行高撑开，并且图片的底边与文字的底边在同一条水平线上。但是不太符合审美，于是我通常采用如下写法：

```html
<p style="border: 1px solid red;">
    <img src="https://b-gold-cdn.xitu.io/v3/static/img/logo.a7995ad.svg" alt="logo" style="vertical-align: middle;"> 
    掘金一个很不错的网站
</p>
```

`<img>` 可以放在一个 `<a>` 标签的内部，可以把图片当作一个可以点击的链接，通常做法就是把 `logo` 图片放在一个 `<a>` 链接中，如下：

```html
<p style="border: 1px solid red;">
   <a href="https://juejin.im/timeline">
     <img src="https://b-gold-cdn.xitu.io/v3/static/img/logo.a7995ad.svg" alt="logo" style="vertical-align: middle;">
   </a>
    掘金一个很不错的网站
</p>
```

#### 属性

##### 1. alt 属性

`alt` 属性用来设定图片的文字说明。图片不显示时（路径错误、名称错误、加载失败等），会在图片位置上显示该文本。如下：

```html
<img src="logo.jpg" alt="logo图片">
```

##### 2. width 和 height 属性

图片默认大小是插入图像的大小，`width` 属性和 `height` 属性可以给图片设置宽高，单位是像素，也可设置百分比，如下：

```html
<img src="logo.jpg" alt="logo图片" width="100" height="200">
```

注意：如果我们设置了图片的宽高，浏览器会在网页上预留出空间大小，不管图片有没有加载成功。宽高也可以通过 `css` 设置，这也是工作中常用的写法。

`img` 标签特性，如果只是设置了宽高的其中一个，那么另一个会去自动缩放。所以我们在设置的时候只需设置一个属性即可。

#### 响应式

一句话，只需给图片加上 `max-width: 100%` 的样式。

#### 事件

* `onload` 图片加载完成之后调用，如下：

```javascript
oImg.onload = function() {
  console.log('加载完成！')
}
/*oImg 是当前图片*/
```

* `onerror` 图片加载失败之后调用，如下：

```javascript
oImg.onerror = function() {
  console.log('加载失败');
}
/*加载失败后，可以给图片一个默认的图片，这样对于用户来说就显得比较友好了*/
```

#### 支持的图片格式

* `JPEG`
* `GIF`
* `PNG`
* `SVG`
* `BMP`
* `base64`

### `table` 标签

表格布局是已经淘汰了的布局。但是表格对于平时的工作来说还是重要的，尤其是做后台管理系统来说，一个好的表格显的尤为重要。市面上有很多优秀的 `UI` 框架的表格做的非常不错，如，`element-ui` 、`Ant Design`、`iview` 等，它们的表格是非常值得学习的。

表格是由**表头**、**表体**、**表尾**构成的，三大块又是由`行` 和 `列` 构成，如下代码：

```html
<table border="1">
    <thead>
        <tr>
            <th>表头</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>内容</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td>表尾</td>
        </tr>
    </tfoot>
</table>
```

三者的前后顺序不会影响网页解析表格的前后顺序。

#### 1. `<table>` , `<caption>` 

* 如上代码所示，`table` 是一个块级容器标签，所有表格内容都要放在这个标签里。
* `<caption>` 总是 `<table>` 里的第一个子元素，表示表格的标题，是可选的。

```html
<table>
  <caption style="width: 200px;">表格标题</caption>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd;">1</td>
      <td style="border: 1px solid #ddd;">2</td>
    </tr>
  </tbody>
</table>
```

#### 2. `<thead>` 、`<tbody>` 、`<tfoot>`

三者是表格的三大模块，`<thead>` 与 `<tfoot>` 是可选的，其实 `<tbody>` 也可选，但是呢如果我们省略了 `<tbody>` 浏览器是会自动解析一个 `<tbody>` 所以在书写表格时，`<tbody>` 必须写。`<tbody>` 可以是多个，比如表格嵌套表格等。

#### 3. `<colgroup>` 、`<col>`

`<colgroup>` 是 `<table>` 的子元素排在第一位，除标题外，用来包含一组列的定义，`<col>` 是它的子元素，用来定义表格的一列，如下：

```html
<table>
  <colgroup>
    <col>
    <col>
    <col>
  </colgroup>
</table>
```

上述代码表示表格有三列内容，`<col>` 是一个单标签，也是一个空标签，不会产生子元素。它的主要作用是，除了声明表格的结构，还可以给表格附加单独的样式，如加宽度等，如下：

```html
<table border="1">
  <colgroup>
    <col width="100">
    <col width="200">
    <col widht="300">
  </colgroup>
  <tbody>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
```

针对于 `<col>` 设置的样式会对整个表格有效。

`<col>` 有一个 `span` 属性，属性值为正整数，默认为 `1` 。如果大于1，表示该列的宽度包含连续的多列，如下：

```html
<table border="1" width="100%">
  <colgroup>
    <col width="100">
    <col width="200">
    <col widht="300" span="2">
  </colgroup>
  <tbody>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
```

在实际数据中第三列和第四列公用一个宽度。

#### 4. `<tr>`、`<th>` 、`<td>`

`<tr>` 标签表示表格的一行，放在 `<thead>`、`<tbody>` 、`<tfoot>` 之中。

`<th>` 和 `<td>` 用来定义单元格，`<th>` 是标题单元格，默认是加粗的，`<td>` 是数据单元格，如下代码：

```html
<table border="1">
  <colgroup>
    <col width="100">
    <col width="120">
    <col width="120">
    <col width="120">
  </colgroup>
  <thead>
    <tr>
      <th>姓名</th>
      <th>语文</th>
      <th>数学</th>
      <th>英语</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>方一凡</th>
      <td>60</td>
      <td>80</td>
      <td>100</td>
    </tr>
    <tr>
      <th>林磊儿</th>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <th>乔英子</th>
      <td>99</td>
      <td>98</td>
      <td>100</td>
    </tr>
  </tbody>
</table>
```

#### 5. `<colspan>`属性、`<rowspan>`属性

单元格存在跨行和跨列的情况，可以通过 `<colspan>` 与 `<rowspan>` 属性设置，前者表示跨列，后者表示跨行，他们的值只能是正整数，默认为1，如下代码：

```html
<table border="1" width="500">
  <tbody>
    <tr>
      <td colspan="2" rowspan="2">A</td>
      <td>C</td>
    </tr>
    <tr>
      <td>C</td>
    </tr>
    <tr>
      <td>A</td>
      <td>B</td>
      <td>C</td>
    </tr>
  </tbody>
</table>
```

注意：去除边框合并使用 `css` 样式 `border-collapse: collapse;` 加在 `table` 标签上。

## 后记

`HTML` 重点标签还有 `form` 表单标签，它可以让前端跟后端相连接从而可以获取到真实的数据，这块内容比较多，需要单独拿出来，所以看后续的笔记喽。`HTML` 需要多多记忆，多多练习，一定记得用正确的标签做正确的布局。以此共勉，加油！！

## 参考链接

[阮一峰 网道教程 HTML 篇](https://wangdoc.com/html/)

