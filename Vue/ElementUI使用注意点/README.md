# ElementUI 使用技巧以及注意点

## ElementUI 切换窗口 tabs 出现蓝色边框的问题

使用 `ElementUI` 的 `tabs` 组件有时候会遇到莫名出现蓝色边框的问题

> 需要注意：在项目的公共 `css` 文件中添加上面代码，这里的一定要加上 `!important`,因为 `npm run build` 打包代码的时候的,这段代码会被的 `element ui` 框架代码覆盖掉

```html
<style>
  /* elementui 的tabs组件出现蓝色边框问题 */
  .el-tabs__item:focus.is-active.is-focus:not(:active) {
    -webkit-box-shadow: none !important;
    box-shadow: none !important;
  }
</style>
```

ElementUI 官方文档中使用`picker-options`属性来限制可选择的日期，但是详细语法并未多加赘述，这里举例子稍做补充。

## 单个时间选择器

组件代码:

```html
<el-date-picker
  v-model="value1"
  type="date"
  placeholder="选择日期"
  :picker-options="pickerOptions0"
>
</el-date-picker>
```

- 需求 1：设置选择今天以及今天之后的日期

```js
data (){
  return {
    pickerOptions0: {
      isabledDate(time) {
        return time.getTime() < Date.now() - 8.64e7;
      },
    }
  }
}
```

- 需求 2：设置选择今天以及今天以前的日期

```js
data (){
  return {
    pickerOptions0: {
      disabledDate(time) {
        return time.getTime() > Date.now() - 8.64e6
      }
    },
   }
}
```

- 需求 3：设置选择今天以后的日期（不能选择当天时间）

```js
data(){
  return {
    pickerOptions0:{
      disabledDate(time){
        return time.getTime() < Date.now();
      }
    }
  }
}
```

- 需求 4：设置选择今天之前的日期（不能选择当天时间）

```js
data(){
  return {
    pickerOptions0:{
      disabledDate(time){
        return time.getTime() > Date.now();
      }
    }
  }
}
```

- 需求 5：设置选择三个月之前到家今天的日期

```js
data(){
  return {
    disabledDate(time){
      let curData = (new Date()).getTime();
      let three = 90 * 24 * 3600 * 1000;
      let threeMonths = curData - three;
      return time.getTime() > Date.now() || time.getTime() < threeMonths;
    }
  }
}
```

## 两个时间选择器

组件代码

```html
<el-date-picker
  v-model="value1"
  type="date"
  placeholder="开始日期"
  :picker-options="pickerOptions0"
>
</el-date-picker>
<el-date-picker
  v-model="value2"
  type="date"
  placeholder="结束日期"
  :picker-options="pickerOptions1"
>
</el-date-picker>
```

- 需求 1：限制结束日期不能大于开始日期

```js
```

[参考链接](https://www.cnblogs.com/martinl/p/6696273.html)
