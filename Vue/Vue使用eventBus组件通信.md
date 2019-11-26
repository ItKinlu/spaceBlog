---
title: Vue使用eventBus组件通信
tags:
  - Vue
abbrlink: 201805022113
date: 2018-06-02 21:13:45
---

`Vue` 中组件的通信方式可以通过使用第三组件来传值或者使用 `vuex` 来传值，也可以通过新建一个 `Vue` 实例来传值

但是并不是所有的项目中都必须用到 `vuex` ，在一些小的项目中，使用 `eventBus` 是一个很好的选择，比如有两个组件以及一个 `eventBus.js`

eventBus.js

```js
import Vue from 'vue'
export default new Vue()
```

组件 1

```html
<template>
  <div @click="sendSomeThing($evnent)">点击</div>
</template>
<script>
  import eventBus from 'eventBus.js'
  export default {
    methods: {
      sendSomeThing(event) {
        // add 传递的事件名称，event 是传递的值，广播事件
        eventBus.$emit('add', event)
      }
    }
  }
</script>
```

组件 2

```html
<script>
  import eventBus from 'eventBus.js'
  export default {
    created() {
      // 添加事件监听
      eventBus.$on('add', target => {
        console.log(target)
      })
    }
  }
</script>
```

这样我们在组件 1 中每次点击 div，在组件 2 中就会监听到`add`事件被触发，就会打印出参数。
