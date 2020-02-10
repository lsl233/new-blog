---
title: Objective-C Class
date: 2019-09-18 10:11:37
tags: Objective-C Class 基础
---
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

### 初始化器
### 类型初始化器

