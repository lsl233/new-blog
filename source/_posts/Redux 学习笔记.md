---
title: Redux 学习笔记
date: 2017-7-11 2:53
tags: 
  - React
  - Redux
  - JavaScript
---
Redux 学习笔记
<!-- more -->
### store

**Store** Store 就是保存数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。

Redux 提供createStore这个函数，用来生成 Store。createStore函数接受另一个函数作为参数，返回新生成的 Store 对象。

```javascript
import { createStore } from 'redux';const store = createStore(fn);
```

### action

**Action** State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，State 的变化必须是 View 导致的。Action 就是 View 发出的通知，表示 State 应该要发生变化了。

Action 是一个对象。其中的type属性是必须的，表示 Action 的名称。其他属性可以自由设置，社区有一个规范可以参考。改变 State 的唯一办法，就是使用 Action。它会运送数据到 Store。

```javascript
const action = {
	type: 'ADD_TODO',
  	payload: 'Learn Redux'
};
```
### dispatch

dispatch()是 View 发出 Action 的唯一方法。dispatch接受一个 Action 对象作为参数，将它发送出去。

```javascript
dispatch({
  type: 'ADD_TODO',
  payload: 'Learn Redux'
});
```

### reducer

Store 收到 Action 以后，必须给出一个新的 State，这样 View 才会发生变化。这种 State 的计算过程就叫做 Reducer。Reducer 是一个函数，它接受 Action 和当前 State 作为参数，返回一个新的 State。

```javascript
const reducer = function (state, action) {  
  // ...  
  return new_state;
};
```