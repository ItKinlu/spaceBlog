# Mixin 理解和使用

`Mixin` 是组件复用的一种方式

使用过 React 的都知道 React 中有高阶组件，高阶组件的作用就抽是象一些逻辑，达到组件复用的目的，而 Vue 中组件复用的方式就是 mixins

> 混入 (mixins) 是一种分发 Vue 组件中可复用功能的非常灵活的方式。混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被混入该组件本身的选项。

```js
export const commonMinxin = {
  data(){
    return {
      dataFirst:"1",
      dataSecond:"2"
    }
  },
  methods:{
    changeFirst(){
      ....
    }
  }
}

// App.vue 中 script
import {commonMinxin} from './';
export default {
  // 将我们预先定义好的可复用的部分(minxin)，注册到组件中
  mixins:[commonMinxin],
  methods:{
    ...
  },
  mounted(){
    console.log(this.$data);// 可以访问到 `commonMinxin` 预先定义的 `data`;
    this.changeFirst(); // 可以执行 `commonMinxin` 预先定义的methods
  },
}
```

- 如果 mixins 中定义的数据项和组件中定义的数据项重名了怎么办

  > 数据对象在内部会进行浅合并 (一层属性深度)，在和组件的数据发生冲突时以组件数据优先。

- 如果有重复的生命周期函数将怎么处理
  > 同名钩子函数将混合为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。

```js
const mixin = {
  created: function() {
    console.log("混入对象的钩子被调用");
  }
};

new Vue({
  mixins: [mixin],
  created: function() {
    console.log("组件钩子被调用");
  }
});
// => "混入对象的钩子被调用"
// => "组件钩子被调用"
```

- 全局混入
  > 一旦使用了全局混入，将会影响到所有 Vue 实例

```js
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created () {
    var myOption = this.$options.myOption
    if (myOption) {
      console.log(myOption)
    }
  }
})

new Vue({
  myOption: 'hello!'
  ...
})
// => "hello!"
```
