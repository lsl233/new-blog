---
title: VUE 学习总结
date: 2019-11-18 20:54:40
tags:
  - VUE
  - JavaScript
  - 生命周期
---
对于 Vue 学习总结...

# 生命周期
### beforeCreate & created
`beforeCreate` 组件创建之前, 在VUE源码中, 
``` JavaScript
Vue.prototype._init = function (options?: Object) {
  // ...
  initLifecycle(vm)
  initEvents(vm)
  initRender(vm)
  callHook(vm, 'beforeCreate')
  initInjections(vm) // resolve injections before data/props
  initState(vm)
  initProvide(vm) // resolve provide after data/props
  callHook(vm, 'created')
  // ...
}
```
initState 主要是 `props`、`data`、`methods`、`watch`、`computed`, 所以不能获取 `props`、`data`, 也不能调用 `methods` 中的方法,  但是可以获取到`router` 信息, 一般会用于权限验证, 自定义重定向操作.

`created` 组件创建完成, 尽早请求数据, 一般会这里进行数据请求, 可以获取 `props`、`data`、`methods`

### beforeMount & mounted
`beforeMount ` 组件挂在之前 (该钩子在服务器端渲染期间不被调用)
`mounted` 即组件挂在完成, 可以通过$refs获取组件实例或者真是DOM, 一般会做事件绑定, 调用组件内部方法.

### beforeUpdate & updated
beforeUpdate 数据更新之前, 这里适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器
`updated` 重新渲染完成后, 组件 DOM 已经更新

### beforeDestroy & destroyed
`beforeDestroy ` 组件销毁之前, 可以访问 `props` `data`..., 一般用于清除 在当前组件内绑定的全局事件 setTimeout, setInterval

`destroyed ` 组件销毁后, 所有的事件监听器会被移除，所有的子实例也会被销毁(该钩子在服务器端渲染期间不被调用)

### activated & deactivated
钩子函数是专门为 keep-alive 组件定制的钩子
当A组件第一次切换到B组件, B组件会执行 `created` 和 `activated`, B 切换到 A 时会触发 `deactivated`
A 再次切换回 B 时, B只会执行 `activated`

### errorCaptured
当捕获一个来自子孙组件的错误时被调用, 此钩子可以返回 false 以阻止该错误继续向上传播。
