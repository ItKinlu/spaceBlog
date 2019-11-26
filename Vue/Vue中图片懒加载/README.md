# Vue 图片懒加载

使用 `vue-lazyload` 完成图片懒加载

## 安装

```bash
npm install vue-lazyload --save
# 或者
yarn add vue-lazyload
```

## 使用

在入口文件中引用并且使用

```js
import VueLazyLoad from "vue-lazyload";
Vue.use(VueLazyLoad, {
  error: "./static/error.png",
  loading: "./static/loading.png"
});
```

模板文件中将需要懒加载的图片绑定 `v-bind:src` 修改为 `v-lazy`

```html
<img class="image" v-lazy="~@/assets/img/img.png" />
```
