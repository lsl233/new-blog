---
title: JavaScript 基础-this
date: 2016-07-02 23:00:11
tags:
	- JavaScript
	- this
	- 基础
---

`this`是JavaScript中最复杂的的机制之一，`this`作用是隐式传参，自动引用上下文对象。this是在函数呗调用是绑定的，它指向什么是由函数在哪里调用决定的。
<!-- more -->
调用位置：函数在代码中被调用的位置。
调用栈：为了达到当前执行位置所调用的所有函数。

### 错误理解
this 既不指向函数自身也不指向函数的词法作用域。

### 绑定规则

## 默认绑定
独立的函数调用, 没有任何修饰， foo中this 指向 window。 但是如果是严格模式（strict mode）this 会绑定到 undefined。

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
foo(); // 2
```

### 隐式绑定
当作为对象调用时候， this会指向当前对象，对象属性的最后一层会影响this的指向。

```javascript
function foo () {
    console.log(this.a);
}

var obj1 = {
    a: 42,
    foo: foo
};

obj1.foo() // 42

var obj2 = {
    a: 2,
    obj1: obj1
}
obj2.boj1.foo() // 42
```
### 隐式丢失

```javascript
function foo() {
    console.log(this.a);
}
var obj = {
    a: 2,
    foo: foo
};
obj.foo() // 2

var bar = obj.foo;
var a = 3;
bar() // 3 this指向全局。
```

### 显式绑定
使用call() 和 apply() bind() 方法



