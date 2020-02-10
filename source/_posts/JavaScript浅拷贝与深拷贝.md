---
title: JavaScript浅拷贝与深拷贝
date: 2019-04-08 20:40:12
tags:
    - JavaScript
    - 基础
---
JavaScript浅拷贝与深拷贝
<!-- more -->
### 拷贝
**赋值**：将一个变量的值赋给另一个变量。

``` JavaScript
let a = 1
let b = a
console.log(b) // 1
a = 2
console.log(a, b) // 2 1
```
基本数据类型：赋值，赋值之后两个变量互不影响。

```JavaScript
let a = {
    name: 'lll',
    book: {
        title: 'hello',
        price: 20
    }
}
let b = a
console.log(b)
// {
//     name: 'lll',
//     book: {
//         title: 'hello',
//         price: 20
//     }
// }
a.name = 'sss'
a.book.price = 100
console.log(a, b)
// {
//     name: 'sss',
//     book: {
//         title: 'hello',
//         price: 100
//     }
// }

// {
//     name: 'sss',
//     book: {
//         title: 'hello',
//         price: 100
//     }
// }
```
引用数据类型：赋址，两个变量具有相同的引用，指向同一个对象，相互之间有影响。a 与 b 都只保存了对象引用地址，无论 a 或 b 谁修改了对象中的数据，都会影响。

### 浅拷贝（Shallow Copy）
浅拷贝中**浅**的意思即，创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是基本类型，拷贝的就是基本类型的值，如果属性是引用类型，拷贝的就是内存地址 ，所以如果其中一个对象改变了这个地址，就会影响到另一个对象。浅拷贝只解决了第一层的问题，常用的浅拷贝方法有
1. Object.assign
2. 展展语法(Spread)
3. Array.prototype.slice(针对数组)

### 深拷贝（Deep Copy）
深拷贝会拷贝所有的属性，并拷贝属性指向的动态分配的内存。当对象和它所引用的对象一起拷贝时即发生深拷贝。深拷贝相比于浅拷贝速度较慢并且花销较大。拷贝前后两个对象互不影响。常用的深拷贝方法有：
1. JSON.parse(JSON.stringify(object));

> 1 方法会有几个问题
> 1. 会忽略 undefined
> 2. 会忽略 symbol
> 3. 会忽略 function
> 4. 不能循环引用的对象（Uncaught TypeError: Converting circular structure to JSON）
> 5. 不能正确处理 new Date() (时间转换为字符串)
> 6. 不能处理正则（转换为控对象{}）
