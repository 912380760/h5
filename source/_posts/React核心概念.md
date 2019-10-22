---
title: React核心概念
date: 2019-08-07 18:56:28
tags: react
---

## JSX
- JSX中用 **{}** 嵌入表达式
```jsx harmony
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;
```
- JSX也是一个表达式
可以在if语句和for循环的代码块中使用JSX,将JSX赋值给变量,把JSX当作参数传入,从函数中返回JSX
```jsx harmony
function getGreeting(user) {
    if (user) {
        return <h1>Hello, {formatName(user)}!</h1>;
    }
    return <h1>Hello, stranger.</h1>;
}
```
- JSX特定属性
可以通过引号或大括号来赋值DOM属性值,同一个属性只能选择其中一种方式,JSX里的class变成**className**.
```jsx harmony
// 通过引号
const element = <div tabIndex="0"></div>;
// 通过大括号
const element2 = <img src={avatarUrl} />;
```
- JSX防注入攻击 React DOM在渲染所有输入内容前默认会进行转译,所有内容在渲染前都被转成字符串.

## 组件&Props
组件接受任意的入参(即"**props**"),并返回用于描述页面展示内容的React元素
- React会将以小写字母开头的组件视为原生DOM标签,大写字母开头的为自定义组件.
- 函数组件和Class组件
```jsx harmony
// 函数组件
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

// Class组件
class Welcome extends React.Component {
    render() {
        return <h1>Hello, {this.props.name}</h1>;
    }
}
```
- 渲染组件  
React元素既可以是DOM标签,也可以是自定义的组件,当React元素为自定义组件时,它会将JSX所接受的属性转换为单个对象传递给组件,这个对象被称为"**Props**".
````jsx harmony
// DOM元素
const element = <div></div>;
// 自定义组件
const element2 = <Welcome name="Sara" />;
````
- 组件最外层只能有一标签

## State & 生命周期
### state
- 构造函数是唯一可以给 **this.state** 赋值的地方
- 不要直接修改 **State** ,不会重新渲染组件,应该使用 **setState()** 修改state,使用constructor需要把 **props** 传递到父类的构造函数中
```jsx harmony
// 例子
class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = {date: new Date()};
    }
    
    componentDidMount() {
        this.timerID = setInterval(
            () => this.tick(),
            1000
        );
    }
    
    tick() {
        this.setState({
            date: new Date()
        });
    }
}
```
- **State** 的更新可能是异步的, 所以不要依赖他们的值来更新下一个状态  
解决办法: 让 **setState()** 接收一个函数而不是一个对象.这个函数用上一个state作为第一个参数,将此次更新被应用时的props作为第二个参数
```jsx harmony
// Wrong
this.setState({
    counter: this.state.counter + this.props.increment,
});
// Correct
this.setState((state, props) => {
    return {
        counter: state.counter + props.increment,
    }
})
```
- 数据是向下流动的, 任何的state总是所属于特定的组件,而且从该state派生的任何数据或UI只能影响树中"低于"它们的组件.

## 事件处理
- React 事件采用小驼峰式,而不是纯小写.
- 使用JSX语法时你需要传一个函数作为事件处理函数,而不是一个字符串
```jsx harmony
// 传统HTML
<button onclick="activateLasers()">
  Activate Lasers
</button>

// React
<button onClick={activateLasers}>
    Activate Lasers
</button>
```
- 不能通过返回false的方式阻止默认行为,必须显示的调用**preventDefault**
```jsx harmony
// 传统HTML
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>

// React
function ActionLink() {
    function handleClick(e) {
        e.preventDefault();
        console.log('The link was clicked.');
    }
    
    return (
        <a href="#" onClick={handleClick}>
            Click me
        </a>
    )
}
```
- 绑定this的三种方法
```jsx harmony
// 通过bind绑定
class Toggle extends React.Component {
    constructor(props) {
        this.handleClick = this.handleClick.bind(this);
    }
}

class Toggle extends React.Component {
    // 通过箭头函数
    handleClick = () => {
        
    }    
}

class Toggle extends React.Component {
    handleClick () {
        
    }
    render() {
        // 通过在事件内写箭头函数,需要显示的传递e(event合成事件)
        <button onClick={(e) => this.handleClick(e)}></button>
    }
}

class Toggle extends React.Component {
    handleClick () {
        
    }
    render() {
        // 通过在事件内使用bind绑定
        <button onClick={this.handleClick.bind(this)}></button>
    }
}
``` 
- 向事件处理程序传递参数
```jsx harmony
// 通过箭头函数
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>;
// 通过bind, 事件对象e会被作为第二个参数隐形传递
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>; 
```

## 条件渲染
