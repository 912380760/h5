---
title: React核心概念
date: 2019-08-07 18:56:28
tags:
---

## JSX
- JSX中用{}嵌入表达式
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
可以通过引号或大括号来赋值DOM属性值,同一个属性只能选择其中一种方式,JSX里的class变成className.
```jsx harmony
// 通过引号
const element = <div tabIndex="0"></div>;
// 通过大括号
const element2 = <img src={avatarUrl} />;
```
- JSX防注入攻击 React DOM在渲染所有输入内容前默认会进行转译,所有内容在渲染前都被转成字符串.

## 组件&Props
组件,接受任意的入参(即"props"),并返回用于描述页面展示内容的React元素
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
React元素既可以是DOM标签,也可以是自定义的组件
``````


