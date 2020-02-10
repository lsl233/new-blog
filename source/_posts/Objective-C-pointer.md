---
title: Objective-C 临时笔记
date: 2019-09-19 12:19:24
tags:
---

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


