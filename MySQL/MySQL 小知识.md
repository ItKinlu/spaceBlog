---
title: MySQL 小知识
tags:
  - MySQL
abbrlink: 201905151800
date: 2019-05-15 18:00:28
---

socket 文件：当用 Unix 域套接字方式进行连接时需要的文件

pid 文件：MySQL 实例的进程 ID 文件

MySQL 表结构文件：用来存放 MySQL 表结构定义文件

## 套接字文件

Unix 系统下本地连接 MySQL 可以采用 Unix 域套接字方式，这种方式需要一个套接字（socket）文件。套接字文件可由参数 socket 控制。一般在 `/tmp` 目录下，名为`mysql.sock`

```bash
# 登录到 MySQL 通过以下命令查看 socket 文件地址
show variables like 'socket'\G
```

## pid 文件

当 MySQL 实例启动时，会将自己的进程 ID 写入一个文件中，该文件即为 pid 文件。该文件可由参数 pid_file 控制。默认路径位于数据库目录下，文件名为`主机名.pid`

```bash
# 登录 MySQL 使用以下面命令可以查看 pid 文件地址
show variables like 'pid_file'\G
```
