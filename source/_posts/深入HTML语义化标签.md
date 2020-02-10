---
title: 深入HTML语义化标签
date: 2019-03-27 21:55:57
tags: HTML
---

那些实际场景适合用哪些语义化标签呢？

<!-- more -->

### aside
表示一个和其余页面内容几乎无关的部分，是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。
使用场景: 侧边栏类容, 广告, 导航

### article
表示文档、页面、应用或网站中的独立内容，成为可独立分配的或可复用的结构。
使用场景: 用户提交的评论、交互式组件，或者其他独立的内容项目。


### hgroup
表示标题组
使用场景: 一个`h1`标题中有一个副标题`h2`

#### Examples
```html
<hgroup>
  <h1>Main title</h1>
  <h2>Secondary title</h2>
</hgroup>
```

> 本元素已经从HTML5（W3C）规范中删除，但是它仍旧在 WHATWG 的 HTML 版本里。大多数浏览器都部分地实现，所以它不太可能消失。
> https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/hgroup

### abbr
表示缩写
使用场景: WWW 是 World Wide Web 的缩写, 所以 WWW 应该使用 `abbr`标签, 并且还应该使用 `title` 属性描述完整描述
#### Examples

```html
<abbr title="World Wide Web">WWW</abbr>
```

### hr
表示段落级元素之间的主题转换
使用场景: 一个文章的一个章节或者故事内容发生变化时
⚠️: `hr` 表现形式是一个水平直线, 他不应该用作2个内容的分割，它的语义仅仅作用于文章
#### Examples
```html
<p>前段时间，网友晒出一组偶遇Angelababy与妈妈、婆婆带小海绵出游的照片。照片中，baby身穿白色上衣面带微笑，站在一旁看着正在玩耍中的小海绵，而小海绵穿着浅色上衣搭配深色运动裤，站在游乐球中央手指向前方，相当可爱。</p>
<hr />
<p>昨晚，甄子丹老婆汪诗诗在社交平台上称出席慈善活动时被主办单位歧视，且主办单位老板态度相当不尊重。汪诗诗直言：“他们对外国人和韩国人完全不同，态度好好，我觉得根本是歧视中国人”，最后一家三口提前离场，汪诗诗还自带话题“中国人不是东亚病夫”发文。</p>
```
> https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/hr

### strong
表示该元素包裹的内容很重要
使用场景: 需要着重提醒用户这段词或话很重要的时候
#### Examples
```html
<p><strong>周五 14:00</strong>考试</p>
```

### blockquote, q, cite
`blockquote` 表示段落级引述内容
`q` 表示行内引述内容
`cite` 表示引述作品名

### time
表示24小时制时间或者公历日期
#### Examples
```html
<p>The concert starts at <time>20:00</time>.</p>
```

### figure & figcaption
表示一段独立的内容, 经常与说明 `figcaption` 一起使用
使用场景: 一个图片，和图片标题或者说明
#### Examples
```html
<figure>
    <img src="/media/examples/elephant-660-480.jpg"
         alt="Elephant at sunset">
    <figcaption>An elephant at sunset</figcaption>
</figure>
```

### nav
表示页面中导航性质的内容
```html
<nav>
    <h2>table</h2>
    <ol start="7">
        <li>first item</li>
        <li>second item</li>
        <li>third item</li>
    </ol>
</nav>
```

### 其他
| 标签       | 说明                                                                  |
| :--------- | :-------------------------------------------------------------------- |
| small      | 之前表示字体缩小废弃标签，HTML5修改为补充评论                         |
| s          | 之前表示划线的废弃标签，HTML5表示错误内容，经常用于电商折扣之前的价格 |
| i          | 之前表示斜体的废弃标签，HTML5表示读的时候重读                         |
| b          | 之前表示黑体的废弃标签，HTML5表示关键字                               |
| u          | 之前表示下划线的废弃标签，HTML5表示避免歧义的注记                     |
| data       | 和time标签类似，给机器阅读的内容，意义广泛，可以自由定义              |
| var        | 变量，多用于计算机和数学领域                                          |
| kdb        | 用户输入，表示键盘按键                                                |
| sub, sup   | 上下标                                                                |
| bdi, bdo   | 指定语言的书写方向（左到右，右到左）                                  |
| mark       | 表示高亮，从读者角度希望高亮（与strong有区别）                        |
| wbr        | 表示换行位置，长用于英文                                              |
| *menu      | ul变体，在做功能菜单时使用                                            |
| dl, dd, dt | 一般出现在论文之类的文章，对术语进行定义                              |
| main       | 整个页面只出现一个，表示页面主要内容                                  |