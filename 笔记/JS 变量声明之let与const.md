## 前言

变量声明的三种形式：`var` 、`let` 、`const` 。

```js
var a = 1;
let b = 2;
const c = 3;
```

`ES6` 采用的是 `let` 与 `const` 的声明方式。可以规避 `var` 声明带来的一些问题。

### 块级作用域

先来看一段代码：

```js
if (bFlag) {
  var a = 1;
}
console.log(a);
```

按照正常的逻辑来讲是，如果 `if` 条件成立才会创建 `a` 否则不创建，结果应该是报错才对；但是呢由于 `var` 存在变量提升，提升后代码相当于：

```js
var a;
if (bFlag) {
  a = 1;
}
console.log(a);
```

这样的话，即使条件不成立，结果还是会打印出一个 `undefined`。

所以为了规避这种问题，加强对变量生命周期的控制，`ECMAScript6` 引入了块级作用域。

块级作用域存在 **函数内部**与**块中也就是{}之中**。

### let 和 const

块级声明中声明的变量，在块级之外是无法访问的。

`let` 与 `const` 都是块级声明的一种。`let` 与 `const` 有如下特点：

#### 1. 不会被提升

```js
if (false){
  let a = 1;
}
console.log(1); // Uncaught ReferenceError: value is not defined
```

#### 2. 重复声明也会报错

```js
var a = 1;
let a = 2;// Uncaught SyntaxError: Identifier 'a' has already been declared
```

#### 3. 不绑定全局作用域

如果用 `var`声明一个变量时，会创建一个新的全局变量作为 `window` 的属性。

```js
var a = 1;
console.log(window.a); // 1
```

但是在 `let` 与 `const` 中不会发生这个操作。

```js
let b = 2;
console.log(window.b); // undefined
```

### 临时死区

临时死区(Temporal Dead Zone)，简写为 `TDZ`。

`let` 与 `const` 声明的变量不会提升到作用域的顶部，所以如果是在声明之前访问这些变量，则会导致报错：

```js
console.log(c); // Cannot access 'c' before initialization
let c = 1;
```

> 原因： `JavaScript` 引擎在扫描代码发现变量声明时，要么将它们提升到作用域顶部(遇到 `var` 声明)，要么将声明放在 `TDZ` 中(遇到 `let`和 `const` 声明)。访问 `TDZ`中的变量会触发运行时错误。只有执行过变量声明语句后，变量才会从 `TDZ` 中移出，然后方可访问。

```js
var value = 'global';

// 例子1
(function() {
    console.log(value);
    let value = 'local';
})()

// 例子2
{
    console.log(value);
    const value = 'local';
}
```

上述两个例子并不会打印全局的 `global` 而是会抛出一个错误 `Cannot access 'value' before initialization`。是因为存在暂存死区的缘故。

### 循环中的块级作用域

```js
var arr = [];
for (var i = 0; i < 3; i++) {
  arr[i] = function () {
    console.log(i);
  };
}
arr[0](); // 3
```

这是循环之后被赋值为3的缘故，如何解决呢？方案如下：

```js
var arr = [];
for (var i = 0; i < 3; i++) {
  arr[i] = (function (i) {
    return function() {
      console.log(i)
    }
  }(i));
}
arr[0](); // 0
```

`ES6` 解决方案：

```js
var arr = [];
for (let i = 0; i < 3; i++) {
  arr[i] = function () {
    console.log(i);
  };
}
arr[0](); // 0
```

如果 `for` 循环中采用了 `let` 声明变量，那么当前的 `i`只在本轮循环有效，所以每次循环的 `i` 都是一个新的变量。那么，如果每一轮循环的变量 `i` 都是重新声明的，那它如何知道上一轮循环的值呢？然后再根据上一轮的值计算出本轮的值？是因为在 `javascript` 引擎内部会记住上一轮循环的值，初始化本轮的变量 `i` 时，就在上一轮循环的基础上进行计算。

`for` 循环中，`let` 声明的变量，会在 `for (let i = 0; i < 3; i++)`圆括号内建立一个隐藏的作用域，而循环体内部是另外一个作用域。

```js
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc 
// abc
// abc
```

代码运行后，输出了3次 `abc`。表明了函数内部的变量 `i` 与循环变量的 `i`不在同一个作用域，都有着自己单独的作用域。 

### const

`const` 跟 `let` 基本上是一样的。但是 `const` 声明的是一个常量值，一旦声明，常量的值就不能改变。如果强行改变则会报错！

```js
const a = 1;
a = 4; //  Assignment to constant variable.
```

`const` 声明的变量不得改变值，意味着 ,`const` 一旦声明变量，就必须立即初始化，而不能留到之后再赋值。

```js
const b 
// Missing initializer in const declaration
```

#### const 本质

`const`的值不可变，指的是变量指向的值的内存地址保存的数据不得改变。对于简单类型的数据（数字、字符串、布尔），值就保存在变量指向的那个内存地址里，因此等于是常量不可变。但是由于复合类型的数据（主要是数组与对象），变量指向的内存地址，保存的只是一个指向实际数据的指针，`const` 只能保证这个指针是固定的也就是说指向一个固定的地址，至于它指向的数据结构是不是可变的，就完全不受控制了。

```js
const obj = {};
obj.name = 'Tom';
obj.age = 18;
obj = {}; // 这样就会报错了，因为这样是指向了另外一个地址了
```

换成数组也是一样的。

```js
const arr = [];
arr.push('hello'); // 可以执行
arr.length = 10; // 可执行
arr = []; // 报错
```

在开发时，默认使用 `const` ,只有当确定需要改变变量的值的时候才用 `let`。这是因为大部分变量的值在初始化后不应再改变。

## 参考资料

* [ES6系列值let和const](https://juejin.im/post/5b0238f66fb9a07aca7a74ba)

* [ES6入门之let和const](http://es6.ruanyifeng.com/#docs/let)

