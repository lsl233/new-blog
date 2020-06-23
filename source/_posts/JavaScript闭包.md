---
title: JavaScript闭包
date: 2016-06-7 20:42:53
tags: JavaScript 闭包
---
在《你不知道的JavaScript》书中作用域闭包中看到
“对于那些有一点JavaScript使用经验但从未真正理解闭包概念的人来说，理解闭包可以看作是某种意义上的从生。”
<!-- more -->
### 理解
下面这段代码，是最常用也经常看到的闭包：
```javascript
function foo() {
    var a = 2;
    function bar() {
        console.log(a);    
    }
    return bar;
}
var baz = foo();
baz(); // 2
```
通常函数在执行完毕后，函数内部的变量都会被销毁，而闭包可以阻止这一行为，`bar()`函数依然维持着外部作用域`foo()`的引用，所以在执行`baz()`后，`a`变量依然可以访问父元素的变量。


下面是一个类似于jquery的写法，也是一个闭包。
```javascript
(function () {
    var a = 0;
    var tools = {};

    tools.get = function () {
        return a;
    };

    tools.set = function (val) {
       a = val;     
    };

    // ...

    window.tools = tools;
})();

tools.get();
```
上面这个函数看起来不像是闭包，因为没有`return`，其实它就是一个闭包，一个自执行函数内部有一个变量`a`，一个对象`tools`，tools有两个方法`get`，`set`，通过`window`对象，把tools对象暴露为全局对象，在自执行函数外部就可以访问到变量`a`，依然维持着`tools.get`父级作用域的引用。

对于闭包还有一个可怕的说法是，闭包不会自动释放内存，会造成内存泄漏，所以要减少闭包的使用。这个说法很片面，因为使用闭包，是因为，我们确实需要局部变量，如果不使用闭包，就会把变量设置成全局变量， 而全局变量一样不会被自动销毁，其实和使用闭包的影响是差不多的。所以这说法是不对的。

### 循环中的闭包
再循环中使用闭包，回出现和想象中不一样的结果
```javascript
for (var i = 0, l = 6; i < l; i++) {
    btn[i].addEventListener('click', function () {
        console.log(i);
    }, false);
}
```
这段代码，理想状态下是希望利用for循环依此给6个btn元素绑定一个事件，输出线对应的数字。但结果是btn的click事件加上了，但每个按钮输出结果都是6。
回掉函数执行时候，内部的i指向的是全局变量i，而此时for循环已经循环完毕，所以看出在i是**全局变量**，所以要在for循环的时候，让每一次循环创建一个独立的作用域！

es5解决方案，匿名自执行函数。

```javascript
for (var i = 0, l = 6; i < l; i++) {
	(function (a) {
	    btn[i].addEventListener('click', function () {
	        console.log(a);
	    }, false);
	})(i);
}
```
通过一个匿名自执行函数将将i传递给a，回掉函数中的a就指向了父级作用域的，这样输出结果就和理想结果一样。

es6解决方案，let关键字
```javascript
for (let i = 0, l = 6; i < l; i++) {
    btn[i].addEventListener('click', function () {
        console.log(i);
    }, false);
}
```
其实思想和上面的思想一样，创造一个封闭的环境，let关键字作用是申明一个局部变量，隐式的添加{}，生成一个块级作用域。

### 应用
模拟私有变量，将一些不必要暴露变量或方法隐藏起来，只暴露关键方法给外部使用。
```javascript
function Counter() {
    var a = 0;
    var b = 1;
    return {
        add: function () {
            a = a + b;
        },
        get: function () {
            return a;
        }
    }
}
```
上面函数`Counter`内部有变量`a`和`b`，返回add和get方法。在外部我们只能通过`add`方法执行`a+b`，`get`方法来获取变量a，而无法获取变量b，这样函数的安全性就得到了保障。

包装一个函数，返回一个新函数

```javascript
function bind(context, name) {
  return function() {
    return context[name].apply(context, arguments);
  }
}

var button = {
  clicked: false,
  click: function() {
    this.clicked = true;
    console.log(this)
  }
}

document.getElementById('btn').addEventListener('click', bind(button, 'click'), false)

```
这是一个简单的bind方法，通过apply和闭包强制改变函数的上下文环境。

### 总结
闭包在我的理解下就是，通常一个函数在执行完毕后内部作用域的变量就会被销毁，无法访问，而在闭包中，函数执行完毕后会阻止作用域的销毁，在函数外部便能够访问函数内部的变量或函数。
