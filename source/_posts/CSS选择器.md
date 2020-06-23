---
title: CSS选择器
date: 2016-04-04 10:54:22
tags:
    - CSS
    - 选择器
    - 基础
---
CSS 选择器总结
<!-- more -->

CSS 选择器根据 MDN 分类，共分为**5**大类
1. 简单选择器（Simple selectors）：通过元素类型、class 或 id 匹配一个或多个元素。
2. 属性选择器（Attribute selectors）：通过 属性 / 属性值 匹配一个或多个元素。
3. 伪类（Pseudo-classes）：匹配处于确定状态的一个或多个元素，比如被鼠标指针悬停的元素，或当前被选中或未选中的复选框，或元素是DOM树中一父节点的第一个子节点。
4. 伪元素（Pseudo-elements）:匹配处于相关的确定位置的一个或多个元素，例如每个段落的第一个字，或者某个元素之前生成的内容。 
5. 组合器（Combinators）：这里不仅仅是选择器本身，还有以有效的方式组合两个或更多的选择器用于非常特定的选择的方法。例如，你可以只选择divs的直系子节点的段落，或者直接跟在headings后面的段落。
6. 多重选择器（Multiple selectors）：这些也不是单独的选择器；这个思路是将以逗号分隔开的多个选择器放在一个CSS规则下面， 以将一组声明应用于由这些选择器选择的所有元素。

其中 伪类（Pseudo-classes）又可分为 **3** 类
1. 关系伪类选择器：根据与其他元素的关系选择元素。
2. 行为伪类选择器：更具用户行为选择元素。
3. 逻辑选择器：根据条件排除元素。

详细请看脑图 [CSS选择器](http://naotu.baidu.com/file/41b2afa65cc0743a9ba5c46e553dfb0c?token=2cf87eda49d6cf9b)

> [MDN](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Introduction_to_CSS/Selectors)