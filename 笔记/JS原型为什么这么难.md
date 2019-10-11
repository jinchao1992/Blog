`JS` 原型作为 `JS` 世界中的三座大山之一，如果要搞明白的话着实是要费一些劲的。因为它存在了很多概念，这些概念又来回颠倒，所以导致我们傻傻分不清楚。那么这篇文章就是从新整理原型的知识，方便之后反复学习。因为 `JS` 是复杂的，就是需要反反复复的学习，并且需要结合实践来学习。话不多说，开始走进原型的世界。

##  三大知识点

### `JS`  中的唯一公式

```js
对象.__proto__ === 其构造函数.prototype
```

### 根公理

```js
Object.prototype 是所有对象的（直接或间接）原型
```

这是 `JS` 中的公理，就是在 `JS` 创建的时候就采用了这个说法。必须牢记于心。

### 函数公理

* **所有函数都是由 `Function` 构造的**；
* 如果结合第一个公式则会推出： `任何函数.__proto__ === Function.prototype`;
* 任何函数包括：`Object` /  `Array` / `Function`;

**结论：基于以上的三大知识点和基础知识就构成了整个的 `JS` 世界**。

## 带着问题来消化

* 以下代码中对象的原型是什么意思？

  ```js
  1. {name: 'jacky'} 的原型
  2. [1, 2, 3] 的原型
  3. Object 的原型
  ```

  解读：

  **`Object` 的原型是 `Object.__proto__`** 而并不是 `Object.prototype`，为什么？

  当在问到某一个对象 「的原型」时，约定指的就是 `对象.__proto__`。

* 如果 `[1, 2, 3].__proto__ === Array.prototype` 那么数组是一个对象，根据**根公理** `Object.prototype` 是所有对象的原型？那上述的代码就不应该成立吧？其实原因如下：
  * 原型分为直接原型和间接原型；
  * `Object.prototype` 是数组对象和函数对象的间接原型；是普通对象的直接原型
  * `Array.prototype` 的数组对象的直接原型；

* `Object.prototype` 是所有对象的原型；`Object` 是 `Function` 构造出来的；所以 `Function` 构造了 `Object.prototype` 得出推论， `Function` 才是万物之源啊？上述我们也说了根公理不容置疑，既然置疑了，就来 ”打破“ 置疑，原因如下：
  
  * `Object.prototype` 和 `Object.prototype` 对象的区别。`Object.prototype` 指向了一个地址，而这个地址里的属性组成了对象也就是 `Object.prototype` 对象。

## 从新认识JS世界

一个草草的内存图了解一下：

![](../images/41.png)

解析上图，来了解`JS` 世界的构造顺序：（#后跟的数字，解析为内存地址）

* 创建根对象 `#101` ,此时根对象没有名字；
* 创建 `函数的原型 #204`， 函数原型 `__proto__` 为 `#101`;
* 创建 `数组的原型 #404` ，数组原型 `__proto__` 为 `#101`;
* 创建 `Function #2004` 原型 `__proto__` 为 `#204`; 
* 让 `Function.prototype` 等于 `#204`;
* 用 `Function` 创建 `Object`;
* 让 `Object.prototype` 等于 `#101` ;
* 用 `Function` 创建 `Array`;
* 让 `Array.prototype` 等于 `#404`;
* 创建 `window` 对象；
* 用 `window` 的 `Object` 和  `Array` 属性分别为 `Function ` 创造出来的 `Object` 和 `Array` 命名。

### 用代码来理解

```js
let obj1 = new Object();
// 用 new 创建了对象 obj1
// new 会将 obj1 的原型 __proto__ 设置为 Object.prototype 也就是内存图上说到的 #101
```

`obj1` 代码演示截图：

![](../images/42.png)

```js
let arr1 = new Array();
// 用 new 创建了数组 arr1
// new 会将 arr1 的原型 __proto__ 设置为 Array.prototype, 也就是内存图上说到的 #404
```

`arr1` 代码演示截图：

<img src="../images/43.png" style="zoom:75%;" />

可以看出数组对象的间接的原型为 `Object.prototype`

```js
let f1 = new Function()
// 用new创建了函数 f1
// new 会将 f1 的原型 __proto__ 设置为 Function.prototype, 也就是内存图中的 #204
```

`f1` 代码演示截图：

![](../images/44.png)

通过上述的三段代码，可以看出函数、对象以及数组都是 new 出来的。`new` 的时候会将对象的 `__proto__` 自动的指向原型。

那么我们可以得到如下结论：

* 如果定义一个构造函数 `Person` ,函数里给 this 添加属性
* `Person` 自动创建 `prototype` 属性和对应的对象形成一个内存地址 （假如命名为：#502）；
* 给 `Person.prototype` #502上面加属性；
* 用 `new Persopn()` 创建对象 `p1`;
* `new` 会将 `p1` 的原型 `__proto__` 设为 `#502`;

如下图：

![](../images/45.png)

一张图了解 `JS` 原型的世界：

![](../images/46.png)

上图就是整个 `JS` 原型的构成。（此图非常之重要需要反复复习）