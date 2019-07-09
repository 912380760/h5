---
title: BFC
date: 2019-07-09 15:01:46
tags: css
---

## BFC 块级格式化上下文
用于决定块盒子的布局及浮动互相影响范围的一个区域.

## BFC的创建方法
* 根元素或其它包含根元素的元素
* 浮动**float: left/right**
* 绝对定位元素 **pisition: absolute/fixed**
* 表格元素 **table/table-cell/table-caption...**
* **overflow: hidden/auto/scroll**
* 弹性元素**flex/inline-flex**
* 网格元素**grid/inline-grid**
* **[contain](https://developer.mozilla.org/zh-CN/docs/Web/CSS/contain): layout/content/strict**
* **[column-count](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-count)**/**[column-width](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-width)**不为auto
* **display: flow-root**;(这个新属性就是为了创建一个新的BFC)

## BFC的效果
* 内部的盒子会在垂直方向一个接一个排列;
* 处于同一个BFC中的元素相互影响,浮动只影响同一个BFC的元素,不会影响其他BFC.Margin塌陷也只会发生在同一个BFC内.
* 计算高度的时候,会考虑BFC包含的所有元素,连浮动元素也参与计算;

## 范例
下面例子中,我们让float盒子浮动,浮动脱离了文档流,所以box的background和border仅仅包含了内容,不包含整个浮动.
``` html
<div class="box">
    <div class="float">I am a floated box!</div>
    <p>I am content inside the container.</p>
</div>

<style>
.box {
    background-color: rgb(224, 206, 247);
    border: 5px solid rebeccapurple;
}

.float {
    float: left;
    width: 200px;
    height: 150px;
    background-color: white;
    border:1px solid black;
    padding: 10px;
}      
</style>

// 创建一个BFC包含这个浮动
<style>
.box {
    background-color: rgb(224, 206, 247);
    border: 5px solid rebeccapurple;
    display: flow-root;
}
</style>
```
盒子浮动,超出box
<img src="/h5/images/BFC1.png" style="margin-left: 0;">
创建一个BFC包含这个浮动
<img src="/h5/images/BFC2.png" style="margin-left: 0;">

## 参考资料

[学习 BFC (Block Formatting Context) - 掘金](https://juejin.im/post/59b73d5bf265da064618731d)
[格式化上下文 - Web 开发者指南 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)
