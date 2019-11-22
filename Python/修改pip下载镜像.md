# 修改 pip 下载镜像地址

## 示例

- 国内几个常用的源镜像地址

> > 新版 ubuntu 要求使用 https 源

```b
清华：https://pypi.tuna.tsinghua.edu.cn/simple
阿里云：http://mirrors.aliyun.com/pypi/simple/
中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
华中理工大学：http://pypi.hustunique.com/
山东理工大学：http://pypi.sdutlinux.org/
豆瓣：http://pypi.douban.com/simple/
```

- 暂时修改

```bash
# pip 下载的时候添加-i参数
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspider
```

- 永久修改

> `windows` 下修改 `C:\Users\snowman\pip\pip.ini`，不存在就去新建
> `Linux` 下修改 `~/.pip/pip.conf`

```conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host=mirrors.aliyun.com
```
