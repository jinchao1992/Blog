jQuery 是全世界使用最广泛的 JavaScript 库。虽然前端现在是「三大框架」的天下，但是不可否认，jQuery 曾经支撑了前端很多年，它使用之久，运用之广是其他框架无法企及的。所以，时至今日我们还是有必要学习一下 JQuery的一些用法，以及在这些用法中包含的一些思想。

## 神奇的选择器

jQuery 的主要思想和用法，就是 **选择某个网页元素，然后对其进行某种操作。**我一开始接触 jQuery时其实就是为了运用它的选择器，以及它所封装的 Ajax。

jQuery 的选择器就是将一个表达式，放进构造函数`jQuery()` 中（简写为$），然后就可以得到被选中的元素。当然我们获取到的是一个 `jQuery` 对象。

选择表达式可以是 CSS 选择器。意思就是可以是 标签、属性、类、ID 等等，只要是符合 CSS 选择器的都可以在里面写。（注意：jQuery获取到的都是一组元素）如下示例：

```js
$('#test') // 选择 ID 为 test的元素
$('div.myClass') // 选择 class 为 myClass 的 div 元素
$(document) // 选择整个文档元素
$(document.body) // 获取body
$('input[value="20"]') // 属性选择器，获取value值为 20 的 input元素
```

当然，也可以是 jQuery 的 特有的表达式，如下：

```js
$('div:last') // 选择网页中最后一个div元素
$('tr:odd') // 选取表格的奇数行
$('div:visible') // 选择可见的 div 元素
```

[更多](https://www.jquery123.com/category/selectors/jquery-selector-extensions/)

## 更改结果的 API

jQuery 设计思想的第二个方面，就是提供了各种强大的过滤器，对结果进行过滤，然后可以缩小我们的查找范围。如下：

```js
$('div').has('p'); // 选择包含p元素的div元素

$('div').not('.myClass'); // 选择class不等于myClass的div元素

$('div').filter('.myClass'); // 选择class等于myClass的div元素

$('div').first(); // 选择第1个div元素

$('div').eq(5); // 选择第6个div元素
```

还可以通过一些方法，找到自己附近的一些元素。如下：

```js
$('div').next('p') // 选择div元素后面的第一个p元素
$('div').parent() // 选择div的父元素，是直接父级
$('div').children() // 选择div的第一级子级
$('div').siblings() // 选择div的兄弟元素
```

## 强大的链式操作

jQuery 的设计思想三，可以选择到元素之后，对它进行链式操作，只要使用得当我们可以一直链下去。

```js
$('div').addClass('red').css('fontSize', '12px')
// 找到 div 元素添加一个 red 类选择器，然后再把它的 fontSize 改为 12px
```

这就是强大的链式操作，是 jQuery 的一个伟大发明。其中的原理，则是每一步的的操作最后，都会返回一个 jQuery 对象，这样我们就又可以进行下一步的调用，就会把每一步都链在一起了。

当然，我们也可以使用 `.end()` 方法可以使得链式向上返回一层。如下示例：

```js
$('#test').find('.child').addClass('red').end().addClass('blue')
// 找到id为test的元素下的所有class为child的元素，并添加一个red类，然后再返回到 test 再为 test 添加一个 blue 类
```

## 元素的取值和赋值

既然我们能获取元素，那么我们肯定也能给元素赋值。jQuery 设计思想第四个方面则是用同一个函数进行取值和赋值，用参数来判断到底是取值还是赋值。如下：

```js
$('div').html() // 获取div的HTML内容
$('div').html('hello') // 给div里增加HTML内容
```

常见的取值和赋值函数由以下几种：（通过字面意思即可理解）

* `html()` 
* `test()` 
* `attr()`
* `width()`
* `height()`
* `val()`

注意：如果我们是对一组元素进行的取值赋值操作，则取值时，取的是第一个元素，赋值时则是赋值的一组元素。（.text() 例外）

## 创建元素、插入元素、复制和删除元素

* **创建：** `$('标签名')`，例如： `$('<div id="div1"></div>');`。
* **插入：**
  1. append(); 把元素添加到指定的节点的里面的最后；或者 元素.appendTo(指定的节点)。
  2. prepend(); 把元素添加到指定的节点的里面的最前；或者 元素.prependTo(指定的节点)。
  3. before(); 把元素添加到指定的节点的前面；或者元素.insertBefore(指定的节点)。
  4. after(); 把元素添加到指定节点的后面；或者元素.insertAfter(指定的节点)。

注意：上述两者的区别在于：后续操作的是给谁操作？ 答案：谁的在前面就是操作的谁，第一种是指定的节点在前面，第二种是元素在前面，所以第一种后续的操作是操作的指定的节点，而第二种后续的操作是操作的元素。

* **删除：** `元素.remove()`。
* **复制：** `要复制的元素.clone()`

## 后续

以上只是对 jQuery的一个初步介绍，jQuery还有很多东西，比如 [工具方法](https://www.jquery123.com/category/utilities/) 、[事件操作](https://www.jquery123.com/category/events/) 、[动画](https://www.jquery123.com/category/effects/)等。如果要想掌握好 `jQuery` 还是需要从项目中来。当然前端发展到今天 jQuery 大家可能都不用了，但是我们还是可以学习一下它的一些思想，也利于我们更好的去掌握更加新的框架，万变不离其宗嘛，加油呀！

## 参考学习资料

* [jQuery 设计思想](http://www.ruanyifeng.com/blog/2011/07/jquery_fundamentals.html)
* [jQuery 中文文档](https://www.jquery123.com/)

