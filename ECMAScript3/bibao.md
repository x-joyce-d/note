闭包
===
允许将数据与一个或多个方法关联起来（eg:点击事件）

是什么
---
* 函数对象
* 与词法作用域，作用域链有关
* 函数是在其定义的作用域外被访问时，
* 是由该函数和其上层执行上下文共同构成

产生
---
* 函数作为返回值
* 函数作为参数传递

影响
---
* 内存泄漏 -- 阻止了垃圾回收机制对变量进行回收（影响性能）

应用
---
* 模块
可以将模块的公有属性，方法暴露出来
```js
  var myModule = (function (window, undefined) {
  	let name = "echo";
  	function getName() {
  		return name;
  	}
  	return {
  		name,
  		getName
  	}
  })(window);

  console.log( myModule.name ); // echo
  console.log( myModule.getName() ); // echo
```
* 延时器
* 监听器
