---
title: JavaScript中不常用的api
date: 2019-01-23 14:48:53
tags: JavaScript
---
记录一些JavaScript中不常用的, 但又实用的api
<!-- more -->
# Array 篇
### every
测试数组内的元素是否全部通过,用户提供的测试函数, 返回`Boolean`
```javascript
arr.every(callback(element[, index[, array]])[, thisArg])
```
实例: 检测user数组中的年龄是否全部大于18岁
``` javascript
const arr = [
  { name: 'a', age: 10 },
  { name: 'b', age: 20 },
  { name: 'c', age: 25 },
]
arr.every((item) => item.age > 18) // false
```

### some
测试数组内的元素是否有一个通过(与`every`刚好相反), 用户提供的测试函数, 返回`Boolean`
```javascript
arr.some(callback(element[, index[, array]])[, thisArg])
```
实例: 检测user数组中的年龄是否有大于18岁的人
``` javascript
const arr = [
  { name: 'a', age: 10 },
  { name: 'b', age: 20 },
  { name: 'c', age: 25 },
]
arr.every((item) => item.age > 18) // true
```

### includes
检测数组内是否包含某个`值`, 返回`Boolean`
``` javascript
// 语法
arr.includes(searchElement[, fromIndex])
```

实例: 复杂或运算条件判断语句
```javascript
if (val === 'a' || val === 'b' || val === 'c') {
  // TODO
}
// 简化
if (['a', 'b', 'c'].includes(val)) {
  // TODO
}
```

### reduce
迭代数组并且执行用户提供的函数, 返回一个`值`
``` javascript
arr.reduce(callback[, initialValue])
```

### of
将所传入的参数转换为数组, 返回 `Array`
``` javascript
Array.of(element0[, element1[, ...[, elementN]]])
```
### from
迭代一个`arrayLike`对象, 返回`Array`, 与`map`相似, 单`map`只能作用与'Array', 而`from`可以作用与`arrayLike`对象比如: `String`, `arguments`
```
Array.from(arrayLike[, mapFn[, thisArg]])
```

# Object 篇

### keys & values
获取对象中所有的key 或者 value, 组成一个数组，返回`Array`
```javascript
Object.keys(obj)
Object.values(obj)
```

### entries
返回一个给定对象自身可枚举属性的键值对数组
```javascript
const obj = {
  name: 'lll',
  age: 42
}
Object.entries(obj) // [["name","lll"],["age",42]]
```
实例: 
```javascript
// 转换Map
new Map(Object.entries(obj))

// 遍历对象
for (let [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}
```

### hasOwnProperty
判断对象是否存在key
```
obj.hasOwnProperty(key)
```


# String 篇

### repeat
重复目标值次数， 返回`String`
```javascript
str.repeat(count);
```

### padEnd & padStart
填充字符串, 向目标字符之前或之后填充字符串
```javascript
str.padStart(targetLength [, padString])
```
example
```javascript
const phone = '13500000134'
const last4Digits = phone.slice(-4)
const maskedNumber = last4Digits.padStart(phone.length, '*') // *******0134
```

## Number篇

### Number.EPSILON
表示 1 与 `Number` 可表示的大于 1 的最小的浮点数之间的差值, 值接近于 2.2204460492503130808472633361816E-16，或者 2-52。
example 测试浮点数是否相当
```javascript
x = 0.2;
y = 0.3;
z = 0.1;
equal = (Math.abs(x - y + z) < Number.EPSILON);
```

