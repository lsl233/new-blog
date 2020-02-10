---
title: TypeScript基础类型
date: 2018-06-25 20:42:51
tags: JavaScript TypeScript
---
<!-- more -->

### 布尔值 boolean

### 数字 number

### 字符串 string

### 数组 元素类型[]，Array<元素类型>

### 元祖Tuple
元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同

### 枚举 enum
枚举类型可以为一组数值赋予友好的名字。
```javascript
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green; // 2
//
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2] // Green;
```
### Any
### Void
void类型像是与any类型相反，它表示没有任何类型
###Null 和 Undefined
TypeScript里，undefined和null两者各自有自己的类型分别叫做undefined和null。 和 void相似，它们的本身的类型用处不是很大。
### Never
never类型表示的是那些永不存在的值的类型。
```javascript
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

### 联合类型
联合类型(union types)表示取值可以为多个类型中的一种。
```
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
```

###类型断言
通过类型断言这种方式可以告诉编译器，“相信我，我知道自己在干什么”。 类型断言好比其它语言里的类型转换，但是不进行特殊的数据检查和解构。 它没有运行时的影响，只是在编译阶段起作用。
类型断言不是类型转换，断言成一个联合类型中不存在的类型是不允许的：

###类型别名
类型别名用来给一个类型起个新名字。
```
type Name = string;
type NameResolver = () => string;
```
###字符串字面量类型
字符串字面量类型用来约束取值只能是某几个字符串中的一个。
```
type EventNames = 'click' | 'scroll' | 'mousemove';
```