---
title: NodeJS相关镜像设置
---

## 查看当前镜像

```bash
npm config get registry
yarn config get registry
```

## 设置某个包的下载镜像

比如 `express`，临时镜像

```bash
npm --registry https://registry.npm.taobao.org install express
yarn save express --registry https://registry.npm.taobao.org
```

## 永久设置

```bash
npm config set registry https://registry.npm.taobao.org
yarn config set registry https://registry.npm.taobao.org
```

## 设置 electron 镜像地址

```bash
npm config set electron_mirror https://npm.taobao.org/mirrors/electron/
yarn config set electron_mirror https://npm.taobao.org/mirrors/electron/
```

## 通过配置文件修改镜像地址

修改~/.npmrc 文件

```.npmrc
registry=https://registry.npm.taobao.org
electron_mirror=https://npm.taobao.org/mirrors/electron/
```

修改 ~/.yarnrc

```.yarnrc
registry "https://registry.npm.taobao.org"
electron_mirror "https://npm.taobao.org/mirrors/electron/"
```

## npm 下载权限问题

```bash
npm install electron --unsafe-perm=true
```

## 显示下载进度

通过`--verbose`参数显示下载进度

```bash
npm install --verbose electron
yarn add --verbose electron
```

## 获取 npm 设置

```bash
npm config ls # 获取所有 npm 配置
npm config get registry
yarn config get registry
```
