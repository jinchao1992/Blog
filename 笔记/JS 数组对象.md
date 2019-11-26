数组其实是一种特殊的对象。`JS` 中并没有正真的数组，都是用对象去模拟的。如果是前后端分离开发，那么对于数组的处理，将会影响到对数据处理的方方面面，所以对于数组的处理以及把控就显得至关重要啦！

```js
typeof [1,2,3]; // "object" 数组的类型是一个对象
```

## 定义数组

可以通过以下方法进行数组的创建。

### 常用方法创建数组：

```js
let arr = [1, 2, 3];
let arr2 = new Array(1, 2, 3);
let arr3 = new Array(3); // 如果参数只有一个，则代表是数组的长度
```
### 通过转化创建的数组：

```js
let str = '1, 2, 3';
let arr = str.split(','); // 通过 split 分割数组
let arr2 = Array.from('123'); // [1,2,3], es6 新增方法
```

#### Array.from是什么？

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
### 通过合并数组创建新的数组：

```js
let arr1 = [1,2,3];
let arr2 = [4, 5, 6];
let arr3 = arr1.concat(arr2); 
console.log(arr3); // [1,2,3,4,5,6]
console.log(arr1); // [1, 2, 3] 
```

上述代码中可以得出，`concat` 不会改变原数组而是新生成数组；

### 通过截取数组元素创建：

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

* 使用 `for` 循环（常见）

  ```js
  let arr = [1, 2, 3, 4, 5]
  for (let i = 0; i < arr.length; i++) {
    console.log(`${i}: ${arr[i]}`);
  }
  ```

* 使用 `forEach` 循环

  ```js
  let arr = [1, 2, 3, 4, 5]
  arr.forEach((item, index) => {
    console.log(`${index} : ${item}`);
  });
  ```

  使用 `for` 循环模拟 `forEach`

  ```js
  function forEach(array, fn) {
    for(let i = 0; i < array.length; i++) {
      fn(array[i], i, array);
    }
  }
  let arr = [1,2,3,4];
  forEach(arr, function(item, index, arr) {
     console.log(item); // 1,2,3,4
     console.log(index); // 0,1,2,3
     console.log(arr); // [1,2,3,4]
  });
  ```

  **注意：在使用 `forEach` 时，不能使用 `break` 与 `continue`**

### 查看数组单个属性

```js
let arr = [1,2,3,4];
arr[0]; // 1, 这里的下标 0 是字符串， js 会自动转换为字符串
arr['1']; // 2
arr[arr.length]; // undefined
arr[-1]; // undefined
```

注意：如果下标小于0，或者大于等于数组的长度，则返回 `undefined` 。

* `indexOf()` 与 `lastIndexOf()`  都是用于查找元素在数组中出现的位置，如果找不到则返回 `-1` 。`indexOf()` 方法返回的是元素第一次出现的位置，`lastIndexOf()`  返回的是元素最后一次出现的位置。

  ```js
  let arr = ['a', 'b', 'c'];
  arr.indexOf('b'); // 1
  arr.indexOf('d'); // -1
  let arr2 = [1, 2, 3, 1];
  arr2.lastIndexOf(1); // 3
  arr2.lastIndexOf(9); // -1
  ```

* `find()` 方法返回数组中满足提供的测试函数的**第一个**元素的值。否则返回 `undefined`。

  ```js
  let arr = [5, 12, 8, 130, 45, 44];
  arr.find(item => item % 5 === 0); // 5
  ```

* `findIndex()` 方法返回数组中满足提供测试函数的第一个元素的**索引**。否则返回 -1。

  ```js
  let arr = [5, 12, 8, 130, 45, 44];
  arr.findIndex(item => item % 5 === 0); // 0
  ```

* `includes()` 方法用于在查找数组是否包含该元素，返回一个布尔值，包含返回 `true` ，不包含则返回 `false`。包含两个参数，第一个参数是要查找的元素，第二个参数为数组开始下标，默认为 `0`。

  ```js
  const arr = [1, 2, 3]
  arr.includes(7) // false
  arr.includes(1, 3) // false
  arr.includes(2) // true
  ```

* `every()` 方法，接受一个检测函数（predicate），如果数组的每一项都能通过函数检测，则返回 true，否则返回 false。检测函数接收三个参数 `predicate(item[, index[, array]])` 分别代表当前数组元素、索引、以及数组本身。

  ```js
  const evens = [0, 2, 4, 6]
  const numbers = [0, 1, 2, 3, 4]
  function isEven(numer) {
    return numer % 2 === 0
  }
  evens.every(isEven) // true
  numbers.every(isEven) // false
  ```

* `some()` 方法，正好与 `every` 方法相反。接受一个检测函数（predicate），如果数组有一项能通过函数检测，则返回 true，否则返回 false。检测函数接收三个参数 `predicate(item[, index[, array]])` 分别代表当前数组元素、索引、以及数组本身。

  ```js
  const evens = [0, 1, 2, 3]
  const numbers = [1,3,5,7]
  function isEven(numer) {
    return numer % 2 === 0
  }
  evens.some(isEven) // true
  numbers.some(isEven) // false
  ```

## 增加数组元素

* `push()` 方法用于在数组的尾部添加一个或者多个元素，并返回数组的长度。该方法会改变原数组。

  ```js
  let arr = [];
  arr.push(1);
  arr.push(2,3,4);
  arr.push(true, {});
  console.log(arr); // [1, 2, 3, 4, true, {}]
  ```

* `unshift()` 方法用于在数组的头部添加一个或者多个元素，返回数组的长度。该方法会改变原数组。

  ```js
  let arr = [1, 2, 3];
  arr.unshift('a'); 
  arr.unshift('b', 'c');
  console.log(arr); // ['b', 'c', 'a', 1, 2, 3]
  ```

## 修改数组

* `reverse()` 方法用于反转数组元素，返回改变后的数组。该方法会改变原数组。

  ```js
  let arr = ['a', 'b', 'c'];
  arr.reverse(); 
  console.log(arr); // ['c', 'b', 'a']
  ```

* `sort()` 方法对数组元素进行排序。排序后原数组会发生改变。

  ```js
  let arr = [11, 101];
  arr.sort();
  console.log(arr); // [101, 11]
  ```

  如果不给 `sort()` 方法指定排序方法，数字会先转换为字符串，再按照字典顺序进行比较，所以 `101` 排在 `11` 的前面。

  可以给 `sort` 方法传入一个函数，自定义排序：

  ```js
  let arr = [10111, 1101, 111];
  arr.sort(function (a, b) {
     return a - b;
  });
  console.log(arr); // [111, 1101, 10111]
  ```

  `sort` 的参数接收两个参数，表示进行比较的两个数组的成员。如果该函数的返回值大于 0 ,则表示第一个成员排在第二个成员的后面，其他情况下都是第一个元素排在第二个元素的前面。

  也可以指定字段进行排列：

  ```js
  let arr = [
    { name: "张三", age: 30 },
    { name: "李四", age: 24 },
    { name: "王五", age: 28  }
  ];
  arr.sort(function(a, b) {
    return a.age - b.age
  });
  console.log(arr); 
  /*
    [
    	{ name: "李四", age: 24 },
    	{ name: "王五", age: 28 },
    	{ name: "张三", age: 30 },
    ]
  */
  ```

## 数组变换

* `map()` 方法，将数组的所有成员依次传入参数函数，然后每一次的执行结果组成一个新数组返回。**返回的数组中的元素并不会减少；** 注意：该方法并不会更改原始数组！

  ```js
  let arr = [1, 2, 3];
  let arr2 = arr.map(item => item * 2)
  console.log(arr2); // [2, 4 ,6]
  console.log(arr); // [1, 2, 3]
  ```

* `filter()` 方法，用于过滤数组成员，满足条件的成员组成一个新的数组返回，如果条件不满足则返回空数组。 **返回的数组元素会减少；** 注意：该方法不会改变原始数组！

  ```js
  let arr = [1, 2, 3, 4, 5, 6];
  let arr2 = arr.filter(item => item % 2 === 0)
  console.log(arr2); // [2, 4 ,6]
  console.log(arr); // [1, 2, 3, 4, 5, 6]
  
  let arrBooolean = [0, 1, 'a', false, '', undefined, null, NaN]
  let arrNew = arrBooolean.filter(Boolean); // [1, a]
  ```

* `reduce()` 方法，该方法会依次处理数组的每一个成员，最终累计一个值。接收两个参数，第一个参数时回调函数，第二个参数则是初始值。该方法比较复杂，推荐一篇文章可以延伸阅读 [reduce 实用指南](https://juejin.im/post/5bab8a9c6fb9a05d0e2e6bf0)。

## 填充数组

* `array.fill()` 方法，语法：`array.fill(value[, fromIndex[, toIndex]])` 表示数组中从下标为 `fromIndex` 到 `toIndex`的值填充，不包含 `toIndex` 本身。`fromIndex` 是可选参数默认为 `0`, `toIndex` 可选参数默认为 

  `array.length`。**该方法会改变原数组**。

  ```js
  const numbers = [1, 2, 3, 4]
  numbers.fill(0);
  console.log(numbers) // [0, 0, 0, 0]
  ```

  还可以利用 `length` 来初始化特定长度的初始化数组的值。

  ```js
  const length = 3
  const initArray = Array(length).fill(0) // Array 为数组的构造函数
  console.log(initArray) // [0, 0, 0]
  ```

* `Array.from()` 也可以初始化带有对象的特定长度的数组

  ```js
  const length = 4
  const initArray = Array.from(Array(4), () => {
    return {}
  })
  console.log(initArray) // [{}, {}, {}, {}]
  ```

## 数组扁平化

* `flat()` 方法，语法：`array.flat([depth])` 通过递归扁平属于数组的项直到一定深度来创建新数组，**该方法不会改变原数组**。`depth` 代表递归深度，默认为 1。`Infinity` 可展开任意深度的嵌套数组。

  ```js
  const arrays = [0, [1, 3, 5], [2, 4, 6]]
  const flatArray = arrays.flat()
  console.log(flatArray) // [0, 1, 3, 5, 2, 4, 6]
  ```

## 参考资料

[阮一峰网道教程 Array 对象](http://wangdoc.com/javascript/stdlib/array.html)

