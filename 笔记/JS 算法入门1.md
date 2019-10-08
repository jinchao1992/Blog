由以下例子引入算法。

## 最小值算法

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

## 排序算法

### 递归实现方法

> 例子1 长度为2的数组实现从小到大排序

```js
let sort2 = ([a, b]) => a < b ? [a, b] : [b, a]
```

> 例子2 长度为3的数组实现从小到大排序

如果知道长度为2的数组的排序，那如果在数组的三个值中把最小值找出来，然后再排序其他两个的值？这样的方法是否可行呢？

```js
let sort3 = ([a, b, c]) => {
  return [min([a, b, c]), sort2([???])]
}
// 这里是无法确定sort2中的值，因为可能值为 [a,b] [b,c] [a,c]
```

改进版

```js
let minIndex = numbers => {
  return numbers.indexOf(min(numbers))
}
let sort3 = (numbers) => {
  let index = minIndex(numbers); // 找出数组中最小值的下标
  let min = numbers[index]; // 得出最小值
  numbers.splice(index, 1); // 从数组中删除最小值
  return [min].concat(sort2(numbers)); // 数组中删除最小值后单独组成一个数组，然后再通过两个值的排列，再组合为一个新数组
}
```

> 例子3 如果数组长度为4实现从小到大排序

```js
let sort4 = numbers => {
  let index = minIndex(numbers);
  let min = numbers[index];
  numbers.splice(index, 1);
  return [min].concat(sort3(numbers));
}
```

由此可以得出是不是任意长度的数组都可以按照上述的方法进行排序

```js
let sort = (numbers) => {
  if (numbers.length > 2) {
    let index = minIndex(numbers);
    let min = numbers[index];
    numbers.splice(index, 1);
    return [min].concat(sort(numbers))
  } else {
    return numbers[0] < numbers[1] ? numbers : numbers.reverse()
  }
}
```

## 总结

通过以上的代码我们得出了两个算法，算是比较基础的算法：

* 找出最小值的算法 `min`；
* 选择排序算法 `sort` , 这个算法并不是最优的，接下来的文章会进行算法入门2的 `sort`