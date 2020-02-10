---
title: 深入学习JavaScript类型判断
date: 2019-03-31 22:07:08
tags:
    - JavaScript
    - JS 
    - 基础
---
JavaScript 没有一个函数或者操作符就可以判断所有的基本数据类型和复杂类型
<!-- more -->

### typeof
typeof 操作符用来返回数据类型，它可判断的类型有一下几种：

| 类型                                        | 结果                                 |
| ------------------------------------------- | ------------------------------------ |
| Undefined                                   | 'undefined'                          |
| Null                                        | 'object'（见下文）                   |
| Boolean                                     | 'boolean'                            |
| Number                                      | 'number'                             |
| String                                      | 'string'                             |
| Symbol （ECMAScript 6 新增）                | 'symbol'                             |
| 宿主对象（由JS环境提供）                    | Implementation-dependent(由宿主确定) |
| 函数对象（[[Call]] 在ECMA-262条款中实现了） | 'function'                           |
| 任何其他对象                                | 'object'                             |

但是它不能准确判断`null`，这是一个设计缺陷。

| 表达式           | typeof          | 类型      |
| :--------------- | :-------------- | :-------- |
| null             | object          | Null      |
| {}               | object          | Object    |
| 3                | number          | Number    |
| new Number(3)    | object          | Number    |
| 'ok'             | string          | String    |
| new String('ok') | object          | String    |
| true             | boolean         | Boolean   |
| undefined        | undefined       | Undefined |
| Symbol('a')      | symbol          | Symbol    |
| (function(){})   | function        | Object    |
| /s/(正则表达式)  | function/object | Object    |
| NaN              | Number          | NaN       |

所以 typeof 能够判断 除了 Null 类型意外的 其他**6**中数据类型, 再加 Object类型的子类型 `function`

### instanceof
instanceof 操作符判断一个**对象**是否属于某个构造函数的实例，也可以判断一个对象的实例。

| 数据              | 原型            | 结果           |
| ----------------- | --------------- | -------------- |
| 'str'             | String/Object   | false          |
| new String('str') | String/Object   | true           |
| 123               | Number/Object   | false          |
| new Number(123)   | Number/Object   | true           |
| new Date()        | Date/Object     | true           |
| []                | Array/Object    | true           |
| (function () {})  | Function/Object | true           |
| ({})              | Object          | true           |
| undefined         | Undefined       | ReferenceError |
| Symbol('hello')   | Symbol/object   | false          |

instanceof 有个小技巧，可以巧妙地解决，调用构造函数时，忘了加new命令的问题。
```JavaScript
function Foo(options){
    if (this instanceof Foo) {
        this.options = options;
    } else {
        return new Foo(options);
    }
}
```
但是不同window或不同iframe之间对象类型检测不能用instanceof。
```JavaScript
var iframe = document.createElement('iframe')
document.documentElement.appendChild(iframe)
iframe.src="javascript:var b = {};"

var b1 = iframe.contentWindow.b;
var b2 = {};

console.log(typeof b1, typeof b2); //object object

console.log(b1 instanceof Object, b2 instanceof Object); //false true

```

### toString
实例对象的toString方法可以十分准确判断数据类型的方法。

| 数据            | 结果                 |
| --------------- | -------------------- |
| 2               | '[object Number]'    |
| NaN             | '[object Number]'    |
| 'abc'           | '[object String]'    |
| true            | '[object Boolean]'   |
| undefined       | '[object Undefined]' |
| null            | '[object Null]'      |
| Math            | '[object Math]'      |
| {}              | '[object Object]'    |
| []              | '[object Array]'     |
| function() {}   | '[object Function]'  |
| /abcd/          | '[object RegExp]'    |
| new Date()      | '[object Date]'      |
| Symbol('hello') | '[object Symbol]'    |
| new Set()       | '[object Set]'       |

可以利用toString 可以写出比typeof运算符更准确的类型判断函数。
```JavaScript
function getType (o){
    var s = Object.prototype.toString.call(o)
    return s.match(/\[object (.*?)\]/)[1].toLowerCase()
}
```

### 补充

#### 类数组
拥有length属性，key为为非负整数的对象，但是没有数组其他方法 `push`, `forEach`, `indexOf` 等叫做类数组，常见的伪数组有 `arguments`, `NodeList`, `HTMLCollection` Jquery内部大量运用了伪数组。可以说整个Jquery对象，都是构建在伪数组的基础之上的。
转换为真数组
为什么要有类数组呢？类数组可以添加特有的属性，不必在数组上添加。比如arguments上，有`callee`（ES5严格模式中删除）
缺点：类数组本来就是对象，所以遍历类数组与遍历数组性能差距非常大。

`slice`, `from`
```JavaScript
const arrayLike = {
    length: 2,
    0: 'hello',
    1: 'world'
}

Array.prototype.slice.call(arrayLike)

Array.from(arrayLike)
```
由于类数组没有实现数组方法，所以需要使用`Array.prototype`来调用数组原生方法
```JavaScript
Array.prototype.forEach.call(arrayLike, () => console.log(item))
Array.prototype.push.call(arrayLike, '.')
```
判断是否为类数组(参考 underscore 中的实现)
```JavaScript
function isArrayLike(o) {
    // 返回参数 collection 的 length 属性值
    var length = o.length;
    
    // length是数值，非负，且小于等于MAX_ARRAY_INDEX
    // Number.MAX_SAFE_INTEGER 最大安全整数
    return typeof length == 'number' && length >= 0 && length <= Number.MAX_SAFE_INTEGER;
}
```

