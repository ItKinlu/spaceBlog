# Git 常用命令

## 本地新建非 master 分支到远程仓库

```bash
git branch 分支名 # 新建本地分支
git push origin 分支名 # 将本地分支提交到远端
git push origin 分支名:master #将分支代码提交到 远端master
# 示例
git branch v2.0 # 新建分支
git checkout v2.0 # 切换分支
git push origin v2.0 # push到远程仓库
git checkout 分支名 # 本地分支之间切换

git push origin -d 分支名 # 删除远端分支
git branch -d 分支名 # 本地分支
git branch -r # 查看远端分支
git branch # 查看本地分支
git branch -a # 查看所有分支（本地+远端）
```

## 同步远端仓库到本地

```bash
git branck -a # 查看远端仓库分支
git checkout -b v2 origin/v2 # 新建本地分支和远端分支同名

git add *
git commit -m "update" # master 代码提交

git checkout v2 #切换到本地分支 v2
git pull # 拉取最新代码

git merge master # 切换到v2 后 合并master 分支代码到 v2

git branch -vv # 查看本地分支和远端分支对应情况
```

## 提交本地分支代码到远端

先拉取 git pull
然后提交
git push origin v2:v2

对于已经修改提交过的注释，如果需要修改，可以借助 git commit --amend 来进行。

## Git 忽略文件

通过 `.gitignore` 来忽略文件

如果要忽略的文件已经提交到了仓库中，需要使用

```bash
# 成功将git仓库中的 文件删除 并保留文件在本地
git rm -r --cached
```

删除本地仓库文件

```bash
git rm 文件名称
```

删除本地仓库中文件夹，这里 r 代表递归所有文件和文件夹

```bash
git rm -r 文件夹名称
```

保留本地文件，删除仓库里的文件

```bash
git rm --cached file_name # 本地会保留，仓库里会删掉
```

将删除文件缓存

```bash
git add -u
```

## 帮助命令

```bash
git rm -h
```

## 远程仓库改名本地如何修改

方法 1

```bash
git remote set-url origin git@gitee@xx.git
```

方法 2

```bash
git remote rm origin
git remote add origin git@gitee@xx.git
```

## 查看远程仓库地址

```bash
git remote -v
# origin  git@gitee.com:verlight/demo.git (fetch)
# origin  git@gitee.com:verlight/demo.git (push)
```

## git 大小写

```bash
# 设置大小写敏感(不推荐设置)
git config core.ignorecase false

# 可以通过以下命令来修改
git mv Date.vue date.vue
```

## 回滚到任意版本

```bash
git log -3 # 显示几条提交的log
git reset --hard e377f60e28c8b84158 # 回滚到指定版本
```
