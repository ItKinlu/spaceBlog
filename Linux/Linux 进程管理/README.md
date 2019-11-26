# Linux 进程管理

## 进程管理

- 通过端口号查看 pid

```bash
lsof -i:5000 # 查看在 5000 端口运行的进程
kill -9 pid # 通过pid杀死进程
cd /proc/pid # 通过pid查看进程 然后执行 `ls -ail`
```

- Linux 查看进程树

```bash
# 获取 gunicorn 进程树
pstree -ap | grep gunicorn
kill -9 [pid] # 退出进程
kill -HUP [pid] # 重启进程
```
