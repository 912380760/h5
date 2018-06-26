---
title: css基础
date: 2018-06-27 00:06:00
tags: css
---

## CSS形式
* 内联样式
* 内部样式表
* 外部样式表

```
// 内联样式，写在元素的style属性里
<div style="color: red;">test</div>

// 内部样式表，将CSS放置在<style>元素中
<style>
.test {
    color: red;
} 
</style>

// 外部样式表，保存个独立的.css 的文件，通过link元素引入
<link rel="stylesheet" href="../index.css">
```

## 选择器
### 简单选择器
* 标签选择器 标签名
* class选择器 .classname
* id选择器 #idname

### 伪类
以冒号(:)作为前缀添加到选择器的末尾，如 .classname:hover
* :hover 鼠标经过元素
* [:nth-child()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-child) 选择匹配的第N个元素
* :first-child() 选择匹配的第一个元素
* :last-child() 选择匹配的最后一个元素

### 伪元素
以冒号(::)作为前缀添加到选择器的末尾，如 .classname::after
* [::after](https://codepen.io/912380760/pen/ERepNO) 在标签的前面插入一个元素
* [::before](https://codepen.io/912380760/pen/ERepNO) 在标签的后面插入一个元素

### 组合选择器
* A,B 满足A或B的任意元素
* A B B是A的后代节点
* A > B B是A的子节点
* A + B B是A的下一个兄弟节点
* A ~ B B是A之后的兄弟节点中的任意一个

## CSS单位和值
### 数值
0.5可以缩写成.5 
* px 
* em 父元素的字体大小 
* rem HTML的字体大小
* vw 视口宽度的1/100
* vh 视口高度的1/100
* % 父节点的百分比

### 颜色值
* red 关键字
* #00ff00 十六进制值，可以缩写 #0f0 
* rgb()和rgba 
* hsl()和hsla  

## 继承
子元素会默认继承父节点的字体相关的一些属性，对 font-family 和 color

#### 控制继承
CSS为处理继承提供的通用属性，可以让元素继承或者不继承父元素的属性
* inherit 继承父元素属性， 如：width: inherit;继承父元素的宽度
* initial 设置成浏览器的默认值

## 权重
* !important > 内联样式 > id > class > 标签选择器 > 伪类
* 相同权重下书写在后面的样式比前面的高

## 盒子模型
<img src="./images/盒模型.png" style="margin-left: 0;" width="50%" height="50%">
### content
* width 规定content的宽度
* height 规定content的高度
* min-width 规定content的最小宽度，如果width的值比min-width小，会使用min-width的值
* min-height 规定content的最小高度
* max-width 规定content的最大宽度，如果width的值比max-width大，会使用max-width的值
* max-height 规定content的最大高度

### padding 
背景区域默认包括padding，padding有4个值顺序为top、right、bottom、left
* padding: 10px === padding: 10px 10px 10px 10px; 一个值代表4个方向的值相同
* padding: 10px 20px === padding: 10px 20px 10px 20px; 第一个值上下，第二值左右
* padding: 10px 20px 30px === padding: 10px 20px 30px 20px; 中间值是左右，第一个值上，第三个值下

### margin 
margin和padding类似，不通点
* margin不在背景区域
* margin可以为负数
* 两个元素连在一起，上下margin重叠，只保留两者较大的
* 如果一个元素只有margin是没有高度的，只有padding有高度
* margin值有auto值，一般用于元素居中

### border
border是属性的简写，和padding一样也是有4个方向，下面是简写顺序
* border-style 边框样式 solid（实线）
* border-width 边框宽度
* border-color 边框颜色 
* border: none 去除border属性