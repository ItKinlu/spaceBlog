# linux 小知识

## Linux 软件安装工具

rpm 包和 deb 包是两种 Linux 系统下最常见的安装包格式
rpm 包主要应用在 RedHat 系列包括 Fedora 等发行版的 Linux 系统
deb 包主要应用于 Debian 系列包括现在比较流行的 Ubuntu 等发行版上

yum 可以用于运作 rpm 包，例如在 Fedora 系统上对某个软件的管理
apt-get 可以用于运作 deb 包，例如在 Ubuntu 系统上对某个软件的管理

## sudo 和 su

在 linux 系统中，由于 root 的权限过大，一般情况都不使用它。只有在一些特殊情况下才采用登录 root 执行管理任务，一般情况下临时使用 root 权限多采用 su 和 sudo 命令。
