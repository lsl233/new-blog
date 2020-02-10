---
title: koa 中 ejs 配置
tag: koa ejs 外部函数
date: 2016-01-24 19:42:50
---
<!-- more -->
```javascript
var koa = require('koa');
var render = require('koa-ejs');

var app = koa();
render(app, {
  root: path.join(__dirname, 'view'),
  layout: 'template',
  viewExt: 'html',
  cache: false,
  debug: true,
  locals: locals,
  filters: filters
});

app.use(function *() {
  yield this.render('user');
});

app.listen(7001);
```

* root: view root directory.
* layout: global layout file, default is layout, set false to disable layout.
* viewExt: view file extension, default is html.
* cache: cache compiled function flag.
* debug: debug flag.
* locals: global locals, can be function type, this in the function is koa's ctx.
* filters: ejs custom filters.
* open: open flog.
* close: close floag.
