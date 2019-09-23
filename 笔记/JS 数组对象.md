## 前言

数组其实是一种特殊的对象。`JS` 中并没有正真的数组，都是用对象去模拟的。

```js
typeof [1,2,3]; // "object" 数组的类型是一个对象
```

## 定义数组

### 常用创建数组

```js
let arr = [1, 2, 3];
let arr2 = new Array(1, 2, 3);
let arr3 = new Array(3); // 如果参数只有一个，则代表是数组的长度
```

### 转化创建的数组

```js
let str = '1, 2, 3';
let arr = str.split(','); // 通过 split 分割数组
let arr2 = Array.from('123'); // [1,2,3], es6 新增方法
```

#### Array.from

> `Array.from` 方法用于将两类对象转为真正的数组：类似数组的对象和可便利的对象。

```js
let arrayLike = {
  '0': 'a',
  '1': 'b',
  '2': 'c',
  '3': 'd',
  length: 4
};
let arr = Array.from(arrayLike); // ['a', 'b', 'c', 'd']
```

**类似数组（伪数组）**的对象，本质特点只有一点，就是必须有 `length` 属性。因此任何有 `length` 属性的对象，都可以通过 `Array.from` 方法转化为数组。

**重点：伪数组的原型链中并没有数组的原型**；

```html
<div class="wrap">
    <div class="demo"></div>
    <div class="demo"></div>
    <div class="demo"></div>
</div>
<script>
  let demos = document.querySelectorAll('.demo'); // DOM获取的数组就是伪数组
 demos.push(1); //  demos.push is not a function， 伪数组不能使用数组原型对象的属性
 let demosArray = Array.from(demos); // 通过 Aarray.from 就可以转换为数组
</script>
```

### 合并数组创建

```js
let arr1 = [1,2,3];
let arr2 = [4, 5, 6];
let arr3 = arr1.concat(arr2); 
console.log(arr3); // [1,2,3,4,5,6]
console.log(arr1); // [1, 2, 3] 
```

上述代码中可以得出，`concat` 不会改变原数组而是新生成数组；

### 截取数组创建

* `slice` 方法用于截取目标数组的一部分，返回一个新数组，原数组不变。

* `slice` 第一个参数为起始下标，第二个参数为终止下标，但不包含该下标。如果省略了第二个参数，则一直返回到原数组的最后一个元素。

* 当省略第二个参数后，如果第一个参数为 `0` 或者省略第一个参数，则返回的数组跟原数组一样，相当于一个原数组的拷贝（浅拷贝）。

* 如果 `slice` 的参数是负数，则表示从倒数位置开始计算。

  ```js
  let arr = [1,2,3,4,5,6];
  let arr2 = arr.slice(0); // [1,2,3,4,5,6]，相当于拷贝原数组
  let arr3 = arr.slice(0, 2); // [1, 2]
  let arr4 = arr.slice(1, 4); // [2, 3, 4]
  let arr5 = arr.slice(-2); // [5, 6]
  ```

* 如果第一个参数大于等于数组长度，或者第二个参数小于第一个参数，则返回空数组

  ```js
  let arr6 = arr.slice(7); // []
  let arr7 = arr.slice(1, 0); // []
  ```

* `slice` 可以将伪数组转换为真正的数组，与 `Array.from` 有同样的作用

  ```js
  Array.prototype.slice.call({0: 'a', 1: 'b', length: 2}); // ['a', 'b']
  ```

## 删除数组

* 数组是一种特殊的对象，对象可以用 `delete` 来删除属性，那么数组可以不可以呢？

```js
let arr = [1, 2, 3];
delete arr[0];
console.log(arr); // [empty, 2, 3] 第一个元素被删除但是数组的length并没有发生改变；
```

* 数组可以通过直接改变 `length` 删除数组（慎用）

```js
let arr = [1,2,3,4,5,6];
arr.length = 2;
console.log(arr); // [1, 2]
```

* 删除数组的第一个元素。

```js
let arr = [1,2,3,4,5,6];
arr.shift();
console.log(arr); // [2,3,4,5,6]
```

`shift` 方法用于删除数组的第一个元素，并返回该元素。**该方法会改变原数组**。

* 删除数组的最后一个元素。

```js
let arr = [1,2,3,4,5,6];
arr.pop();
console.log(arr); // [1,2,3,4,5]
```

`pop` 方法用于删除数组的最后一个元素，并返回该元素。**该方法会改变原数组。**

如果是空数组使用 `pop` 方法，不会报错，返回 `undefined`。

* 删除数组中间的元素

```js
let arr = [1,2,3,4,5,6];
arr.splice(1, 2); 
console.log(arr); // [1, 4, 5, 6]
```

第一个参数为删除的起始位置（从0开始），第二个参数是要删除的个数。如果有更多的参数，则表示是要插入到数组中的新元素，如下代码：

```js
let arr = [1,2,3,4,5,6];
arr.splice(1, 2, 222, 333);
console.log(arr); // [1, 222, 333, 4, 5, 6]
```

如果起始位置是负数，则表示是用倒数的位置开始删除：

```js
let arr = [1,2,3,4,5,6];
arr.splice(-2, 1);
console.log(arr); // [1, 2, 3, 4, 6]
```

如果只是想单纯的插入元素， `splice` 方法的第二个参数可以设为 `0`

```js
let arr = [1,2,3,4,5,6];
arr.splice(1, 0, 222);
console.log(arr); // [1, 222, 2, 3, 4, 5, 6]
```

## 查看数组元素

