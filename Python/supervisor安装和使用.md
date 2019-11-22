# supervisor 的安装和使用

## centos7 安装

```bash
yum install epel-release
yum install -y supervisor
systemctl enable supervisord # 开机自启动
systemctl start supervisord # 启动 supervisord 服务

systemctl status supervisord # 查看supervisord服务状态
ps -ef | grep supervisord # 查看是否存在supervisord进程

```

## Ubuntu 安装

```bash
sudo apt-get install supervisor # 安装
```

## 配置文件

`/etc/supervisor/conf.d/` 配置文件路径，一般安装成功就会生成这个目录

## supervisorctl 相关命令

> `supervisord` 服务启动后，可以使用 `supervisorctl` 来启动管理相关应用

```bash
supervisorctl # 进入到 supervisorctl 命令控制界面面
update # 更新新的配置到supervisord（不会重启原来已运行的程序）
reload # 载入所有配置文件，并按新的配置启动、管理所有进程（会重启原来已运行的程序）
start xxx # 启动某个进程
restart xxx # 重启某个进程
stop xxx # 停止某一个进程(xxx)，xxx为[program:theprogramname]里配置的值
stop groupworker # 重启所有属于名为groupworker这个分组的进程(start,restart同理)
stop all # 停止全部进程，注：start、restart、stop都不会载入最新的配置文件
reread # 当一个服务由自动启动修改为手动启动时执行一下就ok
```
