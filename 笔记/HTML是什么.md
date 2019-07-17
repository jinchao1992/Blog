HTML (英语：HyperText Markup Language)  超文本编辑语言，是整个网站的基石，所以学好 `HTML` 非常重要，并且我们要学会使用 **语义化**的标签来书写 `HTML` 标签，接下来我们来一一介绍 `HTML` 标签。

首先来了解下 `W3C` 和 `MDN`

### W3C 简介

#### w3c 是什么？

****

万维网联盟 (英语：**W**orld **W**ide **W**eb **C**onsortium，缩写是 **W3C** )，由李爵士 (蒂姆·伯纳斯-李) 于1994年创立。

####W3C 标准制定 

****

为解决网络中应用中不同平台、技术和开发者带来的不兼容问题，保障网络信息的顺利和完整流通，万维网制定了一系列标准并督促网络应用开发者和内容提供者遵循这些标准。W3C 制定的网络标准并非强制，只是推荐标准。现在浏览器厂商基本都是基于这些标准解析网页。

### MDN 简介

****

**MDN Web Docs** (旧称MozillaDeveloper Network、Mozilla Developer Center, 简称MDN) 是汇集众多网络技术开发文档的免费网站。

该项目于2005年，最初是由Mozilla(网景) 公司员工创建。

### HTML 简介

****

1. HTML 的版本
   1. HTML 4.01
   2. XHTML
   3. HTML5
   4. HTML5.1

2. 规范文档
   1. 由 W3C 写文档

3. DOCTYPE
   1. 用来选择文档类型
   2. 除了 HTML5 的 DOCTYPE，比较方便，其他请参考 <https://www.w3.org/QA/2002/04/valid-dtd-list.html>
   3. HTML5 的声明规范是 <!DOCTYPE html>

#### HTML 标签

注意：所有标签都需闭合如：<head></head>、<img />

****

##### 根元素

`<html>` 

##### 文档元数据

`<base>` 为页面上的所有链接规定默认的地址或者默认的目标，可以是相对的，也可以是绝对的，一份代码中只允许一个 `<base>` 标签，请看示例代码：来源：[w3school](<http://www.w3school.com.cn/tiy/t.asp?f=html_base_test>)

```html
<html>
<head>
<base href="http://www.w3school.com.cn/i/" />
<base target="_blank" />
</head>

<body>
<img src="eg_smile.gif" /><br />
<p>请注意，我们已经为图像规定了一个相对地址。由于我们已经在 head 部分规定了一个基准 URL，浏览器将在如下地址寻找图片：</p>
<p>"http://www.w3school.com.cn/i/eg_smile.gif"</p>

<br /><br />
<p><a href="http://www.w3school.com.cn">W3School</a></p>
<p>请注意，链接会在新窗口中打开，即使链接中没有 target="_blank" 属性。这是因为 base 元素的 target 属性已经被设置为 "_blank" 了。</p>

</body>
</html>
```

`head` 规定文档的配置信息，包括文档标题，文档样式和脚本等

`link` 常用于文档链接外部样式

`meta`  可以用于设置移动端视口信息，设置字符集等

`style` 放置 `css` 样式代码

`title` 定义文档的标题，显示在浏览器器窗口里

##### 分区根元素

`body` 所有主体标签全部都在 `body` 中

##### 内容分区

`address` 提供某个人或者某个组织的联系信息，通常都包含在此标签内

`article` 文档、页面、应用或网站中的独立结构

`aside` 表示和页面中其他没有任何关系的部分，可以单独拆分出来而不影响整体；

`footer` 页脚内容，比如网站友链 关于我们等

`header` 介绍性内容，包含导航 logo 等

`h1 - h6` 表示标题

`main` 主体部分，网站主体部分

`nav` 网页头部导航条，跳转二级页等

`section` 文档中的一个区域

##### 文本内容

`dd`  描述列表中的一个术语描述，只会在描述列表中出现，并且必须跟 `dt` 元素

`div`  容器元素没有任何定义，可以用 `class` 和 `id` 进行区分

`dl` 描述列表，通常用于 键-值对的表示

`dt` 描述列表中的键

`hr`  水平分割线，语义上的，并非是样式上的

`li` 列表里的条目

`ol` 有序列表

`p` 文本的一个段落

`pre` 预定义的格式文本

`ul` 无序列表

##### 内联文本语义

`a` 超链接，可以是 网页、文件、电话、邮件地址等

`b` 粗体元素，用于样式上的

`br`  强制换行

`code` 展示一段计算机代码

`em` 着重标识

`i` 斜体标识

`kbd` HTML 输入键盘字符

`mark` 表示凸显的文字信息，如搜索结果里的关键词等

`small` 字体变小

`span`  没有特别意义，通常用来表示行内元素

`strong` 文本十分重要，语义上的加粗

`time` 用来表示时间

##### 图片和多媒体元素

`area` 热点区域，可以关联一个超链接

`audio` 用于放置音频

`video` 用于放置视频

`img` 可以链接图像

`map` 与 `area` 结合使用，绘制热区

##### 脚本

`canvas` 通过脚本来绘制图形，实现动画等，一个画布

`noscript` 如果页面上的脚本类型不受支持或者当前浏览器关闭了脚本，则在 HTML 中使用 `noscript`中的替代内容

`script` 嵌入或者引用可执行脚本

##### 表格内容

`col` 定义表格中的列，并用于所有公共单元格上的公共语义，结合 `colgrpup` 使用

`colgroup` 表格列组

`table` 

`tbody`

`td` 一列

`tfoot`

`th`

`thead` 

`tr` 一行

#####  表单

`button` 按钮

`form` 表单文档区域，可以提交信息

`input` 表单输入，如 文本框 单选框 多选框等

`label` 表示用户界面某个元素的说明

`option`  结合 `select` 使用，下拉框

`textarea` 文本域，多行文本

****

### 什么是空标签

****

在 HTML 元素中，没有内容的就是 空元素，空元素通常都是单标签元素，HTML 包含以下的空元素：

* `<area>`
* `<base>`
* `<br>`
* `<col>`
* `<colgroup>`
* `<command>`
* `<embed>`
* `<hr>`
* `<img>`
* `<input>`
* `<keygen>`
* `<link>`
* `<meta>`
* `<param>`
* `<source>`
* `<track>`
* `<wbr>`

### 什么是可替换元素

****

在 css 中，可替换元素的展示效果不是由 css 来控制的。

css 可以影响可替换元素的位置，但是不会影响到可替换元素本身的内容。

典型的可替换元素：

`<iframe>`

`<video>`

`<embed>`

`<img>`

有些元素在特定情况下被视作可替换元素：

`<option>`

`<audio>`

`<canvas>`

`<object>`

`...`



### 重点介绍标签

****

#### iframe 标签

* `src` 属性，可以嵌入打开的地址，可以是相对的也可以是网址，如：`<iframe src="https://qq.com"></iframe>`

* `frameborder` 属性，设置为 `0` 可以去除 `iframe` 的默认样式, 如：`<ifrmae src="https://qq.com" frameborder="0"></iframe>`

* `name` 属性，如果设置一个 `name` 值，则可以结合 `a` 标签使用；如：

  ```html
  <iframe name="xxx" src="#" frameborder="0"></iframe>
  <a href="http://qq.com" target="xxx">在ifrme中打开qq.com</a>
  ```

#### a 标签

* `target` 属性
  * `_top` 在顶层窗口打开页面
  * `_blank` 在新窗口打开页面
  * _self 在本窗口打开页面
  * _parent  在父级窗口打开页面
* `download` 属性 提供下载，根据`http`响应提供的 `content-type` 属性可以直接下载文件，当值为 `application/octet-stream` 可以直接下载
* `href` 属性 链接到的地址，值可以为：
  * 网址，网址可以是 `http` 协议，或者当前添加一个相对路径，当前是什么协议就走什么协议
  * 可以发起请求，通常是 `get`
  * 可以是一个伪协议，如: `<a href="javascript:;"></a>`
  * 可以是一个查询字符串，如：`<a href="?name=aaa"></a>` 发起 `get` 请求
  * 可以是一个锚点，如：`<a href="#bbb"></a>`，单独写`#`的话会出现回到顶部效果；
  * 可以是一个空字符，如果是空字符串的话，则会刷新页面；

详情请查看 <https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a>

#### form 标签

* `form` 标签发起 `post`请求，可以使用 `method` 规定请求方式，默认是 `get` 提交
* `action` 设置请求地址，如：`<form action="./index2.html"></a>`
* `target` 窗口打开方式，与 超链接打开方式一致

##### form 子级

**重点：如果一个form表单中只有一个按钮（`button`）,那么会自动升级为提交按钮，form表单必须有提交按钮才可以提交，也就是`<input type="submit" value="提交">`**

更多请查看：<https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form>

#### table 标签

`table` 用于展示数据，注意：当 `thead tbody tfoot` 同时存在时，前后书写顺序不会影响展示效果；

详细属性请查看：<https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/table>

###  总结

****

HTML 常用的标签就是以上几种了，是不是很多，当然我们在平时的布局网页中，要尽量使用语义化的标签，要多参考大牛们写的网页，或者著名网站的源代码，这样在我们未来切图上才会积累起来更多的布局风格以及标签的用法，加油！

### 参考文档

****

[HTML元素参考](<https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element>)

[可替换元素](<https://developer.mozilla.org/zh-CN/docs/Web/CSS/Replaced_element>)

[HTML空标签](<https://developer.mozilla.org/zh-CN/docs/Glossary/%E7%A9%BA%E5%85%83%E7%B4%A0>)