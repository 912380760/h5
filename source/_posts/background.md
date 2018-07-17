---
title: background
date: 2018-07-17 15:21:37
tags: css
---


## background
* **background-color** 
背景颜色, 可以使用[linear-gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient)和[radial-gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient)
* **background-image** 
背景图片，可以写多个，用逗号隔开，也可以使用渐变
* [**background-repeat**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-repeat) 
背景重复
repeat默认值 repeat-x repeat-y no-repeat 
space 图片会尽可能的重复，不会裁切，第一个和最后一个固定在左右两边，多余间距平均分配
round 缩放图片的大小，，让图片刚好铺满整个背景。
* [**background-attachment**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-attachment) 
背景在视口中是否随包含它的区块滚动
```
// 背景相对于元素本身固定，而不是随着它的内容滚动
background-attachment: scroll;
// 背景相对于视口固定
background-attachment: fixed;
// 背景相对于元素的内容固定，背景将随着元素内容滚动
background-attachment: local;
```
* **background-position** 
背景定位
```
/* 关键字 */
background-position: top;
background-position: bottom;
background-position: left;
background-position: right;
background-position: center;

/* 百分比 */
background-position: 25% 75%;

/* 长度 */
background-position: 20px 20px;
background-position: 1cm 2cm;
background-position: 10ch 8em;

/* 多个背景图 */
background-position: 0 0, center;

/* 怪异的简写语法 */
// 在 background 简写属性中指定 background-size 时，需要同时提供一个 background-position 值
// (哪怕它的值就是其初始值也需要写出来)，而且还要使 用一个斜杠(/)作为分隔
background: url(tr.png) no-repeat top right / 2em 2em;
```

* [**background-size**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-size) 
背景大小
```
/* 关键字 */
background-size: cover;  // 居中裁剪
background-size: contain; // 按比例最大化显示

/* 一个值: 这个值指定图片的宽度，图片的高度隐式的为auto */
background-size: 50%;
background-size: 3em;
background-size: 12px;
background-size: auto;

/* 两个值 */
/* 第一个值指定图片的宽度，第二个值指定图片的高度 */
background-size: 50% auto;
background-size: 3em 25%;
background-size: auto 6px;
background-size: auto auto;

/* 逗号分隔的多个值：设置多重背景 */
background-size: auto, auto; // 不同background-size:auto auto;
background-size: 50%, 25%, 25%;
background-size: 6px, auto, contain;
```
* [**background-origin**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-origin) 
背景圆点位置
border-box 
padding-box 
content-box 
* [**background-clip**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip)
背景范围
border-box 背景范围到border
padding-box 背景范围到padding
content-box 背景范围只有content
text 背景被剪切到前景文本中
* [**background-blend-mode**](https://developer.mozilla.org/en-US/docs/Web/CSS/background-blend-mode)
定义该元素的背景图片，以及背景色如何混合。