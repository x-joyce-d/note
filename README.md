ECMAScript 3 语法
===

全局函数
---
* decodeURI()
* decodeURIComponent()
* encodeURI() - 可把字符串作为uri进行编码
* encodeURIComponent()
* escape() - 对字符串进行编码
* eval() - 计算某个字符串，并执行其中的JavaScript代码
* isFinite() -检查其参数是否是无穷大
* isNAN() - 用于检查其参数是否是非数字值
* Number() - 把对象的值转换为数字
* parseFloat() -解析一个字符串并返回一个浮点数
* parseInt() - 解析一个字符串并返回一个整数
* String() - 把对象的值转为字符串
* unescape() - 对字符串进行解码


原生类型
---
变量可存放两种类型的值，即`原始值`和`引用值`
### 原始数据类型（堆）
  原始值可以被替换，但不可以被改变，除了`Null`和`Undefined`之外，所有基本类型（在一定条件下可以）都有其对应的包装对象，`valueOf()`返回基本类型值
* [Null](./ECMAScript3/Null.md)
* [Undefined](./ECMAScript3/Undefined.md)
* `Boolean` - true/false
* `Number` - int/float
* `String` - "1ada"
* `Symbol` - 唯一且不可变
```
  数据类型转换：
    字符串转数字：parseInt() parseFloat()
```
```js
  // 使用字符串方法不会改变一个字符串
  var bar = "baz";
  bar.toUpperCase();
  console.log(bar);               // baz
  console.log(bar.toUpperCase());  // BAZ 是对原值的副本的操作
  bar = bar.toUpperCase();     // BAZ - 赋值行为可以给基本类型一个新值，而不是改变它
```

### 引用数据类型（栈）
引用值可以改变
* [Object](./ECMAScript3/Object.md)
```js
  var foo=[]
  foo.push('abc')
  console.log(foo)   // ['abc']
```

语言特性
---
* `弱/动态类型`
  -不需提前声明变量的类型，在程序运行过程中，类型会被自动确定，可使用一个变量来保存不同数据类型的值
```js
  var num = '123'
  var num = 0
  var num = true
  alert(typeof num)
```
* [闭包](./ECMAScript3/bibao.md)
* [原型、继承](./ECMAScript3/protoType.md)
  -
* [作用域](./ECMAScript3/scope.md)
* `单线程`
```js
function main(param){
  console.log("aaa",param);
  setTimeout((param)=>{
    console.log("bbb",param)
  },1000)  // 1s后不会立即输出；必须等待前一个任务执行完成才会执行它
  console.log("ccc",param)
}
main("123")
```
* [递归](./ECMAScript3/recursion.md)

[包装对象](./ECMAScript3/wrapperObject.md)
---
引用类型中包含了三种基本包装类型：String、Number、Boolean；它们是特殊的引用类型
```js
var str = 'hello'; //string 基本类型
var s2 = str.charAt(0); //here 后台会自动完成以下动作：
（
 var str = new String('hello'); // 1 找到对应的包装对象类型，然后通过包装对象创建出一个和基本类型值相同的对象
 var s2 = str.chaAt(0); // 2. then 该对象调用包装对象下的方法，并返回结果
 str = null;  //    3. 该临时创建的对象被销毁
 ）
alert(s2);//h
alert(str);//hello
```
全局对象
---
