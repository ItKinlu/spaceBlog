# 面试题

## JavaScript 常见面试题

### new 之后发生了什么

```js
/**
 * 创建一个空对象，构造函数中的this指向这个空对象
 * 这个新对象被执行 [[原型]] 连接
 * 执行构造函数方法，属性和方法被添加到this引用的对象中
 * 如果构造函数中没有返回其它对象，那么返回this，即创建的这个的新对象，否则，返回构造函数中返回的对象。
 * **/
/**
 * 1.创建一个新对象
 * 2.this 指向这个新对象
 * 3.执行代码，即对 this 赋值
 * 4.返回 this
 */
function _new() {
  let target = {}; // 创建新对象
  let [coustructor, ...args] = [...arguments];
  target.__proto__ = coustructor.prototype;
}
```

### 如何准确判断变量是数组类型

```js
var arr = []
arr instanseof Array // true
typeof arr // "object" typeof 只能判断简单数据类型
Object.prototype.toString.call(arr)// "[object Array]"
```

## Object 和 Function

> 在 JavaScript 语言中，整个核心的体系结构都围绕着两个构造函数 `Object` 和 `Function` 来构建的

```js
var arr = [];
arr instanceof Object; // true
Array instanceof Object; // true
String instanceof Object; // true
String instanceof Function; // true
Function instanceof Object; // true
Object instanceof Function; // true
```

### 原型链 ( prototype chain )

- 每个函数默认都会有一个属性叫 `prototype`
- 每一个通过函数和 `new` 操作符生成的对象都具有一个属性 `__proto__`, 这个属性保存了创建它的构造函数的`prototype` 属性的引用

```js
var arr = []; // 等同于 new Array()
arr.prototype; // undefined
arr.__proto__; // [constructor:f()....]
Array.prototype; // [constructor:f()....]
Array.prototype === arr.__proto__; // true
```

- 自己创建构造函数，原型链 demo

```js
function Car() {} // 构造函数: 拥有 prototype 属性
Car.prototype; // {constructor: ƒ}
var a = new Car(); // 通过new 创建实例
a.__proto__; // {constructor: ƒ}
a.__proto__ === Car.prototype; // true
a instanceof Car; // true
a instanceof Object; // true 实例继承自 Object
a instanceof Function; // false
Car instanceof Function; // true 构造函数继承自 Function
```

- 构造器 `Function` 的构造器是它自身
- 构造器 `Object` 的构造器是 Function

```js
Function.constructor === Function; // true
Object.constructor === Function; // true
Function.prototype.constructor === Function.constructor; // js 构造器是放在原型链上的 属性获取会搜索自身再搜索原型链
Object.__proto__.constructor === Function.constructor;
```

- 所有的引用类型（数组、对象、函数）都有一个 `_proto_` 属性(隐式原型属性），属性值是一个普通的对象
- 所有的函数，都有一个 `prototype(显式原型）` 属性，属性值也是一个普通的对象
- 所有的引用类型（数组、对象、函数），`__proto__` 属性值(隐式原型属性）指向它的构造函数的 `prototype` 属性值

### DOM 查询封装

```js
function $(selector) {
  // 实例属性
  this.element = document.querySelector(selector);
}
// 实例方法
// 属性操作
$.prototype.html = function(value) {
  var element = this.element;
  if (value) {
    element.innerHTML = value;
    return this; // 链式操作
  } else {
    return element.innerHTML;
  }
};
// 实例方法
// 事件绑定
$.prototype.on = function(type, fn) {
  var element = this.element;
  element.addEventListener(type, fn);
};
```

## 事件传播的三个阶段是什么

- 捕获 > 目标 > 冒泡

## 写一个闭包，每次调用的时候自加 1

```js
function b() {
  var i = 0;
  return function() {
    return i++;
  };
}
bid = b();
bid(); // 0
bid(); // 1
```

## 写一个函数，重复执行传入的函数指定次数，并且可以定义重复时间

```js
function doRepeat(func, times, waits) {
  let i = 0;
  return function() {
    const args = arguments;
    const timer = setInterval(function() {
      if (times === i) {
        clearInterval(timer);
        return;
      }
      i++;
      func(args[0]);
    }, waits);
  };
}
// 每间隔1s执行 console.log ，执行10次
var b = doRepeat(console.log, 10, 1000);
b("ff");
```

## 如何让 `a==1 && b ==2 && c==1` 的值为 true

- 如果 a 是一个 Object

```js
/**
 * 如果 a 是一个对象 Object ，那在执行 a== 的时候首先会去先执行 `valueOf` 方法，如果没有 `valueOf` 方法，就会去执行 `toString` 方法。（ toString 方法与 valueOf 类似，这里不再重复）
 * **/
const a = { value: 0 };
a.valueOf = function() {
  return (this.value += 1);
};
console.log(a == 1 && a == 2 && a == 3); // true
```

- 如果 a 是一个 Array

```js
/**
 * 如果a是一个数组Array，在数组转换成字符串的时候，数组toString会隐含调用join()方法
 */
const a = [1, 2, 3];
a.join = a.shift;
console.log(a == 1 && a == 2 && a == 3);
```

## 异步加载 JavaScript 脚本的方式

```html
<!-- html4 中使用 defer 属性 -->
<script defer src="./index.js"></script>

<!-- html5 中使用 async 属性 -->
<script async src="./index.js"></script>

<!-- 两者区别：
defer 要等到整个页面在内存中正常渲染结束（DOM 结构完全生成，以及其他脚本执行完成），在window.onload 之前执行；
async 一旦下载完，渲染引擎就会中断渲染，执行这个脚本以后，再继续渲染。
如果有多个 defer 脚本，会按照它们在页面出现的顺序加载
多个 async 脚本不能保证加载顺序 -->
```
