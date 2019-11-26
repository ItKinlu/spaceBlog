---
title: MySQL 基本使用
tags:
  - MySQL
abbrlink: 201905151700
date: 2019-05-15 17:00:28
---

## 启动停止

```bash
net start mysql
```

## 连接

```bash
mysql -u username -p # 本机
mysql -h110.110.110.110 -uusername -p #远程
```

## 创建库

[参考地址](https://www.cnblogs.com/jiangxiaobo/p/7089345.html)

## 创建表

## 备份

```bash
# 备份一个数据库
mysqldump -u username -p 数据库名 > backup.sql

# 备份数据库下的person的表
mysqldump -u rusername -p 数据库名 表名 > backup.sql
```

## 恢复备份

```bash
# 恢复某个数据库
mysql -uusername -p 数据库名 < 备份文件.sql
```

[参考地址 1](https://www.cnblogs.com/chenqionghe/p/4848424.html)
[参考地址 2](https://www.cnblogs.com/kissdodog/p/4174421.html)
