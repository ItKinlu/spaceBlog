---
title: wget 和 curl
tags:
  - Linux
addrlink: 201805191119
date: 2018-05-19 11:19:00
---

wget 和 curl 区别：

`wget` 是一种下载工具，`wget` 是个专职的下载利器，简单，专一，极致；是 `Linux` 最常用的下载命令。

`curl` 是比 `wget` 工具功能更加丰富的工具，`curl` 是一个利用 `URL` 规则在命令行下工作的文件传输工具，可以说是一款很强大的 `http` 命令行工具。它支持文件的上传和下载，是综合传输工具。

wget 使用
一般的使用方法是: wget + 空格 + 要下载文件的 url 路径

下载文件

```bash
# O大写，不用O只是打印内容不会下载
curl -O http://man.linuxde.net/text.iso

# 不用参数，直接下载文件
wget http://www.linuxde.net/text.iso
```

下载文件并重命名

```bash
# o小写
curl -o rename.iso http://man.linuxde.net/text.iso
# O大写
wget -O rename.zip http://www.linuxde.net/text.iso
```

断点续传

```bash
# C大写
curl -O -C -URL http://man.linuxde.net/text.iso
# c 小写
wget -c http://www.linuxde.net/text.iso
```

显示响应头部信息

```bash
curl -I http://man.linuxde.net/text.iso
wget --server-response http://www.linuxde.net/test.iso
```

打包下载网站

```bash
wget --mirror -p --convert-links -P /var/www/html http://man.linuxde.net/
```
