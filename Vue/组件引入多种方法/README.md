# 组件引入的多种方法

## 示例代码

- `vue-router` 懒加载
- `vue 打包优化` 加载动画

当使用 webpack 打包构建应用时，JavaScript 包会变得非常大，影响页面加载。如果我们能把不同路由对应的组件分割成不同的代码块，然后当路由被访问的时候才加载对应组件，这样就更加高效了。

结合 vue 的异步组件 和 webpack 代码分割，可以实现路由组件的懒加载

- 将路由所对应的组件定义成异步加载结合 webpack 代码分割功能

```js
const NotFound = resolve => {
  // 结合 webpack 的代码分割函数 require.ensure() 来使用
  require.ensure(["@/components/404.vue"], () => {
    resolve(require("@/components/404.vue"));
  });
};
```

- vue 2.3.0 + vue-router 2.4+ 版本中使用如下引入方法

```js
const NotFound = () => ({
  // import('').then() 方法，es6原生的异步引入方法
  component: import("@/component/404.vue"),
  loadding: loading, // 组件加载ing的软件
  error: errorComponent, // 组件加载失败用显示的组件
  delay: 200
});
```

- 另外一种代码分块的语法，使用 AMD 风格的 require，更加简单

```js
const NotFound = resolve => require(["@/components/404.vue"], resolve);
```

- 一般一个路由下会有多个组件，或者组件下有多个子组件，这里就需要把组件按组分块了。

把某个路由下的所有组件都打包在同个异步 chunk 中。只需要给 chunk 命名，提供 require.ensure 第三个参数作为 chunk 的名称：

```js
const NotFound = r =>
  require.ensure([], () => r(require("@/components/404.vue")), "notfound");
```

Webpack 将相同 chunk 下的所有异步模块打包到一个异步块里面 —— 这也意味着我们无须明确列出 require.ensure 的依赖（传空数组就行）。

组件加载 ing 显示 loading

以 mint-ui 的 loading 为例

```js
import { Indicator } from "mint-ui";
const NotFound = resolve => {
  Indicator.open();
  require.ensure(["@/components/404.vue"], () => {
    resolve(require("@/components/404.vue"));
    Indicator.close();
  });
};
```
