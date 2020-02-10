---
title: TypeScript接口
date: 2018-06-23 14:42:51
tags: JavaScript TypeScript
---
<!-- more -->
TypeScript的核心原则之一是对值所具有的结构进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。 在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。
```javascript
// 方式一
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

// 方式二
interface LabelledValue {
  label: string;
}
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}
```

###可选属性
接口里的属性不全都是必需的
```
interface SquareConfig {
  color?: string;
  width?: number;
}
```

###只读属性
```
interface Point {
    readonly x: number;
    readonly y: number;
}
```

###函数类型
```
interface SearchFunc {
  (source: string, subString: string): boolean;
}
const allle: SearchFunc = function (source, subString) {
    return true;
};
```

###可索引的类型
与使用接口描述函数类型差不多，我们也可以描述那些能够“通过索引得到”的类型，比如a[10]或ageMap["daniel"]。 可索引类型具有一个 索引签名，它描述了对象索引的类型，还有相应的索引返回值类型。 
```
interface StringArray {
  [index: number]: string;
}
```
共有支持两种索引签名：字符串和数字。

###类类型
```
// 检查静态
interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}
// 实例方法
interface ClockInterface {
    tick(): void;
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() { }
}
class AnalogClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() { }
}

let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```

###继承接口
```
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}
```