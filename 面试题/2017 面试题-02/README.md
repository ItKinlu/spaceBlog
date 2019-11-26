# 常见 JavaScript 面试题

- 用`typeof bar === "object"`判断`bar`是否是一个`object`的潜在缺陷是什么？怎样才能避免这种缺陷？
  答：尽管用`typeof bar === "object"`是一个判断 bar 是一个 object 的可靠方法，但是令人惊讶的是，在 JavaScript 中 null 也是一个 object!

  ```js
  var bar = null;
  console.log(typeof bar === "object"); // true,js中null也是object
  console.log(bar !== null && typeof bar === "object"); // false,判断是要过滤掉null
  // 如果bar是一个function，也会返回false,通常情况下，这是我们期望的，但是在某些情况下，我们希望当bar是function时，也返回true,你就需要修改上面的解决方案如下：
  console.log(
    bar !== null && (typeof bar === "object" || typeof bar === "function")
  );
  // 但是数组也是object的一种，所以也要忽略掉
  console.log(
    bar !== null &&
      typeof bar === "object" &&
      toString.call(bar) !== "[object Array]"
  );
  ```

- 下面的代码将输出什么？并说明原因

  ```js
  (function() {
    var a = (b = 3);
  })();
  console.log(a); // 访问不到a
  console.log("b is" + b);
  // 上面函数内运行的实际上是：
  b = 3;
  var a = b;
  // a是使用var声明的，在外部访问a是访问不到的，b是3
  // b 未使用关键字声明，所以会属于 window.b
  ```

- 以下代码的输出是什么？并说明原因。

  ```js
  var myObject = {
    foo: "bar",
    func: function() {
      // 另存this this指的是当前对象 myObject
      var self = this;
      console.log("outer func:  this.foo = " + this.foo); // outer func:  this.foo = bar
      console.log("outer func:  self.foo = " + self.foo); // outer func:  self.foo = bar
      (function() {
        console.log("inner func:  this.foo = " + this.foo); // inner func:  this.foo = undefined
        console.log("inner func:  self.foo = " + self.foo); // inner func:  self.foo = bar
      })();
    }
  };
  myObject.func();
  // 在inner function里，this不再指向myObject,因此，this.foo在inner function里面是undefined,然而，self依然指向myObject，（在ECMA5之前，this在内部function里将指向window，然而，在ECMA5之后，内部function的this将是undefined)
  ```

- 将一个 JavaScript 文件封装在一个 function 块里的意义，原因是什么？
  答：比如`jQuery`将源码文件封装在一个函数中越来越普遍。这种技术会为这个源码文件创建一个封闭的环境，可能最重要的是创建了一个私有的命名空间，因此避免了在不同的 JavaScript modules 和库中出现潜在的命名冲突。这种技术的另一个特点是允许通过别名的方式很容易的引用全局变量。

- 在 JavaScript 源码文件中以"use strict"开始的意义和好处是什么？
  答：采用 strict 模式的主要好处如下：
  a. 使得 debugging 更容易：在一些被忽略或者潜在的错误会产生 error 或者 exceptions，会很快的在你的代码中显示警告，引导你很快的找到对应的源码。
  b. 阻止出现意外的全局变量：如果不是在 strict 模式里，那么赋值给一个没有声明的变量时，会自动的创建一个同名的全局变量，这是 JavaScript 中最常见的错误之一。在 strict 模式里，会尝试抛出一个 error.
  c. 强制排除 this 错误：在非 strict 模式里，this 引用为 null 或者 undefined 时，会自动强制指向全局，这会导致各种错误的引用。在 strict 模式里，this 值为 null 或者 undefined 将会抛出 error.
  d. 不允许重名的属性名或者参数名.在 strict 模式里，如果定义了如：var object={foo:’bar’,foo:’baz’};或者定义一个重名参数的函数，如:function foo(val1,val2,val1){}.会产生一个 error,而这个 bug 几乎一定会产生，但你可能浪费大量的时间才能找到。
  e. 使 eval()更加安全。在 strict 模式和非 strict 模式里，eval()存在很多不同。在 strict 模式里，变量和函数在 eval()中声明，但语句不在内部块创建，但是在非 strict 模式里，语句也会在内部块里创建，这也是常见的源码问题。
  f. 不正确使用 delete 会抛出 error:delete 操作（用于从 object 中删除一个属性）不能用于没有配置的属性，在非 strict 模式的代码里删除一个没有配置的属性会失败，但不会有提示，在 strict 模式里，则会抛出 error。
