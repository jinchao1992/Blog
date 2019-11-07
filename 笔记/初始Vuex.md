2019.11.07 新的开始。

之前对 `Vuex` 基本上就是处于一个了解的状态，根本没有深入研究过。入职新公司公司 `Vue` 项目所有的代码封装都是在 `Vuex` 上，没得办法，学呗！于是开始从头看文档，本篇是 `Vuex` 的一个学习笔记，防止自己遗忘而写（基本上跟官网的API文档一样，为了防止遗忘增深记忆而写，如有不当请谅解。）。

## Vuex 是什么

`Vuex` 是专门为 `Vue.js` 应用程序开发的 **`状态管理模式`**。

`Vuex` 主要是用来解决共享状态的数据操作。如果我们的数据是简单的单一页面，那么不建议使用 `Vuex` 来解决。

## 入手

`Vuex` 应用的核心概念就是 `store` （仓库）。它包含了应用中大部分的状态（`state`）。有如下两个特点：

1. 它的存储是响应式的。当 `Vue` 组件从 `store` 中读取组件状态时，若 `store` 中的状态发生了变化，那么相应的组件也会相应得到高效的更新。
2. 不能直接更改 `store` 中的状态，改变 `store` 中的状态的唯一途径就是显示的提交 `commit`  `mutation`。这样使得我们方便的跟踪每一个状态的变化。

```js
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);

const store = new Vuex.Store({
  state: {
    count: 0
  },
  // 通过 mutation 来改变数据状态
  mutations: {
    add(state) {
      state.count++;
    },
    del(state) {
      state.count--;
    }
  }
});

// commit 触发状态变更
store.commit("add");
console.log(store.state.count);
```

## 重要的概念解读

### State是什么？

`Vuex` 使用的是单一的状态树。所有的「数据源」都存放在 `state` 中。单一的状态树让我们能够直接的定位任一特定的状态片段，在调试的过程中也能轻易地取得整个当前应用状态的快照。

#### 如何在组件中获取Vuex的状态

由于 `Vuex` 的状态存储是响应式的，从 `store` 实例中读取状态最简单的方法就是在计算属性中返回某个状态：

```js
import store from "@/store/index";
export default {
  name: "HiVuex",
  props: {
    msg: {
      type: String,
      default: "Hi"
    }
  },
  data() {
    return {};
  },
  computed: {
    count() {
      return store.state.count;
    }
  }
};
```

如上例子，如果是想获取最新的 `count` 只能到 `computed` 中通过 `state.count` 去获取。`store` 为存放 `Vuex` 的实例对象。

当 `store.state.count` 发生变化时，会重新求取计算属性，并且触发更新相关联的 `DOM`。

但是，这样的话会带来一个缺点就是，需要频繁的引入 `store`，因为不同的组件都要使用相同的状态的话，是必须全部导入才能使用的。那么如何解决这个问题呢？

`Vuex` 通过 `store` 选项，提供了一种机制将状态从根组件“注入”到每一个子组件当中，在子组件中可以通过 `this.$store.state` 来获取数据。

```js
export default {
  name: 'HelloWorld'，
  computed: {
    // 获取状态
    count() {
      return this.$store.state.count
    }
  }
}
```

注意：如果是需要在所有子组件当中使用，则只需在跟组件注册 `store` 选项即可。

#### mapState 辅助函数

我们目前学到了，如果需要监控状态的变化，可以在组件中使用 `computed` 检测到。那如果是多个状态的变化呢？都声明为计算属性显得有点冗余了。为了解决这个问题，可以使用 `Vuex` 提供的 `mapState` 函数帮助生成计算属性，就不需要自己去手动的声明了。

```js
import { mapState } from 'vuex';

export default {
  data () {
    return {
      localCount: 3
    }
  },
  computed: mapState({
    count: (state) => state.count,
    // 这里的 'count' 等同于 state => state.count，相当于是给 count来一个别名
    countAlias: 'count',
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

上述的代码重点在于 `mapState` 中可以对 `Vuex` 状态进行更进一步的操作，而且可以把多个状态值都显示到 `mapState`的返回值中。

当映射的计算属性的名称与 `state` 的子节点名称相同时，可以给 `mapState` 传一个字符串数组。

```js
export default {
  ...
  // 此时的页面中可以直接使用count的状态值
  computed: mapState(['count'])
}
```

**特别注意：`mapState` 对象返回的是一个对象。如何将它与我们在子组件中规定的计算属性混合在一起呢，第一，可以造一个工具方法把对象合并，然后再传给 `computed` 。第二，则可以使用 ES6 新语法扩展运算符。**

```js
export default {
  ...
  computed: {
    localComputed() {/**/},
    ...mapState(['count'])
  } 
}
```

我们可以在我们的局部组件里面保留自己的状态，只有涉及到公用的状态时则可以放入到 `Vuex` 中。这需要根据平时的项目业务情况用来自己做相应的评估。

### Getter

有如下场景，我们需要从 `store` 中的 `state` 数据中引出一些别的状态，例如对列表数据进行过滤并计数：

```js
export default {
  ...
  computed: {
    doneTodosCount () {
      return this.$store.state.todos.filter(todo => todo.done).length
    }
  }
}
```

如果我们想在多个组件当中使用这个属性，要么整体复制此方法，要么写一个公共的方法，用到时再导入。其实在 `Vuex` 中已经可以处理此类逻辑了，那就是使用 `getters`，我们把它认为是 `store` 的计算属性。跟计算属性一样，`getter` 的返回值也会根据它依赖的数据被缓存起来，当依赖的数据发生变化的时候才会被重新计算。

`getters` 接收 `store` 作为它的第一个参数：

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

因为 `Getter` 会暴露为 `store.getters` 对象，所以可以以属性的形式进行访问。

```js
store.getters.doneTodos // { id: 1, text: '...', done: true }
```

`Getter` 还可以接受其他的 `getter` 作为第二个参数的值：

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    },
    doneTodosCount: (state, getters) => {
      return getters.doneTodos.length
    }
  }
})
```

如果是要在组件中使用，可以如下写法：

```js
export default {
  ...
  computed: {
    doneTodoConunted () {
      return this.$store.getters.doneTodosCount
    }
  }
}
```

#### 通过方法访问 getter

可以通过让 `getter` 返回一个函数，来实现给 `getter` 传参。使用的场景则是，如果我们需要对 `store` 里的数组数据进行查询时就显得很重要了。

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    getTodoById: (state) => {
      return (id) => {
        return state.todos.find(todo => id === todo.id)
      }
    }
  }
})
```

```js
store.getters.getTodoById(2) // { id: 2, text: '...', done: false }
```

#### mapGetters 辅助函数

与 `mapState` 类似，`mapGetters` 函数是将 `store` 中的 `getter` 映射到局部的计算属性上。

```js
import { mapGetters } from 'vuex'

export default {
  ...
  computed: {
    // 使用对象的展开运算符将 getter 混入到 computed 对象中
    ...mapGetters([
      'doneTodosCount',
      'doneTodos',
      'getTodosId'
      // ...
    ])
  }
}
```

如果想给 `getter` 属性取另外的名字，则需要使用对象的形式：

```js
import { mapGetters } from 'vuex'

export default {
  ...
  computed: {
    // 使用对象的展开运算符将 getter 混入到 computed 对象中
    ...mapGetters({
      // 取别名
      doneCount: 'doneTodosCount'
    })
  }
}
```

### mutation

在 `Vuex` 中的修改 `store` 中的状态的唯一的方法就是提交 `mutation`。在 `Vuex` 中的 `mutation` 非常类似于事件的操作。它的组成方式是：一个字符串的 **事件类型** 和 一个 **回调函数**。我们可以在回调函数中进行状态的变更，接受 `state` 为第一个参数：

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    addCount(state) {
      state.count++
    }
  }
})
```

在 `Vuex` 中 我们不能直接调用 `mutations` 的方法。这里只是提供事件注册，如果需要调用则需要 `store.commit('addCount')`。

#### 提交载荷（Payload）

在执行 `commit` 传入额外的参数，即 `mutation` 的 **载荷（payload）**。

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutations: {
    addCount (state, n) {
      state.count += n
    }
  }
})

store.commit('addCount', 10)
```

或者传入一个对象更加容易操作：

```js
const store = new Vuex.Store({
  state: {
    count: 1
  },
  mutaions: {
    addCount (state, payload) {
      state.count += payload.amount
    }
  }
})

store.commit('addCount', {
  amount: 10
})

// 或者
store.commit({
  type: 'addCount',
  amoute: 10
})
```

#### Mutation 一些注意事项

1. 提前在 `store` 中初始化所有的属性。

2. 当需要在对象添加新属性时，应该如下两种操作：

   * 使用 `Vue.set(store.state, 'name', 'jack')`。

   * 或者使用对象的扩展运算符操作

     ```js
     store.state.obj = {...store.state.obj, 'name': 'jack'}
     ```

3. `Mutation` 必须是同步函数。

#### 在组件中使用 Mutation

如果需要在组件中提交 `mutation` 可以使用 `this.$store.commit('xxx')` 来提交 `mutation` 当然还可以使用 `mapMutation` 辅助函数将组件中的 `methods` 映射为 `store.commit` 调用，但是前提是必须在根节点注入 `store`。

```js
import { mapMutation } from 'vuex'

export default {
  ...
  methods: {
    ...mapMutation([
      'addCount',
      'delCount'
    ])
  }
}
```

