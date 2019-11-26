---
title: 简单搞搞 Docker
tags:
  - Linux
addrlink: 20190607091022
date: 2019-06-07 09:10:22
---

[阿里云 docker 镜像](http://mirrors.aliyun.com/docker-toolbox/windows/docker-toolbox/)

[windwos 安装参考地址](https://blog.csdn.net/vitaair/article/details/80894890)

## windwos && Docker Toolbox

- 创建带有 docker 的虚拟机

```bash
docker-machine create --engine-registry-mirror=https://jn9it6kd.mirror.aliyuncs.com -d virtualbox default
```

- 修改镜像源

  1. 执行 `docker-machine ssh [machine-name]` 进入 VM bash
  2. sudo vi /var/lib/boot2docker/profile` # 在这里可以查看使用的镜像地址
  3. 在
     `--label provider=virtualbox`的下一行添加:
     `--registry-mirror https://xxxxxxxx.mirror.aliyuncs.com`
  4. 重启 docker

  - 虚拟机下执行 `sudo /etc/init.d/docker restart`
    或者
  - windows 下命令行执行 `docker-machine restart`

- ssh 工具登录

使用 `docker-machine` 创建的虚拟机上的 docker，可以使用 ssh 工具登录
用户名: docker
密码: tcuser

## docker 常用命令

```bash
# 从远程仓库拉取镜像
docker pull ${name:version}

# 查看已安装的镜像
docker image ls
docker images ${name}
```

## 运行 nginx

```bash
# -i 以交互模式运行容器，通常与 -t 同时使用
# -t 为容器重新分配一个伪输入终端，通常与 -i 同时使用
# -p 参数将一个docker主机的端口映射到容器中
# -it 参数一般连用，在docker run 启动一个容器后提供一个容器的终端，如果容器中没开启shell进程，也无法对容器进行交互
docker run -it -p 8848:80 nginx:1.15
```
