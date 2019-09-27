函数是一段可以反复调用的代码块。函数能接收输入的参数，不同的参数会返回不同的值。函数跟数组一样也是一种特殊的对象。

## 定义函数

* 具名函数定义

  ```js
  function fn(s) {
      console.log(s)
  }
  ```

* 函数表达式定义

  ```js
  let fn = function(x, y) {return x + y}
  let fn2 = function fn(x, y) {return x + y};
  fn2(); // fn is not defined, 等于号右边有名字的函数作用域只作用于等于号右边
  ```

* 箭头函数定义

  ```js
  let f1 = x => x*x
  let f2 = (x, y) => x + y // 如果是两个参数及以上则圆括号不能省略
  let f3 = (x, y) => {return x + y} // 如果有两个以上的语句则花括号不能省略， 且 return 也不能省略
  let f4 = (x, y) => ({name: x, age: y}); // 直接返回对象会报错，需要加一个圆括号
  
  f1(8); // 64
  f2(6, 7); // 13
  f3(5, 8); // 13
  ```

* 构造函数定义（不推荐，了解即可）

  ```js
  let fn = new Function('x', 'y', 'return x + y');
  // 等同于
  function fn(x, y) {
      return x + y
  }
  ```

**重点：所有函数都是 `Function` 构造出来的，包括 `Object` 、`Array` 、`Function` 也是**

