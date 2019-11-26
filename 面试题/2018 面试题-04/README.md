# JavaScript 面试题

- Q: null 和 undefined 的异同

  1. 相同点:
     在 if 判断语句中,值都默认为 false
     大体上两者都是代表无,具体看差异

  2. 差异:
     null 转为数字类型值为 0,而 undefined 转为数字类型为 NaN(Not a Number)
     undefined 是代表调用一个值而该值却没有赋值,这时候默认则为 undefined
     null 是一个很特殊的对象,最为常见的一个用法就是作为参数传入(说明该参数不是对象)
     设置为 null 的变量或者对象会被内存收集器回收

---

- Q: JS 有几种数据类型,其中哪些的基本数据类型有哪些!
  七种数据类型
  Boolean
  Null
  Undefined
  Number
  String
  Symbol (ECMAScript 6 新定义)
  Object
  其中 5 种为基本类型:string,number,boolean,null,undefined
  Object 为引用类型(范围挺大),也包括数组、函数,
  Symbol 是原始数据类型 ，表示独一无二的值

---

- Q: 跨域解决方案
  1. 服务器配置 cors
  2. 使用 jsonp
  3. webpack 中的 proxy 代理
  4. node 或者 nginx 代理，node 基于 express 的接口转发

---

- Q: new 操作符具体干了什么呢?

  ```js
  // 1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
  // 2、属性和方法被加入到 this 引用的对象中。
  // 3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。
  var obj = {};
  obj.__proto__ = Base.prototype;
  Base.call(obj);
  ```

---

- Q: documen.write 和 innerHTML 的区别

  1. document.write 可以重绘整个页面
  2. innerHTML 只能重绘页面的一部分

- Q: 预解析是什么

- Q: 下面代码将会输出什么结果：考察即时运行函数：

  ```js
  var result = (function() {
    return 1;
  },
  function() {
    return "2";
  })();
  console.log(typeof result); // 结果是2
  // 因为内部直接执行两个函数，后面的return的值会覆盖前面的return的值
  ```

---

- Q: 移动端和 PC 端有哪些异同
  PC 考虑的是浏览器兼容性，移动端开发考虑的更多的是手机兼容性，因为目前 ios 和 android 系统一般浏览器用的都是 webkit 内核，所以做移动端开发，更多考虑的应该是手机分辨率的适配，和不同操作系统的略微差异化。
  1. 移动端不需要 300ms 的单击确认，所以不要监听 click 事件
  2. 移动端网络一般较慢，如何减小页面体积及请求数，利用好缓存？
  3. 移动端需要点击的元素及其间隔不能太小，考虑手指的面积？
  4. 横屏和竖屏下的表现？
  5. 不同浏览器间的兼容性（太多了，如 position:fixed）？
  6. Retina 屏图片会不会模糊？
  7. 输入状态键盘会不会挡住输入内容？
  8. 在浏览器上点击后退的行为？
  9. 某些浏览器（如 Safari）的隐私模式下 cookie 和 localStorage 的替代方案？……7

---

- Q：什么是浏览器的重排重绘
  浏览器下载完页面中的所有组件——HTML 标记、JavaScript、CSS、图片之后会解析生成两个内部数据结构——DOM 树和渲染树。DOM 树表示页面结构，渲染树表示 DOM 节点如何显示（绘制）。重排是需要重新分析页面元素尺寸；重绘是元素样式的改变。

---

- Q：哪些操作会导致重拍重绘
  1. 添加或者删除可见的 DOM 元素
  2. 元素位置改变
  3. 元素尺寸改变
  4. 元素内容改变（例如：一个文本被另一个不同尺寸的图片替代）
  5. 页面渲染初始化（这个无法避免）
  6. 浏览器窗口尺寸改变

---

- Q：v-show 元素的显示和隐藏算是重排吗?
  添加或者删除可见的 dom 元素属于重排,v-show 是设置了 css 的 display 属性，是算重排的

---

- Q: setTimeout 的异步执行,下面代码的执行结果是什么

  ```js
  var a = 2;
  // 同步内容执行完毕再执行setTimeout中的，js中同步会阻塞异步内容
  setTimeout(function() {
    a--;
  });
  // 先执行a++，值不变还是2
  a++;
  console.log(a);

  // 程序是按照步骤来的，如果是a++的话，在那一行代码中，a的值是不变的，
  // 下一行才发生变化，++a则是在那一行已经发生了变化。
  ```

- Q: 有一个输入框，在用户停止输入后 1s 后搜索

  ```js
  var time = null;
  input.addEventListener("input", () => {
    cleartimeout(time);
    time = setTimeout(() => {
      seach();
    });
  });
  ```

- Q: Vue 和 jQuery 相比有哪些优势
  jQuery 是以操作 dom 为主，做了数据处理之后还需要对 dom 进行操作。vue.js 是以操作数据为主，不操作 dom，也就是传说中的双向数据绑定，你只需要操作数据就好，dom 自动更新。这只是对初学者来说最大的不同。jQuery 只是一个类库，只是提供了很多的方法，不能算框架，而 vue.js 是一个框架，有一套完整的体系。

- Vue 的 data 为什么是函数
  Object 是引用数据类型,如果不用 function 返回,每个组件的 data 都是内存的同一个地址,一个数据改变了其他也改变了;
  javascipt 只有函数构成作用域(注意理解作用域,只有函数的{}构成作用域,对象的{}以及 if(){}都不构成作用域)，data 是一个函数时，每个组件实例都有自己的作用域，每个实例相互独立,不会相互影响。

- 什么是 webWorker
  webWorker 是为了解决 js 单线程问题的，因为 js 的 ui 和计算是同一个进程，如果计算量比较大就会阻塞 ui 的渲染,所以会引入 webWorker 来解决这个问题。webWorker 会独立一个上下文运行一个文件。Web Worker 使用起来非常简单，在“主线程”中执行 new Worker 返回一个 webWorker 实例，通过监听 onmessage 事件获取消息，通过 postMessage 发送消息：“主线程”和 Worker 之间通过 postMessage 发送消息，通过监听 onmessage 事件来接收消息，从而实现二者的通信。

- 对象的深度克隆

  ```js
  function clone(Obj) {
    var buf;
    if (Obj instanceof Array) {
      buf = []; //创建一个空的数组
      var i = Obj.length;
      while (i--) {
        buf[i] = clone(Obj[i]);
      }
      return buf;
    } else if (Obj instanceof Object) {
      buf = {}; //创建一个空对象
      for (var k in Obj) {
        //为这个对象添加新的属性
        buf[k] = clone(Obj[k]);
      }
      return buf;
    } else {
      return Obj;
    }
  }
  ```

- 分析下面的代码判断输出

  ```js
  for (var i = 0; i < 5; i++) {
    console.log(1);
    setTimeout(function() {
      console.log(1, i);
    }, 1000);
  }
  // 先执行for循环，然后执行之后一行的console,最后执行setTimeout中的console
  console.log(1, i);
  ```

- 分析下面代码的输出

  ```js
  if (!("a" in window)) {
    var a = 10;
  }
  // undefined,变量提升
  // 声明变量 var a = undefined;
  console.log(a);
  ```

- 分析下面代码，并且判断输出

  ```js
  var count = 0;
  console.log(typeof count === "number"); // true , 这个不用解释了
  console.log(!!typeof count === "number"); // false
  // typeof count 就是字符串"number"
  // !!是转为布尔值(三目运算符的变种),非空字符串布尔值为 true
  // 最后才=== 比较 , true === "number" , return false
  ```

- 关于 IIFE 立即执行函数的面试题

  ```js
  // 立即执行函数，会立即执行函数内部的代码，并且生成一个函数作用域，所以使用var声明的a变量，在预解析时已经被赋值为undefined然后代码执行赋值为3，所以在函数外部访问当然是undefined，因为已经是内部的作用域，外部访问不到，而变量b未使用var声明，所以不存在变量提升，所以为全局变量直接赋值为3
  (function(){
    var a = b = 3;
  })()

  console.log(typeof a === "undefined"); // true
  console.log(typeof b === "undefined"); // false
  // 这里涉及的就是立即执行和闭包的问题,还有变量提升,运算符执行方向(=号自左向右)
  // 那个函数可以拆成这样：
  (function()
    var a; // 局部变量,外部没法访问
    b = 3; // 全局变量,所以 window.b === 3 , 外部可以访问到
    a = b;
  })()

  // 所以下面这样也是正确的
  console.log(typeof b === "number" && b ===3); // true
  ```

- 以下代码的输出是什么？并说明原因。

```js
var myObject = {
  foo: "bar",
  func: function() {
    var self = this;
    console.log("outer func:  this.foo = " + this.foo);
    console.log("outer func:  self.foo = " + self.foo);
    (function() {
      console.log("inner func:  this.foo = " + this.foo);
      console.log("inner func:  self.foo = " + self.foo);
    })();
  }
};
myObject.func();
/*
 * outer func: this.foo = bar
 * outer func: self.foo = bar
 * inner func: this.foo = undefined
 * inner func: self.foo = bar
 * 在 outer function 里，this 和 self 都指向 myObject, 因此都能访问到 foo
 * 在 inner function 里，this 不再指向 myObject,因此，this.foo 在 inner       function 里面是 undefined 或者是 window
 * 然而，self 依然指向 myObject，（在 ECMA5 之前，this 在内部 function 里将指    向 window，然而，在 ECMA5 之后，内部 function 的 this 将是 undefined).
 **/
```

- 函数提升和变量提升，它们的优先级

```js
// 变量提升
var a = funtion () {
  console.log(10)
}
var a;
console.log(a);    // f a() {console.log(10)}
console.log(a());  //  undefined

a = 3;
console.log(a)   //3
a = 6;
console.log(a());   //a() is not a function;
// 由此可见函数提升要比变量提升的优先级要高一些，且不会被变量声明覆盖，但是会被变量赋值之后覆盖。
```
