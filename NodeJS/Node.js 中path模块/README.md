# path 模块

## 常用方法啊

```js
/**
 * PATH 模块
 *
 * 文件操作过程中必须物理路径（绝对路径，，以盘符开头）
 */
const path = require("path");

const basePath = path.join(__dirname, "../Node/fs.js");
// 基本名称，获取文件名(文件名,[是否删除扩展名.js])
path.basename("./fs.js");

// 获取不同操作系统中默认的路径分隔符
console.log(path.delimiter); // ; 或者 :

// node中获取环境变量
console.log(process.env.path.split(path.delimiter));

// 获取目录名称 (文件地址)
console.log(path.dirname(basePath)); // C:\Users\Administrator\Desktop\Node

// 获取扩展名(文件地址)
console.log(path.extname(basePath)); // .js 包含点.

// 将一个路径字符串转换为一个对象，包含文件目录，路径，扩展名
let obj = path.parse(basePath);
console.log(obj);

// 将对象路径转换为路径字符串(obj)
path.format(obj);

// 判断一个路径是不是一个绝对路径
console.log(path.isAbsolute(basePath)); //  true

// 拼合路径(n个参数);
path.join(__dirname, "");

// 常规化一个路径(针对于window设计)；根据操作系统
let a = path.normalize("c://dev");

// (from,to)获取从to相对于from的一个相对路径
console.log(path.relative(__dirname, "C:UsersAdministratorDesktopNodepath.js"));

// 于join不同
path.resolve(__dirname, "../", "/code");

// 路径里的分隔符，当前操作系统中的路径成员分隔符
console.log(path.sep); // / or \

// win 指的就是windows
// 允许在任意操作系统使用widow的方式操作路径
console.log(path.win32);
console.log(path === path.win32); // true
var a = {
  win32: p
};
a.win32 = a;
// 允许在任意操作系统使用linux的方式操作路径
console.log(path.posix);
```
