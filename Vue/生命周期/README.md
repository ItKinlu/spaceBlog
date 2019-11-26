# Vue 生命周期

## 生命周期

beforecreate : 可以在这加个 loading 事件
created ：在这结束 loading，还做一些初始化，实现函数自执行
mounted ： 在这发起 axios 请求，拿回数据，配合路由钩子做一些事情
beforeDestory： destoryed ：当前组件已被删除，清空相关内容
