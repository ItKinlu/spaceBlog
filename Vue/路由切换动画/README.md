# 路由切换动画

几个 vue 路由切换动画，使用 `transition` 组件，配合 `css` 达到路由切切换动画，以及一些过渡动画

## 示例代码

```html
<transition name="fade-transverse">
  <router-view></router-view>
</transition>
<transition name="fade-scale">
  <router-view></router-view>
</transition>
<style>
  /* 过渡动画1 横向渐变*/
  .fade-transverse-leave-active,
  .fade-transverse-enter-active {
    transition: all 0.5s;
  }
  .fade-transverse-enter {
    opacity: 0;
    transform: translateX(-30px);
  }
  .fade-transverse-leave-to {
    opacity: 0;
    transform: translateX(30px);
  }

  /* 过渡动画2 缩放渐变*/
  .fade-scale-leave-active,
  .fade-scale-enter-active {
    transition: all 0.5s;
  }
  .fade-scale-enter {
    opacity: 0;
    transform: scale(1.2);
  }
  .fade-scale-leave-to {
    opacity: 0;
    transform: scale(0.8);
  }
</style>
```
