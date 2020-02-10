---
layout: react
title: React lifecycle
date: 2018-11-29 11:40:26
tags: React lifecycle Javascript
---
React 生命周期
<!-- more -->
React 的生命周期主要分为4个阶段:
1. 初始化(Initialization)
2. 挂在(Mounting)
3. 更新(Update)
4. 卸载(Unmounting)

## Initialization
初始化阶段, 组件准备数据的时候. 为接下来渲染组件做数据准备
这个阶段一般会进行以下操作:
1. 初始化`state`
```Javascript
state = {
    // Initializing state
}
```
2. 设置默认`prop`
```javascript
static defaultProps = {
    // default defaultProps
}
```

## Mounting
挂载阶段会依次执行以下生命周期函数
新: `constructor` -> `static getDerivedStateFromProps` -> `render` -> `componentDidMount`
旧: `constructor` -> `componentWillMount` -> `render` -> `componentDidMount`

### constructor
构造方法常常也用于初始化state
```javascript
constructor(props) {
    super(props);
    this.state = {
        // Initializing state 
    };
}
```

### static getDerivedStateFromProps
这一生命周期方法是静态的，它在组件实例化或接收到新的 props 时被触发, 如果返回对象则会更新state, 如果为null则什么也不更新
```javascript
static getDerivedStateFromProps(nextProps, prevState) {
    nextProps // 最新props
    prevState // 当前state
}
```

### render
`render`方法, 需要返回 JSX 或者 null
```javascript
render() {
    return // jsx or null
}
```

### componentDidMount
该方法中, dom已经挂载完成, 可以访问元素dom元素, 绑定原生事件, 如果有异步数据初始化, 一般也在这里请求后更新state
```javascript
componentDidMount() {
    // add event
    // refs
    // ajax
}
```

## Update 
数据更新(使用`setState`或props更新后)后渲染, 会依次执行以下生命周期函数
新: `static getDerivedStateFromProps` -> `shouldComponentUpdate` -> `render` -> `getSnapshotBeforeUpdate` -> `componentDidUpdate`
旧: `componentWillReceiveProps` -> `shouldComponentUpdate` -> `componentWillUpdate` -> `render` -> `componentDidUpdate`

### static getDerivedStateFromProps
同上

### shouldComponentUpdate
用于判断是否需要渲染组件, 返回 true 需要, false 则不需要.

### render
同上

### getSnapshotBeforeUpdate
在render之后，但在节点挂载前, 调用, 返回值作为`componentDidUpdate` 第三个参数

```javascripot
getSnapshotBeforeUpdate(prevProps, prevState) {
    if (prevProps.list.length < this.props.list.length) {
      return this.listRef.current.scrollHeight; // componentDidUpdate 的第三个参数
    }
    return null;
  }
```

### componentDidUpdate
在节点挂载后
```javascript
componentDidUpdate(prevProps, prevState, snapshot) {
    // 更新dom
  }
```

## Unmounting
组件卸载阶段, 组件卸载前会执行`componentWillUnmount`, 这个函数主要用于清除原生事件绑定,`timeout`和`interval`

