---
title: react-component
date: 2018-11-30 14:43:17
tags: react component
---
react 中组件分类
<!-- more -->
# Class Component
最传统, 最常用的组件
```javascript
export default class Welcome extends Component {
    render() {
        return <h1>Welcome, {this.props.name}</h1>
    }
}
```

# Function Component
函数组件, 适合纯展示类组件, 无法操作state
```javascript
export default function Welcome(props) {
    return <h1>Welcome, {props.name}</h1>
}
```

# Higher-Order Component(HOC)
高阶组件, 源于高阶函数(Higher-Order Function), 高阶函数需要满足以下条件:
1. 接受一个或多个函数作为输入
2. 输出一个函数

高阶组件也是一样, 接受一个或多个组件, 输出一个组件
```javascript
function HOC(WrappedComponent) {
    return class extends Components {
        render() {
            return <WrappedComponent {...props} data={this.state} />
        }
    }
}

class WrappedComponent extends Components {
    render() {
        return <h1>Welcome, {this.props.name}</h1>
    }
}

export default HOC(WrappedComponent);
```
