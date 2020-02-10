---
title: 深入学习JavaScript类型
date: 2019-03-28 14:31:11
tags: 
  - JavaScript
  - JS 
  - 基础
---
深入学习JavaScript类型...
<!-- more -->
JavaScript语言规定了 <strong>7</strong> 种数据类型:

1. Undefined
2. Null
3. Boolean
4. String
5. Number
6. Symbol (ES6 新加入)
7. Object

其中前**6**个是原始类型（基本数值、基本数据类型），所有基本类型的值都是不可改变的。

### Undefined
Undefined类型表示未定义，它只有一个值：undefined，任何变量在未赋值时都是 undefined，但是undefined是个全局变量，undefined又不是JavaScript关键字，所以可以轻易创建一个变量 undefined 并赋予它任意值，这就可能会影响后续代码的执行（这是JavaScript设计缺陷之一， 2009年的ECMAScript 5被修复了）。所以可以使用 `void` 运算符把人一个表达式转换为 undefined

### Null
Null类型表示空值，它只有一个值：null， null是一个关键字，所以可以放心使用。

### Boolean
Boolean类型表示真和假，它有两个值：true 和 false，他俩都是关键字。不可被修改。

### String
String类型表示文本数据，String最大长度是 2^53 - 1，这个长度不是文字或字母的长度，而是字符串编码长度。JavaScript中字符串一旦创建是无法改变的。每一次修改都会创建一个新字符串。

### Number
Number类型有 2^64 - 2^53 + 3 个值 和 NaN，Infinity，-Infinity，浮点数运算时有精度问题，即 `0.1 + 0.2 == 0.3` 返回false，正确比较方法应该是 `Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON`
> `Number.EPSILON` 最小精度值

### Symbol
Symbol是唯一的并且是不可修改的，可以用来作为Object的key的值

### Object
Object是对象，一个key，value集合，在JavaScirpt有几个基本类型，在对象类型中都有对应的类（基本类型包装对象）：
1. Number
2. String
3. Boolean
4. Symbol

Number、String、Boolean, 可以通过new运算符创建 **对象** , 是对象不是Number、String、Boolean类型，所以直接创建Number、String、Boolean类型 与 通过 new 运算符创建的对象，就算值相同，也不相等，例：
```JavaScript
new Number(1) === 1 // false
```
但是我们可以在基本类型上使用对象上的方法
```JavaScript
"abc".charAt(0)
```
当直接调用Number、String、Boolean时，它们表示强制类型转换
```JavaScript
Boolean(1) === true // true
```
Symbol 比较特殊，不能使用new，否则报错

##### Object 子类型
1. Date(日期)，日期对象
2. Array/Typed Arrays(数组/类型数组)，数组对象
3. 键控集: Maps, Sets, WeakMaps, WeakSets
4. 结构化数据: JSON
5. 标准库中更多的对象
6. ...

## 类型转换
|         | Null      | Undefined   | Boolean  | Number         | String         | Symbol    | Object   |
| :------ | :-------- | :---------- | :------- | :------------- | :------------- | :-------- | :------- |
| Boolean | false     | false       | -        | false(0/NAN)   | false('')      | true      | true     |
| Number  | 0         | NaN         | 1/0      | -              | StringToNumber | TypeError | 拆箱转换 |
| String  | 'null'    | 'undefined' | 'true'   | NumberToString | -              | TypeError | 拆箱转换 |
| Object  | TypeError | TypeError   | 装箱转换 | 装箱转换       | 装箱转换       | 装箱转换  | -        |

### StringToNumber
有**三种方法**转换，`Number`, `parseInt` 和, `parseFloat`, 其中`parseInt`比较特殊，因为ECMAScript 5 规定使用10，但是并不是所有的浏览器都遵循这个规定。因此，永远都要明确给出radix参数的值。在多数情况下用 `Number`进行类型转换是最好的选择，因为
`parseInt` 和, `parseFloat` 不支持科学记数法，并且会把非数字字符串转换为`NAN`。

### NumberToString
有**两种方法**转换`String` 和 `num.toString()`, 当number绝对值太大或太小，会转换为科学计数法字符串,保证字符串不会过长
⚠️
```JavaScript
999.toString() // TypeError

const num = 999
num.toString() // '999'

// or
(999).toString() // '999'
```

### 装箱转换
每一种基本类型`Number`, `String`, `Boolean`, `Symbol`，在对象中都有对应的类，**装箱转换**，就是把基本类型转换为对应的对象。

### 拆箱转换
拆箱转换和 装箱转换相反，把对象类型转换为基本类型, 其中`String` 和 `Number` 会先拆箱再转换，再从基本类型转换为对应类型，`Number`拆箱转换会尝试调用对象中的`valueOf`如果不存在则调用`toString`方法来获得基本类型(`String 调用顺序相反`)，如果它们都不存在，则转换失败抛出TypeError
```JavaScript
const o = {
    valueOf: () => {
        return 1
    },
    toString() {
        return 2
    }
}

console.log(Number(o)) // 1
console.log(String(o)) // '2'
```
再ES6还增加了`toPrimitive`方法来进行拆箱转换
```JavaScript
const o = {
    valueOf: () => {
        return 1
    },
    toString() {
        return 2    
    }
}

o[Symbol.toPrimitive] = () => 3 // 会覆盖 valueOf 和 toString

console.log(Number(o)) // 3
console.log(String(o)) // 3
```