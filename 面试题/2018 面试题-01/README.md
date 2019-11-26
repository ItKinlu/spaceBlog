# 面试题

## JavaScript 相关

JavaScript 中如何检测一个变量是一个 String 类型？请写出函数实现

```js
typeof obj === "string";
typeof obj === "string";
obj.constructor === String;
```

使用 JavaScript 清除字符串中的空格

- 使用正则匹配

```js
// 去除所有的空格
str = str.replace(/\s*/g, "");
// 取出两头空格
str = str.replace(/^\s*|\s*$/g, "");
// 去除左边的空格
str = str.replace(/^\s*/, "");
// 去除右边的空格
str = str.replace(/(\s*$)/g, "");
```

- 使用 str.trim()方法

```js
// 局限是无法去除中间的空格
var str = "   xiao  ming   ";
var str2 = str.trim();
console.log(str2); //xiao  ming
```

- 使用 jquery,\$.trim(str)方法

```js
$.trim(str);
// 局限性是无法去除中间的空格
```

- 如何获取 URL 中的字符串

```js
function getParams() {
  var sHref = window.location.href;
  // 通过?拆分
  var args = sHref.split("?");
  // 如果没参数，返回空值
  if (args[0] == sHref) {
    return "";
  }
  // 如果参数，参数之间通过 & 分割
  var arr = args[1].split("&");
  // 新建一个空对象
  var obj = {};
  // 遍历我们通过 & 分割出来的数组
  for (var i = 0; i < arr.length; i++) {
    // 数组的每一个元素通过 = 分割
    var arg = arr[i].split("=");
    obj[arg[0]] = arg[1];
  }
  return obj;
}
```

- js 字符串操作函数

```js
concat(); // 将两个或多个字符的文本组合起来，返回一个新的字符串。
indexOf(); // 返回字符串中一个子串第一处出现的索引。如果没有匹配项，返回 -1 。
charAt(); // 返回指定位置的字符。
lastIndexOf(); // 返回字符串中一个子串最后一处出现的索引，如果没有匹配项，返回 -1 。
match(); // 检查一个字符串是否匹配一个正则表达式。
substr(); // 函数  返回从string的startPos位置，长度为length的字符串
substring(); // 返回字符串的一个子串。传入参数是起始位置和结束位置。
slice(); // 提取字符串的一部分，并返回一个新字符串。
replace(); // 用来查找匹配一个正则表达式的字符串，然后使用新字符串代替匹配的字符串。
search(); // 执行一个正则表达式匹配查找。如果查找成功，返回字符串中匹配的索引值。否则返回 -1 。
split(); // 通过将字符串划分成子串，将一个字符串做成一个字符串数组。
length; //属性， 返回字符串的长度，所谓字符串的长度是指其包含的字符的个数。
toLowerCase(); // 将整个字符串转成小写字母。
toUpperCase(); // 将整个字符串转成大写字母。
```

- 怎样添加、移除、移动、复制、创建和查找节点

  1）创建新节点

  createDocumentFragment() //创建一个 DOM 片段
  　　 createElement() //创建一个具体的元素
  　　 createTextNode() //创建一个文本节点

  2）添加、移除、替换、插入
  　　 appendChild() //添加
  　　 removeChild() //移除
  　　 replaceChild() //替换
  　　 insertBefore() //插入

  3）查找
  　　 getElementsByTagName() //通过标签名称
  　　 getElementsByName() //通过元素的 Name 属性的值
  　　 getElementById() //通过元素 Id，唯一性

- 比较 typeof 与 instanceof

相同点：JavaScript 中 typeof 和 instanceof 常用来判断一个变量是否为空，或者是什么类型的。
typeof 的定义和用法：返回值是一个字符串，用来说明变量的数据类型。

细节：

(1)、typeof 一般只能返回如下几个结果：number,boolean,string,function,object,undefined。

(2)、typeof 来获取一个变量是否存在，如 if(typeof a!="undefined"){alert("ok")}，而不要去使用 if(a) 因为如果 a 不存在（未声明）则会出错。

(3)、对于 Array,Null 等特殊对象使用 typeof 一律返回 object，这正是 typeof 的局限性。

Instanceof 定义和用法：instanceof 用于判断一个变量是否属于某个对象的实例。

实例演示：

a instanceof b?alert("true"):alert("false"); //a 是 b 的实例？真:假

var a = new Array();
alert(a instanceof Array); // true
alert(a instanceof Object) // true
如上，会返回 true，同时 alert(a instanceof Object) 也会返回 true;这是因为 Array 是 object 的子类。

function test(){};
var a = new test();
alert(a instanceof test) // true
细节：

(1)、如下，得到的结果为‘N’,这里的 instanceof 测试的 object 是指 js 语法中的 object，不是指 dom 模型对象。

if (window instanceof Object){ alert('Y')} else { alert('N');} // 'N'
