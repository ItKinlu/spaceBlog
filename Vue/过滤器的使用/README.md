# Vue 过滤器传参以及接收

## 示例代码

Mustache `\{ \{ \} \}` 语法的过滤器

```html
<span>{{msg | filterMsg('one')}}</span>
<script>
  export default {
    filters: {
      filterMsg(val, msg) {
        // 参数 val 默认参数，为要过滤的值
        // msg 是我们自定义的参数
        return val + msg;
      }
    }
  };
</script>
```

### v-html 过滤器

有时候我们需要根据返回的值来显示不同的 html，所以可以使用`v-html`来绑定 html，但是`v-html`如何实现过滤呢

```html
<span v-html="filterHtml(参数1,参数2)"></span>
<span v-html="$options.filters.filtersMsg(参数1,参数2)"></span>
<script>
  export default {
    methods: {
      // 通过 methods 来做过滤
      filterHtml(val, val2) {
        return val1 + val2;
      }
    },
    filters: {
      filtersMsg(val, val2) {
        return val + val2;
      }
    }
  };
</script>
```
