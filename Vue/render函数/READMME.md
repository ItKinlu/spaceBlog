# render 函数

## render 也是创建模板的一种方式

`render` 函数类似 `template` 标签的功能

```html
<body>
  <b-button>
    <h1>1</h1>
    <h1>2</h1>
  </b-button>
</body>
<script>
  export default {
    name: 'b-button',
    props: {
      color: {
        type: String,
        default: 'red'
      }
    },
    render(h){
      // 在这里定义模板，创建标签
      // 如何渲染一组元素
      const arry = this.$slots.default.map(VNode => {
        return createElement('p', {
          class: 'control'
        }, [VNode])
      });

      return h('button',{
        class:"custom-class-name",
        style:{},
        //正常的html特性(除了class和style)
        attrs:{},
        //用来写原生的DOM属性
        domProps:{
           innerHTML:"ff"
        },
        on:{
          click:()=>{}
        }
      },arry)

       return h('button',{
        class:"custom-class-name"
      },'按钮')

    },
    computed:{},
    mounted(){},
    mehtods:{}
    ...
  }
</script>
```
