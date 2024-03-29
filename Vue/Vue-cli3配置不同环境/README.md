# Vue-cli3 配置不同环境

## 根据配置文件

根据配置文件区分不同的环境

我们在项目根目录创建如下文件:

`.env.development` 和 `.env.production` 和 `.env.test`

每个文件的内容

`.env.development`

```js
// VUE_APP_CURRENTMODE 当前环境变量
VUE_APP_CURRENTMODE = "development";
// 或者可以设置为
NODE_ENV = "development";

VUE_APP_LOGOUT_URL = "自己的地址 ";
VUE_APP_PARAMS = "自定义的参数";
```

`.env.production`

```js
// VUE_APP_CURRENTMODE 当前环境变量
VUE_APP_CURRENTMODE = "production";
// 或者可以设置为
NODE_ENV = "production";

VUE_APP_LOGOUT_URL = "自己的地址 ";
VUE_APP_PARAMS = "自定义的参数";
```

...

## 如何进入我们定义环境

```json
"serve": "vue-cli-service serve --mode development",
"build": "vue-cli-service build --mode production",
```

## 在应用中如何访问环境中的定义的变量

```js
const { NODE_ENV, VUE_APP_PARAMS } = process.env;
console.log(NODE_ENV); // development
```
