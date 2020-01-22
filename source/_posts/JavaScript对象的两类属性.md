---
title: JavaScript对象的两类属性
date: 2020-01-21 10:33:07
tags: js
---
为了提高抽象能力,JavaScript的属性被设计成比别的语言更加复杂的形式,它提供了数据属性和访问器属性两类
## 数据属性
- value: 属性的值
- writable: 决定属性能否被赋值
- enumerable: 决定for in能否枚举该属性
- configurable: 决定属性能否被删除或者改变特征值
我们定义属性,writable、enumerable、configurable都默认为true.可以使用内置函数Object.getOwnPropertyDescripter来查看.
```js
let o = { a: 1 };
o.b = 2;
// a 和 b 皆为数据属性
Object.getOwnPropertyDescriptor(o, 'a'); // {value: 1, writable: true, enumerable: true, configurable: true};
Object.getOwnPropertyDescriptor(o, 'b'); // {value: 2, writable: true, enumerable: true, configurable: true};
```
如果想改变属性的特征或者定义访问器属性,我们可以使用Object.definedProperty
```js
let o = { a: 1 };
Object.defineProperty(o, 'b', {
    value: 2,
    writable: false,
    enumerable: true,
    configurable: true
});
o.b = 3;
console.log(o.b); // 2
```

## 访问器属性
- getter: 函数或undefined,在取属性值时被调用
- setter: 函数或undefined,在设置属性值时被调用
- enumerable: 决定for in 能否枚举该属性
- configurable: 决定该属性能否被删除或者改变特征值
```js
// setter经常和getter连用以创造一个伪属性值,不可能在具有真实值的属性上同时拥有setter
// 可以在对象声明时设置getter和setter
let o = { 
    get a() {return '$' + this.b}, 
    set a(value) {this.b = value * 2}
};
o.a = 10;
console.log(o); // { b: 20}
console.log(o.a) // '$20'
```
