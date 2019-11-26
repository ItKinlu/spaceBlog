# Linux 安装 Python3

一般的 linux 系统都安装了 python2 不用管它 我们只是使用一下 python3 解释器而已

## 安装

- 安装依赖

为了避免后面的安装出问题，还是先将依赖安装一遍

```bash
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
```

- 下载 python3

可以自行官网下载放到服务器上，也可以通过 wget 来下载

```bash
wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
```

- 安装

```bash
# 创建安装路径文件夹
mkdir /usr/local/python3

# 解压下载包
tar -zxvf Python-3.6.1.tgz
cd Python-3.6.1
./configure --prefix=/usr/local/python3
make
make install
```

- 创建软链接并且加入到环境变量中

```bash
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
vim ~/.bash_profile
```

```bash_profile
# 新增该句
PATH=$PATH:$HOME/bin:/usr/local/python3/bin
```

```bash
# 重启环境变量
source ~/.bash_profile
```

- 完成 命令行输入

```bash
python3
pip3
```
