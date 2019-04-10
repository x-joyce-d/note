ECMAScript 3 语法
===

全局函数
---
### 编码函数

| \  | escape() | encodeURI() | encodeURIComponent() |
|-------|:---:|-----------|---------------------------------|
| 是什么  | 编码字符串（不提倡） | 编码整个URI | 编码整个URI中的参数 |
| 可转义字符  | 多为汉字 | 除却ASCII，数字，保留字符之外的所有字符 |保留字符（; / ? : @ & = + $ , #）|
| 不同点  | 与URI无关 | 编码范围小 | 编码范围更大（可编码特殊字符） |

* escape(str) - 对字符串进行编码
* encodeURI() - 可把字符串作为URI进行编码
* encodeURIComponent() - 把字符串编码为URI组件

1. encodeURI()与decodeURI()，假定URI中的任何保留字符都有特殊意义，所以不会进行编码
1. encodeURIComponent()decodeURIComponent()，假定URI中的任何保留字符都看作是普通文本，所以必须进行编码

### 解码函数（与编码函数相对）
* unescape() - 对字符串进行解码
* decodeURI() - 解码某个编码的URI
* decodeURIComponent() - 解码一个编码的URI组件
```js
  // javascript 的输入和输出默认都为`Unicode`字符
  javascript:escape("春节");
  //输出 "%u6625%u8282"
  javascript:escape("hello world");
  //输出 "hello%20word"
  javascript:escape("\u6625\u8282");
  //输出 "%u6625%u8282"

  javascript:unescape("%u6625%u8282");
  //输出 "春节"
  javascript:unescape("hello%20word");
  //输出 "hello world"
```
```js
  // 输出符号并在每个字节前加上`%`
  var test1="http://www.haorooms.com/My first/";
  var nn=encodeURI(test1);
  var now=decodeURI(test1);
  javascript:encodeURI("春节")
  // 输出http://www.haorooms.com/My%20first/
  // 输出http://www.haorooms.com/My first/
  //输出 %E6%98%A5%E8%8A%82
  var test1="http://www.haorooms.com/My first/";
  var bb=encodeURIComponent(test1);
  var nnow=decodeURIComponent(bb);
  //输出 http%3A%2F%2Fwww.haorooms.com%2FMy%20first%2F
  //输出 http://www.haorooms.com/My first/
```

### 转换为数值
1.
| \  | Number() | parseInt() | parseFloat() |
|-------|:---:|-----------|---------------------------------|
| 相同点  | 都返回一个数值 | |
| 不同点  | 转换任意数据类型（转换的是整个值） | 解析字符串（转换第一个无效字符之前的字符串） | 解析字符串 |

2.
| \  | parseInt(string,type) | parseFloat(string) |
|-------|:---:|-----------|
| 相同点  | 都解析字符串 | |
| 不同点  | 1.返回一个整数；2. 可传第二个参数（进制类型）| 1.返回一个浮点数；2.无第二个参数，只解析十进制 |

* Number() - 把对象的值转换为数字
  * Boolean=>0/1;null=>0;undefined=>NAN;
  * 空字符串=>0   
* parseInt(string,type)
  * 参数
    * 若无第二个参数，默认为十进制
    * 若第一个参数不是字符串或空串，则返回NAN
    * 若字符串以"0x/0X"开头，parseInt会将其按照十六进制解析
* parseFloat(string)
  * 若字符串包含的是一个没有小数点，或者小数点后面都为0的数，则返回整数

### 检查数值
* isFinite() - 检查其参数是否是无穷大（确定数值是否介于最小值与最大值之间）
  * 是true,否false（正无穷，负无穷，NAN，非数值）
* isNAN() - 用于检查其参数是否是非数字值
  * 应用
    * 检查算数错误（eg: 0 做除数）
    * 检测parseFloat()与parseInt()的结果，以判断是否是合法的数字

  ```js
    'abc' - 3   // NaN
    parseInt('abc')  // NaN
    parseFloat('abc') // NaN
    Number('abc') //NAN
  ```

### 转换为字符串
* String() - 把对象的值转为字符串（）
```js
  //与toString()方法不同，对null 和 undefined 强制类型转换不会报错
  var a = String(null)  // 输出 "null"
  var b = null.toString() // causes an error
```

### 解析函数
* eval("()") - 常用于将服务器端返回的json字符串解析为json对象
  * 参数
    * 只接受原始字符串作为参数，且只接受一个参数；
    * 若字符串表示为表达式，则进行求值；
    * 若定义了一个或多个值，则返回最后一个值；
  * 注意
    * 在JavaScript中json对象会被当成语句块执行，须用（）括起来；
    * 总是在调用它的上下文作用域内执行。

```js
  //1
  var jsonStr = "{'name':'JOYCE','age':3}";
  alert(jsonStr.name);　　//undefined
  var jsonObject = eval("("+jsonStr+")");
  alert(jsonObject.name);　//JOYCE
  //2
  var geval=eval;                //使用别名调用eval，将是全局eval
  var x="global",y="global";    //两个全局变量
  function f(){                //函数内执行的是局部eval
      var x="local";            //定义局部变量
      eval("x += ' chenged';");//直接使用eval改变的局部变量的值
      return x;                //返回更改后的局部变量
  }
  Function g(){                //这个函数内执行了全局eval
      var y="local";
      geval("y += ' changed';"); //等价于在全局作用域内调用
      return y;
  }
  console.log(f(),x);            //输出 “local changed global”
  console.log(g(),y);            //改变了全局变量，输出“local global changed”
```
### 扩展
* [编码](https://blog.csdn.net/lvxiangan/article/details/8151670)
<!-- 详见[此](https://blog.csdn.net/iefreer/article/details/4836844) -->

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
  <!-- 数据类型转换： -->
    <!-- 字符串转数字：parseInt() parseFloat() -->
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
浏览器对象
---
