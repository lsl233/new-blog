---
title: JavaScript 模块系统
date: 2019-11-19 15:15:09
tags:
---

## CommonJS
CommonJS 是同步加载模块, CommonJS 定义的模块分为3部分:
1. 模块引用(require)
2. 模块定义(exports)
3. 模块标识(module)

`require`用来引入外部模块；`exports`对象用于导出当前模块的方法或变量，唯一的导出口；`module`对象就代表模块本身。

> 所有代码都运行在模块作用域，不会污染全局作用域。
> 模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。
> 模块加载的顺序，按照其在代码中出现的顺序。

## AMD
AMD 采用异步方式加载模块，模块的加载不影响它后面语句的运行。这里异步指的是不堵塞浏览器其他任务（dom构建，css渲染等），而加载内部是同步的（加载完模块后立即执行回调）。
AMD也采用require命令加载模块，但是不同于CommonJS，它要求两个参数:
``` JavaScript
require([module], callback);
```
> https://github.com/amdjs/amdjs-api/wiki/AMD-(%E4%B8%AD%E6%96%87%E7%89%88)

## CMD

## UMD

## ES6 Import
