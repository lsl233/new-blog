---
title: Objective-C struct
date: 2019-09-18 10:42:00
tags:
---
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
