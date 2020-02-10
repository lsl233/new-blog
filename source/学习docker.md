---
title: 学习 docker
date: 2018-12-26 15:00:19
tags: docker
---
Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从Apache2.0协议开源。
<!-- more -->

Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。


### 镜像(Image)
###### 查看所有Image
```
docker images
docker image ls
```
###### 删除
```
docker image rm {Name|ID}
```
### 容器(Container)
###### 创建容器
```
docker run -it
```
`-t` 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上， `-i` 则让容器的标准输入保持打开

###### 停止、启动、杀死、重启一个容器
```
docker stop {Name|ID}
docker start {Name|ID}
docker kill {Name|ID}
docker restart {Name|ID}
```

###### 进入容器
```
docker attach ${ID}
```

###### 删除所有停止的容器
```
docker container prune
```
###### 退出容器
```
exit
```
退出容器后，容器就会自动停止了, 但是这个容器依然还存在，只是”关机“了
可以通过`ctrl+p`, `ctrl+q`，退出容器登入，而不关闭容器

###### 容器状态
```
docker ps -a
```

### 仓库(Repository)
