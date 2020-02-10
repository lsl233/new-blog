---
title: canvas 学习笔记
date: 2017-03-02 20:43:21
tags: canvas
---
<!-- more -->
canvas api

### 绘制矩形

`ctx.fillRect(x, y, w, h);` 绘制一个填充的矩形

`ctx.strokeRect(x, y, w, h);` 绘制一个矩形的边框

`ctx.clearRect(x, y, w, h);` 清除一个指定区域

### 绘制路径
绘制路径步骤，如下：
1. 创建路径起始点。
2. 画图命令去画出路径。
3. 把路径封闭。
4. 描边或填充路径区域来渲染图形。

`ctx.beginPath();` 新建一条路径，生成之后，图形绘制命令被指向到路径上生成路径。
`ctx.moveTo(x, y);` 移动画笔
`ctx.lineTo(x, y);` 绘制从当前上下文开始 ，到x，y 坐标。（可以有多个lineTo）
`ctx.closePath();` 闭合路径之后图形绘制命令又重新指向到上下文中。
`ctx.stroke();` 通过线条来绘制图形轮廓。
`ctx.fill();` 通过填充路径的内容区域生成实心的图形。

### 圆弧
`arc(x, y, radius, startAngle, endAngle, anticlockwise);` 画一个以（x,y）为圆心的以radius为半径的圆弧（圆），从startAngle开始到endAngle结束，按照anticlockwise给定的方向（默认为顺时针）来生成。
<div class="tip">
    arc()函数中的角度单位是弧度，不是度数。角度与弧度的js表达式:radians=(Math.PI/180)*degrees。
    <semantics><mrow><mstyle mathvariant="monospace"><mi>Math.PI</mi></mstyle><mo>=</mo><mi>π</mi><mo>≈</mo><mn>3.14159</mn></mrow></semantics>
</div>

`quadraticCurveTo(cp1x, cp1y, x, y);` 绘制贝塞尔曲线，cp1x,cp1y为控制点，x,y为结束点。
`bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)` 绘制二次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。

### 色彩 Colors
`ctx.fillStyle = color` 设置图形的填充颜色。
`ctx.strokeStyle = color` 设置图形轮廓的颜色。
<div class="tip">
    填充颜色必须在绘制之前使用, `fillRect` 或 `strokeRect`
</div>

### 透明度 Transparency
`globalAlpha = transparencyValue` 这个属性影响到 canvas 里所有图形的透明度，有效的值范围是 0.0 （完全透明）到 1.0（完全不透明），默认是 1.0。

### 线型 Line styles
`lineWidth = value` 设置线条宽度。
`lineCap = type` 设置线条末端样式。
`lineJoin = type` 设定线条与线条间接合处的样式。
`miterLimit = value` 限制当两条线相交时交接处最大长度；所谓交接处长度（斜接长度）是指线条交接处内角顶点到外角顶点的长度。
`getLineDash()` 返回一个包含当前虚线样式，长度为非负偶数的数组。
`setLineDash(segments)` 设置当前虚线样式。
`lineDashOffset = value` 设置虚线样式的起始偏移量。


