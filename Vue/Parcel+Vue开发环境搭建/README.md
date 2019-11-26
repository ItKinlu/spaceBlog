---
title: Parcel + Vue 开发环境搭建
tags:
  - Vue
abbrlink: 201803151259
date: 2018-03-15 12:59:16
---

`Parcel.js` 是极速零配置 Web 应用打包工具，搭建 `Vue` 开发环境

## 安装

- 安装

```bash
npm install -g parcel-bundler
```

## 使用

既然是零配置打包工具，那么也就不需要配置文件，Parcel 自动分析这些文件中引用的依赖关系，并将其包含到输出包(output bundle) 中

- 新建项目并且安装相关依赖

```bash
npm init -y
npm install parcel-bundler parcel-plugin-vue babel-preset-env less  --dev
# 其中parcel-plugin-vue 是用来编译vue文件的
```

- 添加 babel 配置文件

```babel
//.babelrc

{
  "presets": [
    ["env"]
  ]
}
```

- 新建 index.html 并且引入相关依赖库，html 通常是使用 parcel 进行编译的入口

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width,user-scalable=no,initial-scale=1,maximum-scale=1,minimum-scale=1"
    />
    <title>parcel-vue-demo</title>
  </head>
  <body>
    <app></app>
    <script src="./src/index.js"></script>
  </body>
</html>
```

- 配置项目 src 目录

```txt
# 路径结构
src
├── app.vue
├── index.js
├── index.less
├── router.js
└── views
    ├── detail.vue
    └── index.vue
```

- 编辑入口文件 index.js

```js
import Vue from "vue";
import App from "./App";
import router from "./router";

// parcel 针对于css预处理语言，会自动安装不同的解析器进行解析
import "./index.less";

new Vue({
  router,
  el: "app",
  render: h => h(App)
});
```

- 更改`package.json` 中 `scripts` 字段，脚本

```json
 "scripts": {
    "dev": "parcel index.html",
    "build": "parcel build index.html --public-url /"
  },

```
