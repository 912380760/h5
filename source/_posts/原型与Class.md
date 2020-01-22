---
title: 原型与Class
date: 2020-01-21 16:50:29
tags: js
---

## 原型
面向对象的三个基本特征是：封装、继承、多态。
原型系统:
- 所有对象都有私有字段[[prototype]],就是对象的原型
- 读取一个属性,如果对象本身没有,者会继续访问对象的原型,直到找到或者原型为空为止.
ES6提供了一些列函数,直接地访问和操纵原型.三个方法分别问:
- **Object.create** 根据指定的原型创建新对象,原型可以是null;
- **Object.getPrototypeOf** 获得一个对象的原型
- **Object.setPrototypeOf** 设置一个对象的原型
```js
// 用原型来抽象猫和虎的例子
let cat = { 
    say() {
        console.log('meow~');
    },
    jump() {
        console.log('jump');
    }
}
let tiger = Object.create(cat, {
    say: {
        writable: true,
        value: () => { console.log('roar!') }
    }          
})

let yelloCat = Object.create(cat);
yelloCat.say(); // 'meow~'
let blueTiger = Object.create(tiger);
blueTiger.say(); // 'roar!'
```

## 类
ES6开始,[[class]]私有属性被**Symbol.toStringTag**代替,Object.prototype.toString 的意义从命名上不再跟 class 相关。我们甚至可以自定义 Object.prototype.toString 的行为.
```js
let o = { [Symbol.toStringTag]: 'MyObject' };
Object.prototype.toString.call(o); // [object MyObject]
```
### 模拟类
new运算符接受一个构造器和一组调用参数,实际上做了几件事:
- 以构造器的prototype属性为原型,创建新对象
- 将this和调用参数传给构造器,执行
- 如果构造器返回的是对象,则返回,否则返回第一步创建的对象.
new这样的行为,提供了两种方式,一是在构造器中添加属性,二是在构造器的prototype属性上添加属性
```js
function C1() {
    this.p1 = 1;
    this.p2 = function() {
        console.log(this.p1);  
    }
}
let obj1 = new C1;
obj1.p2();  // 1

function C2() {}
C2.prototype.p1 = 1;
C2.prototype.p2 = function() {
    console.log(this.p1);
}
let obj2 = new C2;
obj2.p2();  // 1 
```
### ES6中的类
ES6中引入了**class**关键字,并且在标准中删除了所有[[class]]相关的私有属性描述.
```js
// 类的基本写法
class Rectangle {
    constructor(height, width) {
        this.height = height;
        this.width = width;
    }
    
    get area() {
        return this.calcArea();
    }   
    calcArea() {
        return this.height * this.width;
    }
}

let obj1 = new Rectangle(10, 20);
obj1.area; // 200
```
此外,最重要的是,类提供了继承能力.
```js
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        console.log(this.name + ',发出声音.');   
    }
}

class Dog extends Animal {
    constructor(name) {
        super(name);
    }
    speak() {
        console.log(this.name + ',汪汪汪.');
    }
}
let d = new Dog('旺财');
d.speak(); //  旺财,汪汪汪.
```
