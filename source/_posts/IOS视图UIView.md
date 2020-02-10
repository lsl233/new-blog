---
title: IOS View 笔记
date: 2019-09-19 17:58:26
tags:
---

## View（展示）

### UIView
最基础的视图类，作为各种视图类型的父类，提供基础的能力。

使用

```Objective-C
UIView *view = [[UIView alloc] init];
view.backgroundColor = [UIColor redColor];
view.frame = CGRectMake(100, 100, 100, 100);

[self.view addSubview:view];
```
### 声明周期

1. willMoveToSuperview

2. didMoveToSuperview

3. willMoveToWindow

4. didMoveToWindow



## Controller（管理）

### UIViewController
视图控制器，所有控制器的父类，管理视图View层级结构，自身也包含一个View，包含一个多个View的容器

### 声明周期
1. init 初始化
显示
2. viewDidLoad （适合进行所有View初始化工作）
3. viewWillAppear
4. viewDidAppear
销毁
5. viewWillDisappear
6. viewDiddisappear
7. Dealloc

### UITabBarController
管理 UIViewController 切换

### UINavigationController
通过栈管理页面，控制页面切换


### UITableView
纵向布局，一行一个视图


### UICollectionViwe
纵向于横向布局，一行可以多个视图，比UITableView更灵活

minimumInteritemSpaceing 最小间距


