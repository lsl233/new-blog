---
title: GO基础知识总结
date: 2019-05-09 09:58:09
tags: 
    - GO
    - golang
    - 基础
---

关于GO的基础知识。

### GOPATH 与 GOROOT
GOROOT 是golang的安装路径
GOPATH 是工作目录，可以设置多个目录，
该目录下约定有三个子目录
1. src 源代码 （写代码目录）
2. pkg 编译后生成的文件
3. bin 编译后可执行的文件


### 包管理
go 的第三方包都是放在开源社区（目前支持：github、googlecode、bitbucket、Launchpad)）常用命令：
```
go get github.com/x/x // 获取包
go get -u // 自动更新包
```

`go get` 本质上可以理解为首先第一步是通过源码工具 clone 代码到 src 下面，然后执行 `go install`

go 包管理 与 Node 比起来是非常难用，包都统一放在工作目录的src目录下，并且第三方包没有版本管理概念，如果包更新没有做兼容处理，项目可能会GG

Go 在1.12后加入新的包管理工具 `mod`，下载的包会在 GOPATH/pkg内，主要解决一下问题
1. 自动下载包
3. 项目内会生成一个go.mod文件，列出包依赖

mod 也有坑，某些包会依赖 golang.org 上的包， 因为golang.org被强，导致下载失败，解决方法在 go.mod 文件中替换地址
```
replace (
	golang.org/x/crypto v0.0.0-20190308221718-c2843e01d9a2 => github.com/golang/crypto v0.0.0-20190308221718-c2843e01d9a2
	golang.org/x/net v0.0.0-20190503192946-f4e77d36d62c => github.com/golang/net v0.0.0-20190503192946-f4e77d36d62c
	golang.org/x/sys v0.0.0-20190215142949-d0b11bdaac8a => github.com/golang/sys v0.0.0-20190215142949-d0b11bdaac8a
	golang.org/x/sys v0.0.0-20190222072716-a9d3bda3a223 => github.com/golang/sys v0.0.0-20190222072716-a9d3bda3a223
	golang.org/x/text v0.3.0 => github.com/golang/text v0.3.0
)
```
因为github 会有同样的包，所以可以将 golang.org/x 替换为 github.com/golang