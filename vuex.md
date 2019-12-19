# VueX
什麼是Vuex呢?   VueX是Vue用來統一管理數據(data)的函式庫，並提供更簡潔的方式，使各組件更容易獲得根元素的參數值。

那Vuex怎麼使用呢?我們在以下和你介紹

## Vuex的架構
Vuex由store.js統一管理，並分成六大類

1. state
2. getters
3. mutations
4. actions
5. strict
6. module 

```js
export default new Vuex.Store({
  strict:true,
  state: {},
  getters:{},
  mutations: {},
  actions: {},
  module :{}
})
```
## 流程
[img01]:/image/vuex.png "Vuex圖片"

---
### **1.State**
State是Vuex中存放data的地方，也可將State視為根元素中的data:{ }

在store.js中的用法:
```js
state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
```
在Vue Component中的用法:

- 我們可以透過 `this.$store.state.name` 來獲得state中的name ( 必須搭配`computed` )
```js
computed: {
    count () {
      return this.$store.state.count
    }
}
```
- 必須透過`mutations`來儲存state中的值。
```js
mutations: {
    setName ( state,data ) {
      state.name = data;
    }
}
```
在Vue Component中輔助函數( ...mapState )的用法:
1. 直接引用  ( 帶入vuex參數名 )
2. 指定參數名 ( 指定參數名稱取代vuex參數名 )
3. 搭配函式使用
```js
import { mapState } from 'vuex';

computed: {
  // 使用展開運算符將 mapState 混合到外部物件中
    ...mapState([
      'count',
      countAlias: 'count', //指定組件中的countAlias為count
      countPlusLocalState(state) {
        return state.count + this.localCount;
      },
    ])
  }
```
---
### **2.Getters**
Getters是Vuex中存放過濾State後的參數，也可以認為是State的計算屬性。


在store.js中的用法:
- 我們可以透過 `state.name` 來獲得state中的name，並搭配function處理值。
```js
getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
}
```
- getter也可以處理getters中的值
```js
getters: {
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
```
- getter也可以預設帶入的處理參數
```js
getters: {
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
```

在Vue Component中的用法:
- 我們可以透過 `this.$store.getters.name` 來獲得state中的name ( 必須搭配`computed` )
```js
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```
- 透過`store.getters.getTodoById(id)`去引用getters中預設的處理參數

在Vue Component中輔助函數( ...mapGetters )的用法:
```js
import { mapGetters } from 'vuex';

computed: {
  // 使用展開運算符將 mapGetters 混合到外部物件中
    ...mapGetters([
      'doneTodosCount',
      doneTodosAlias: 'doneTodos',
    ])
  }
```
---
### **2.Mutations**
Mutations是Vuex中改變State的唯一方式，也可以認為是State的計算屬性。
> Mutations是由一個事件類型( type ) 和 一個 callback Function( handler )組成

注意 !! Mutations是用來處理同步參數的
```js
mutations: {
    increment (state) { 
      state.count++
    }
  }
//increment = type ， (state){ } = callback function
```

在store.js中的用法:
- mutations必須由actions或vue component透過`store.commit('increment')`呼叫。
- 也可以透過第二個參數( payload )設定 預帶入參數，actions則由`store.commit('increment', {amount: 10})`呼叫。
```js
mutations: {
  increment (state, payload) {
    state.count += payload.amount
  }
}
```
- actions也可以直接在`store.commit({
  type: 'increment',
  amount: 10
})`中直接指定事件類型 ( type )


在Vue Component中的用法:
```js
this.$store.commit('increment');
this.$store.commit('increment', {amount: 10});
this.$store.commit({type: 'increment',amount: 10})
```

在Vue Component中輔助函數( ...mapMutations )的用法: