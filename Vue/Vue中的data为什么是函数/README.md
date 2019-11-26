# Vue 中的 data 为什么是函数

## 示例代码

`Vue` 中的 `data` 为什么是函数？
组件是可复用的 `Vue` 实例，一个组件被创建好之后，就可能被多次引用，而组件不管被复用了多少次，组件中的 `data` 数据都应该是相互隔离，互不影响的，基于这一理念，组件每复用一次， `data` 数据就应该被复制一次，之后，当某一处复用的地方组件内 `data` 数据被改变时，其他复用地方组件的 `data` 数据不受影响，所以为了保证复用性，组件的 `data` 就必须是一个函数，因为函数是一个独立的作用域，每次调用函数，就会有一个新的空间，返回一份新的 `data`

```html
<template>
  <div class="title">
    <h1>按钮被点击了{{ count }}次</h1>
    <button v-on:click="count++">点击</button>
  </div>
</template>
<script>
  export default {
    name: "BtnCount",
    data() {
      return {
        count: 0
      };
    }
  };
</script>
<style scoped>
  .title {
    background-color: red;
  }
</style>
```
