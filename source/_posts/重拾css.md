﻿---
title: 重拾css，长度单位
date: 2016-07-20 21:37:37
tags: css
---
css中的长度单位主要分为2大类
<!-- more -->
### 绝对长度单位
1. 英寸<in>
2. 厘米<cm>
3. 毫米<mm>
4. 点<pt>： 是一种标准印刷度量单位
5. 派卡<pc>：一种印刷术语

### 相对长度单位
1. ex ： 相对与字符中```x```的高度（可用于模仿sup、sub 上标，下标）， 
2. ch ： 相对与字符``0``的宽度
3. em ： 1个‘em’ 等于 字体的font-size值（font-size=14px， 1em=14px）
4. rem ： 相对于根元素的字体大小 r代表根元素
5. vh : 相对于视口宽度 1vh = 1%的视口高度（浏览器高度是900px, 1vh = 900 * 1% = 9px) 100vh = 视口高度。
6. vw : 和vh相同，没什么特别的。
7. vmin : 相对于vw和vh中最小的值。
8. vmax : 与vmin相同。

px ： px（像素）这个单位，在```<<CSS权威指南第三部>>```中是归类于相对长度单位，相对于用户屏幕的分辨率，但在网络上有些[文章](http://www.w3cplus.com/css/the-lengths-of-css.html)都将px归类于绝对长度单位，很纠结···。 在web中px是基础的长度单位，其他em， rem ··· 都会转换为px处理，javascript获取元素长度单位也是px

[检测css浏览器支持程度](http://caniuse.com/)
> * [em 与 rem 区别](https://jsfiddle.net/lsl233/jjqyzhsb/)
