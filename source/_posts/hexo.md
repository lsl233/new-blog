---
title: hexo 搭建
date: 2016-01-11 2:53
tag: hexo node
---
[hexo](https://hexo.io/zh-cn/)是一款快速、简洁且高效的博客框架，Hexo 支持 GitHub Flavored Markdown 的所有功能，甚至可以整合 Octopress 的大多数插件。只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。
<!-- more -->

### 开始
安装hexo，hexo是基于node第三方模块，需要使用npm安装
```javascript
npm install hexo-cli -g
cd blog
hexo server
```
监测是否安装成功（查看hexo版本信息）
```javascript
hexo -v
```
初始化项目
```javascript
hexo init blog 　// 项目名字
```
进入 blog 目录， 安装依赖
```javascript
npm install
```
启动内置服务器,本地调试， 访问[http://localhost:4000/](http://localhost:4000/)
```javascript
hexo server
```

### 目录介绍
> * public是存放生成好的html，css，js等.
> * themes用于存放主题文件，hexo有很多第三方主题，可以配置各种样的主题， 主题中也会有主题。source>_posts 存放.md文件.
> * 我们的网页，就是基于mackdown语言生成的html， [mackdonw语法](https://www.zybuluo.com/mdeditor)参考。
> * _config.yml 配置文件， 所有的网站信息都从这里配置.

```
|____node_modules
|____public
|____scaffolds
|____source
|____themes
|____ _config.yml
|____ _config.yml.swp
|____ gitignore
|____ db.json
|____ package.json
```

### 安装主题
安装[next](http://theme-next.iissnan.com/)主题。
```
 git clone https://github.com/iissnan/hexo-theme-next themes/next
```
打开 _config.yml
```
theme: next
```
next主题又有三个外观Scheme， 进入themes>next>_config.yml
```
# scheme: Muse
# scheme: Mist
scheme: Pisces
```

### 连接github
安装hexo-deployer-git插件
```
npm install hexo-deployer-git --save
```
打开 _config.yml， 配置提交方式
```
deploy:
  type: git
  repo: git@github.com:<yourname>/blog.git
  branch: gh-pages
```
配置SSH keys
打开终端, 产看现有的SSH key， 如果没有会返回 No such file or directory
```
cd \~/. ssh
```
新建一个ssh key
```
ssh-keygen -t rsa -C "邮件地址@youremail.com"
```
会生成2个文件id_rea, id_rsa.pub, 打开id_rsa.pub复制id_rsa.pub，内容
然后打开，github仓库地址setting>deploy key>add deploy key
title: 随便填写
key: id_rsa.pub的内容

提交文件到github
```
hexo deploy
```
### 域名绑定
在域名管理控制台总

CNAME	www	默认	lsl233.github.io	--	10分钟		修改|暂停|删除|备注
A	@	默认	192.30.252.154	--	10分钟		修改|暂停|删除|备注
A	@	默认	192.30.252.153	--	10分钟		修改|暂停|删除|备注
在source中新建CNAME， 没有后缀名！写入你的顶级域名即可。

### changeLog
2016-12-25 12:07, coding托管 abc233.xyz 域名，国内访问更快。
