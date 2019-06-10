原型与继承
===

原型
---
* javascript对每个创建的对象都会设置一个原型，指向它的原型对象
* 函数与对象
  对象都是通过函数创建的，每个函数都有个prototype属性(原型)，属性值是个对象，默认只有一个叫做constructor的属性，指向这个函数本身
  ```js
  var obj = new Object()
  obj.xxx  // 访问对象属性时，javascript会优先在当前对象身上查找该属性，
  //如果未找到，就到其原型对象上找，直到Object.prototype对象，
  // 如还未找到，返回undefined
  typeof Object //function
  ```
* 属性包括
  - `constructor`
  - `hasOwnProperty`
  - `isPrototypeOf`
  - `toString`
  - `valueOf`
  - `toLocalString`
  - `propertyIsEnumerable`
* “隐式原型” __proto__
  - 每个函数都有一个proto属性，指向创建该对象的函数的prototype

原型链
---
```js
  var arr =[1,2,3] //
  //其原型链为：arr=>Array.prototype=>Object.prototype=>null
```
* 是...
  实现继承的主要方法
  是利用原型让引用类型继承另一个引用类型的属性和方法
* instanceof运算符
  用来检测 constructor.prototype 是否存在于参数 object 的原型链

继承
---
* class继承
定义了构造函数和定义在原型对象上的函数
* 原型继承

创建对象
---
* 构造器
  -  使用`new操作符`来作用一个函数时，该函数就称为构造函数
* class关键字
* Object.create()
* 语法结构

默认顶端原型
---
* Object (protoType的`__proto__`指向的是null)

总结
---
* 对象.__proto__ = 构造函数.prototype
* 对象.constructor 返回值是 对象.构造函数
