上一篇文章介绍了如何使用**递归**来进行排序。这节课我们使用循环来引入更多更好的排序。

## 选择排序

选择排序，就是每次找到一个最小的值，然后把它放到最前面（从小到大排列）。那如何找到最小值呢，思路：找到最小值的下标。如下代码：

```js
let minIndex = (numbers) => {
  let index = 0;
  for(let i = 1; i < numbers.length; i++) {
    // 循环着比对那个值大
    if (numbers[i] < numbers[index]) {
      index = i
    }
  }
  return index;
}
```

上述代码找到了一个数组中最小数值的下标。就可以找到当前数组中的最小的数字，那么就把这个数字放在最前面。然后再循环，再找最小的。假如，一个数组是这样的 `[3,5,4,2,1]` 可以看出第一次的最小值是 `1` 对应的下标则是 `4`。那么就需要把`1`放到最前面，就是要把 `1` 跟 `3` 的位置进行调换，调换之后把 `1` 站定 然后剩余的数字再进行比较，然后再调换。转换为代码如下：

```js
let sort = (numbers) => {
  // 为什么需要length-1，因为最后一次不需要比较，前几次占位之后，最后一次自然就确定位置
	for(let i = 0; i < numbers.length - 1; i++) {
    console.log('------')
    console.log(`i:${i}`)
    // 每次找到最小值后，就应该把这个值去掉，然后剩余的比较，不然每次都要比较, 为什么加i，因为如果不加，则下标每次都是从0开始
    let index = minIndex(numbers.slice(i)) + i;
    console.log(`index:${index}`)
    console.log(`min:${numbers[index]}`)
    if(index !== i) {
      swap(numbers, index, i)
      console.log(`swap ${index}: ${i}`)
 			console.log(numbers)
    }
  }
  return numbers
}

// 交换位置函数
let swap = (arr, i, j) => {
  let temp = arr[i]
  arr[i] = arr[j]
  arr[j] = temp
}
```

## 快速排序

快速排序的核心思想就是，找准一个基准值，一般都是中间值。然后比这个基准值大的放右边，比这个数小的放左边。然后再找，再排，以此类推。

```js
let quickSort = arr => {
  let (arr.length <= 1) {
    return
  }
  let pivoIndex = Math.floor(arr.length / 2)
  let pivot = arr.splice(pivoIndex, 1)[0]
  let leftArr = []
  let rightArr = []
  
 	for(let i = 0; i < arr.length; i++) {
    if(arr[i] < pivot) {
      leftArr.push(arr[i])
    } else {
      rightArr.push(arr[i])
    }
  }
  return quickSort(leftArr).concat([pivot], quickSort(rightArr))
}
```



