由以下例子引入算法。

> 例子1：如何找出两个数字中较小的那一个？

* 如何表示两个数？使用数组表示 `[a, b]` 表示两个数字。代码演示：

  ```js
  let minof2 = numbers => numbers[0] > numbers[1] ? numbers[0] : numbers[1];
  
  minof2.call(null,[1,2]);
  ```

* `ES6` 优化版：

  ```js
  let minof2 = ([a, b]) => a > b ? b : a;
  minof2.call(null, [1, 2])
  ```

* `JS` 内置方法

  ```js
  Math.min(1, 2); // 1
  Math.min.call(null, 1, 2); //1
  Math.min.apply(null, [2, -1]); // -1
  ```

> 例子2：如何找出三个数中最小的数字？

如果我们需要找三个数字中最小的，通过例子1我们知道可以找出两个数字中最小的，那么是不是可以先找出两个数字中最小的再拿另外一个比较，因为我们已经学会了如何比较两个数字中最小的。代码演示：

```js
let minof3 = ([a, b, c]) => {
  return minof2([a, minof2([b, c])]);
};
// 或者
let minof3 = ([a, b, c]) => {
  return minof2([minof2([a, b]), c])
};
```

由此得出推理，如果是4个数字呢？得出以下代码：

```js
let minof4 = ([a, b, c, d]) => {
  return minof2([a, minof3([b, c, d])])
};
```

所以，**任意长度数组求最小值，都可以通过 `minof2` 方法实现**。

终极方法：

```js
let min = (numbers) => {
  if (numbers.length > 2) {
    return min([numbers[0], min(numbers.slice(1))])
  } else {
    return Math.min.apply(null, numbers)
  }
}
// 采用递归的方式进行输出
```

