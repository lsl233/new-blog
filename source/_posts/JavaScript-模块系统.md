---
title: JavaScript 模块系统
date: 2019-11-19 15:15:09
tags:
---

## CommonJS
### 规范
CommonJS 是同步加载模块，是以在浏览器环境之外构建 JavaScript 生态系统为目标而产生的项目，比如在服务器和桌面环境中。
一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在一个文件定义的变量（还包括函数和类），都是私有的，对其他文件是不可见的。CommonJS 加载模块是同步的.所以只有加载完成才能执行后面的操作。
### 实现
`Node.js` 原生模块系统

### AMD
AMD 采用异步方式加载模块，模块的加载不影响它后面语句的运行。这里异步指的是不堵塞浏览器其他任务（dom构建，css渲染等），而加载内部是同步的（加载完模块后立即执行回调）。
实现
`RequireJS`

> 优点: 可以异步加载模块
> 缺点: 不能按需加载依赖模块，必须提前加载
> https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88)

## CMD
### 规范
CMD规范是阿里的玉伯提出来的, 为了解决在AMD规范中没有规范按需加载的问题
实现
`SeaJS`

优点:
* 同样实现了浏览器端的模块化加载。
* 可以按需加载，依赖就近。

### UMD
是一个前后端跨平台的解决方案, 它同时使用两种规范的规范。所以UMD的模块可以同时在客户端和服务端使用
``` JavaScript
// if the module has no dependencies, the above pattern can be simplified to
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define([], factory);
    } else if (typeof exports === 'object') {
        // Node. Does not work with strict CommonJS, but
        // only CommonJS-like environments that support module.exports,
        // like Node.
        module.exports = factory();
    } else {
        // Browser globals (root is window)
        root.returnExports = factory();
  }
}(this, function () {

    // Just return a value to define the module export.
    // This example returns an object, but the module
    // can return a function as the exported value.
    return {};
}));
```

### ES6 Import

### 实现

## CommonJS
CommonJS 是同步加载模块, CommonJS 定义的模块分为3部分:
1. 模块引用(require)
2. 模块定义(exports)
3. 模块标识(module)

`require`用来引入外部模块；`exports`对象用于导出当前模块的方法或变量，唯一的导出口；`module`对象就代表模块本身。

> 所有代码都运行在模块作用域，不会污染全局作用域。
> 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。
> 模块加载的顺序，按照其在代码中出现的顺序。


