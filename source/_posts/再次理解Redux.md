---
title: 再次理解Redux
date: 2017-07-21 21:20:49
tags: Redux React js
---
<!-- more -->
# 区分store和state
state 是应用的状态，一般本质上是一个普通对象
例如，我们有一个 Web APP，包含 计数器 和 待办事项 两大功能
那么我们可以为该应用设计出对应的存储数据结构（应用初始状态）：
```JavaScript
{
  counter: 0,
  todos: []
}
```
store 是应用状态 state 的管理者

### 获取store

```JavaScript
import { createStore } from 'redux'
...
const store = createStore(reducer, initialState) 
```
> reducer 是一个 函数，负责更新并返回一个新的 state
> 而 initialState 主要用于前后端同构的数据同步
### 获取state
```JavaScript
var state = store.getState()
```
Redux 规定，一个应用只应有一个单一的 store，其管理着唯一的应用状态 state
Redux 还规定，不能直接修改应用的状态 state
若要改变 state，必须 dispatch 一个 action

### action
action（动作）实质上是包含 type 属性的普通对象，这个 type 是我们实现用户行为追踪的关键

```JavaScript
{
  type: 'ADD_TODO',
  payload: {
    id: 1,
    content: '待办事项1',
    completed: false
  }
}
```

### Action Creator
顾名思义，Action Creator 是 action 的创造者，本质上就是一个函数，返回值是一个 action（对象

### Reducer
用户每次 dispatch(action) 后，都会触发 reducer 的执行 
reducer 的实质是一个函数，根据 action.type 来更新 state 并返回 nextState
最后会用 reducer 的返回值 nextState 完全替换掉原来的 state

```JavaScript
var initState = {
  counter: 0,
  todos: []
}

function reducer(state, action) {
  // ※ 应用的初始状态是在第一次执行 reducer 时设置的 ※
  if (!state) state = initState
  
  switch (action.type) {
    case 'ADD_TODO':
      var nextState = _.cloneDeep(state) // 用到了 lodash 的深克隆
      nextState.todos.push(action.payload) 
      return nextState

    default:
    // 由于 nextState 会把原 state 整个替换掉
    // 若无修改，必须返回原 state（否则就是 undefined）
      return state
  }
}
```
通俗点讲，就是 reducer 返回啥，state 就被替换成啥

### middleware
中间件，middleware是架在action和store之间的一座桥梁

### 总结
store 由 Redux 的 createStore(reducer) 生成
state 通过 store.getState() 获取，本质上一般是一个存储着整个应用状态的对象
action 本质上是一个包含 type 属性的普通对象，由 Action Creator (函数) 产生
改变 state 必须 dispatch 一个 action
reducer 本质上是根据 action.type 来更新 state 并返回 nextState 的函数
reducer 必须返回值，否则 nextState 即为 undefined
实际上，state 就是所有 reducer 返回值的汇总（本教程只有一个 reducer，主要是应用场景比较简单）

### 步骤
Action Creator => action => store.dispatch(action) => reducer(state, action) => 原 state state = nextState