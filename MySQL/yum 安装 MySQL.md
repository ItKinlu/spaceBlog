---
title: yum 安装 MySQL
tags:
  - Linux
  - MySQL
abbrlink: 201905141700
date: 2019-05-14 17:00:28
---

```bash

# 查询是否安装mysql
rpm -qa | grep mysql

# 下载源需要下载
wget -i -c https://repo.mysql.com/mysql57-community-release-el7.rpm

# 使当前源生效
yum -y install mysql57-community-release-el7.rpm

# 通过yum安装
yum -y install mysql mysql-server

# 安装
yum -y install mysql-community-server

```

## 数据库设置

```bash
# 启动 MySQL
systemctl start mysqld.service

# 查看 MySQL 运行状态
systemctl status mysqld.service

# 找到默认root用户密码
grep "password" /var/log/mysqld.log

# 使用默认密码登录root用户
mysql -u root -p

# 修改 root 密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
```

## 移除我们下载的 yum 源

```bash
yum -y remove mysql57-community-release-el7.rpm
```

## 设置开机启动

```bash
systemctl enable mysqld
systemctl daemon-reload
```

## 授权远程访问

```bash
grant all privileges on *.* to root@'%' identified by "password";
flush privileges;
```
