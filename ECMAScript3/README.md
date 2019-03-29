ECMAScript 3 语法
===

全局函数
---

原生类型
---
变量可存放两种类型的值，即`原始值`和`引用值`
### 原始数据类型（堆）
  原始值可以被替换，但不可以被改变，除了`Null`和`Undefined`之外，遨游基本类型都有其对应的包装对象，valueOf()返回基本类型值
* [Null](./null.md)
* [Undefined](./Undefined.md)
* [Boolean](./Boolean.md)
* [Number](./Number.md)
* [String](./String.md)
* [Symbol](./Symbol.md)

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
* [Object](./Object.md)

```js
  var foo=[]
  foo.push('abc')
  console.log(foo)   // ['abc']
```

语言特性
---
* 弱类型
