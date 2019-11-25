# Flask 部署

采用 supervisor + gunicorn 运行方式

## gunicorn 运行

- 添加 `.sh` 脚本文件，启动 `gunicorn` 文件内容如下

```sh
#!/bin/sh
source ./venv/bin/activate
export a='one'
export b='two'
exec gunicorn -c gunicorn.conf run:app
exec gunicorn -c gunicorn.conf run:app
# exce gunicorn -c gunicorn.conf -preload run:app --log-level=debug
exec .venv/bin/gunicorn -c ./gunicorn.conf run:app
```

> 这需要注意脚本文件的保存格式为 unix 格式

```sh
vim ./start.sh
:set ff # 可看到dos或unix的字样，如果是 dos 则需要修改为 unix
set ff=unix
```

- 在脚本文件中添加应用需要的环境变量

- 启动 `sudo sh ./start.sh`
  > 这里并不是后台运行，我们发现命令行并没有退出去，所需要使用 `supervisor` 来管理

## supervisor

- 安装

```sh
# centos 7
yum install supervisor
# 安装完成后就会有 supervisor 系列命令

# ubuntu
pip3 install supervisor
```

- 修改配置文件

默认配置文件地址 `/etc/supervisord.conf`中

```conf
# 在默认配置文件下添加
[include]
files =/etc/supervisord.d/*.conf
```

- 我们的自定义配置文件就放在 `/etc/supervisord.d/` 目录下

```conf

[program:es]
command= node /home/snow/node-demo/index.js
user=root
stdout_logfile=/var/log/supervisor.log
autostart=true
autorestart=true
startsecs=60
stopasgroup=true
ikillasgroup=true
startretries=1
redirect_stderr=true
```

- 启动 `supervisor`

```bash
# -c 指定配置文件地址
# 一定要提前看配置文件在哪
# centos 7
supervisord -c /etc/supervisord.conf
# unbutu
supervisord -c /etc/supervisord.conf
```

启动后可以使用 `supervisorctl` 来查看管理的应用列表，以及更新重启之类操作
supervisorctl 是 supervisord 的命令行客户端工具

```bash
supervisorctl # 可以进入到一个命令行程序管理应用
supervisorctl status # 查看所有进程的状态
supervisorctl stop [app_name] # 停止应用
supervisorctl start [app_name] # 启动应用
supervisorctl restart [app_name] # 重启应用
supervisorctl update # 配置文件修改后可以使用该命令加载新的配置
supervisorctl reload #  重新启动配置中的所有程序
supervisorctl tail -f program_name # 查看应用日志
# 可以 supervisorctl 进入到命令行应用,可以直接使用以下命令
status
stop [app_name]
stop all # 停止所有应用
...
```

部署 `gunicorn` 一定要设置 `daemon` 为 `'false'`
