---
title: Objective-C 知识点
date: 2019-09-17 10:48:13
tags: Objective-C
---

Objective-C 是 C 的超集，所以任何 C 语言代码都可以通过 Objective-C 编译器的编译，在 Objective-C 中使用 C 语言代码也是完全可以的。Objective-C 是在 C 的基础上加入了面向对象的特性，语法又源于`Smalltalk`消息传递风格。所有其他非面向对象的语法，包括变量类型，预处理器（preprocessing），流程控制，函数声明与调用皆与C语言完全一致。

## 引用类型
### 类 class
`OC` 中 Class 的语法与其他语言如 Java JavaScript C# 的语法大不相同, 但是其表达的意思都大同小异。

### 定义Interface
RPoint.h
```Objective-C
@interface RPoint : NSObject

@property int x;
@property int y;

-(void) print;

@end
```
`@interface` 定义一个接口
`RPoint` 接口名
`RPoint : NSObject` 继承`NSObject`类
`@property` 定义一个属性，对象状态
`-(void)` 定义一个方法，对象行为，实例方法
`@end` 与`@interface`对应。

属性可以添加属性描述
```Objective-C
@property (Attribute) int x;
```
1. 读写特性
    * readwrite (默认)
    * readonly（只读）
2. 多线程特性
    * atomic（默认 原子性）
    * nonatomic (非原子性)
3. 内存管理
    * strong（默认 强引用）
    * weak（弱引用 阻止循环引用）
    * copy （拷贝属性 创建独立拷贝）
    * retain


### 实现Interface
RPonit.m
```Objective-C
#import <Foundation/Foundation.h>
#import "RPoint.h"

@implementation RPoint

-(void) print {
    NSLog(@"[%d, %d]", self.x, self.y);
}

@end
```
实现接口中定义的方法
`self` 当前对象实例

### 声明方法
所有方法默认是公有方法，没有私有方法（可以通过其他方法实现）

实例方法，实例方法中可以通过`self`关键字访问实例属性、变量、方法
```Objective-C
-(void) print;
```

类型方法(静态方法)中，不能通过`self`访问实例属性、变量、方法
```Objective-C
+(void) print;
```
带1个参数
```Objective-C
-(void) print: (int) val
```
多个参数
```Objective-C
-(void) print: (int) val toVal: (int) val
```

### 使用
main.m
```Objective-C
#import <Foundation/Foundation.h>
#import "RPoint.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        RPoint *rp1 = [[RPoint alloc] init]; // 1
        
        // 设置属性
        rp1.x = 10; // or [rp1 x];
        rp1.y = 10;
        
        // 访问属性
        [rp1 print]; // [10, 10]
        [rp1 x]; // or rp1.x，方法不能使用这种方式
    }
    return 0;
}
```
1. 创建对象，`[RPoint alloc]` 内存分配，`[RPoint alloc]`的返回值再调用 `init` 初始化。
- alloc 手动请求堆内存
- 在OC中调用方法又叫，给对象传递消息


#### 数据成员 data member
描述对象状态
1. 实例变量 instance variable
2. 属性 property

#### 函数成员 function member
描述对象行为
1. 方法 method
2. 初始化器 init
3. 析构器 dealloc

### 指针 pointer
### 块 block

## 值类型
### 基础数据类型
### 结构 struct
结构和Class很像，但是他们有几点不同
1. 结构不能定义方法
2. 语法不同
3. Class是引用类型，struct是值类型

### 定义一个结构
SPoint.h
```Objective-C
typedef struct {
    int x;
    int y;
}SPoint;
```

### 使用
main.m
```Objective-C
#import <Foundation/Foundation.h>
#import "SPoint.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        SPoint sp1;
        sp1.x = 10;
        sp1.y = 20;
    }
    return 0;
}
```

### 枚举 enum

## 类型装饰
### 协议 protocal
### 类别 category
### 扩展 extension



### 合并字符串

```Objective-C
NSString text = "文字";
[NSString stringWithFormat:@"合并%@", text];
```

### 窗口大小
```Objective-C
self.view.bounds
```

### 绑定事件
```Objective-C
[self.button addTarget:self action:@selector(clickButton:) forControlEvents:UIControlEventTouchUpInside];
```


