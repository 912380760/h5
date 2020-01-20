---
title: JavaScript类型：关于类型，有哪些你不知道的细节？
date: 2020-01-15 18:30:22
tags: js
---

## 类型
- Undefined
- Null
- Boolean
- String
- Number
- Symbol
- Object

## Undefined、Null
Undefined类型只有一个值undefined,表示未定义.任何变量在赋值前值为undefined.
Null类型只有一个值null,表示值定义了但为空.

## Boolean
Boolean类型只有两个值,true和false,表示逻辑意义上的真和假.

## String
String的意义并非"字符串",而是字符串的UTF16编码

## Number
Number类型为双精度浮点数规则,但是为了表达几个额外语言场景,规定了几个例外情况:
- NaN 错误数值
- Infinity 无穷大
- -Infinity, 负无穷大
根据浮点数的定义,非整数的Number类型无法用==和===来比较,正确的方法是使用JavaScript提供的最小精度值:
```js
Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON;
```

## Symbol
 Symbol是ES6中引入的新类型,它是一切非字符串的对象key的集合,在ES6规范中,整个对象系统被Symbol重塑,可以重新定义对象的一些行为.
 ```js
// 创建Symbol的方式
const mySymbol = Symbol("my symbol");

// 即使Symbol描述相同,不同Symbol也不相等
const mySymbol2 = Symbol("my symbol2");
console.log(mySymbol === mySymbol2); // false

// 使用Symbo.iterator自定义for...of行为
const o = {};
o[Symbol.iterator] = function() {
    let v = 0;
    return {
        next: function() {
            return {value: v++, done: v > 10}
        }
    }   
};
for(let v of o) {
    console.log(v); // 0 1 2 3 ...9
}
```

## Object
对象的定义是"属性的集合",一个key-value结构,属性分为数据属性和访问属性.
JavaScript中的基本类型都在对象类型中有构造器:
- Number
- String
- Boolean
- Symbol

我们必须意识到true与new Boolean(true)是完全不同的值,一个是布尔类型,一个是对象类型.
Number、String和Boolean,三个构造器是两用的,当跟new搭配时产生对象,当直接调用是表示类型转换.
Symbol类型比较特殊,直接用new调用会抛错.
JavaScript语言设计上试图模糊基本类型和对象之间的关系,通过 **.** 运算符提供装箱操作,它会根据基础类型构造一个临时对象,使得能在基础类型上调用对应对象的方法.
```js
// 在原型上添加方法都可以应用于基本类型
String.prototype.hello = () => console.log('hello');
'test'.hello(); // 'hello'
```

## 类型转换

### StringToNumber
字符串到数字的转换支持十进制、二进制、八进制和十六进制.
```js
'30' == 30; // true
'0b11' == 3; // true
'0o13' == 11; // true
'oxf' == 15; // true
```
此外，JavaScript 支持的字符串语法还包括正负号科学计数法，可以使用大写或者小写的 e.
```js
'1e4' == 10000; // true
'-1e4' == -0.0001; // true
```
### 装箱转换
每一种基本类型Number、String、Boolean、Symbol在对象中都有对应的类.所谓装箱转换,正是把基本类型转换为对应的对象.
每个装箱对象皆有私有的Class属性,这些属性可以用**Object.prototype.toString**获取:
```js
console.log(Object.prototype.toString.call('')); // "[object String]"
console.log(Object.prototype.toString.call(123)); // "[object Number]"
console.log(Object.prototype.toString.call(true)); // "[object Boolean]"
console.log(Object.prototype.toString.call(Symbol('a'))); // "[object Symbol]"
```
在JS中没有任何方法可以更改私有的Class属性,因此**Object.prototype.toString**是可以准确识别对象对应的基本类型的方法,它比instanceof更加准确.

### 拆箱转换
在JS标准中,规定了ToPrimitive函数,它是对象类型到基本类型的转换.
对象到String和Nmber的转换都遵循"先拆箱再转换"的规则.通过拆箱转换,把对象变成基本类型,再从基本类型转换为对应的String或者Number.
拆箱转换会尝试调用valueOf和toString来获得拆箱后的基本类型.如果valueOf和toString都不存在或者没有返回基本类型,则会产生类型错误TypeError.
```js
// 到Number转换会优先调用valueOf
let o = { 
    valueOf: () => {console.log('valueOf'); return {}}, 
    toString: () => {console.log('toString'); return {}}
};
o * 2;
// valueOf
// toString
// TypeError

// 到String的转换会优先toString
String(o);
// toString
// valueOf
// TypeError

// 在ES6中,还允许通过显示指定@@toPrimitive Symbol来覆盖原有的行为
o[Symbol.toPrimitive] = () => {console.log('toPrimitive'); return 'hello'};

console.log(o + '');
// toPrimitive
// hello
```

## typeof
JS提供了typeof运算符,用来返回操作数的类型,但typeof的运算结果,与运行时时的规定有不一致的地方.我们可以看下表来对照一下.
![avatar](/h5/images/ec4299a73fb84c732efcd360fed6e16b.png)
在表格中,多数项都是对应的,但是请提别注意null和function是特例.
