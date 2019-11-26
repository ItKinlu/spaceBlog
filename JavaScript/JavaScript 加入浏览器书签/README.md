# 通过 JavaScript 加入浏览器书签

## 如何使用 JavaScript 将页面加入书签

- ie 浏览器下实现的方法

```js
window.external.addFavorite(
  "添加到页面收藏夹的完整页面地址",
  "当前页面的标题名称"
);
<a
  herf="#"
  onClick="javascript:window.external.addFavorite('www.baidu.com'，'百度')"
>
  添加到收藏夹
</a>;
```

- firefox 下实现的方法

通过 window.sidebar.addPanel()

```html
<a
  href="#"
  onClick="javascript:window.sidebar.addPanel('西部e网-软件教程','http://weste.net','');"
  >收藏本站</a
>
```

在链接上添加 rel="sidebar"属性

```html
<a href="http://weste.net" title="西部e网-软件教程" rel="sidebar">收藏本站</a>
```
