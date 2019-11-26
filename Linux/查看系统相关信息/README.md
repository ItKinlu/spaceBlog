# 查看系统相关信息

## 查看 Linux 系统版本的命令

- 方法 1

此命令也适用于所有的 Linux 发行版

```bash
cat /etc/issue
```

- 方法 2

这种方法只适合 Redhat 系的 Linux

```bash
cat /etc/redhat-release
```

- 方法 3

可列出所有版本信息

```bash
lsb_release -a
```

## 查看 Linux 内核版本命令

```bash
cat /proc/version
# 或者
uname -a
```
