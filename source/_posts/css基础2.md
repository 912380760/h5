---
title: CSS字体与排版
date: 2018-07-03 00:12:04
tags: css
---

## font
大部分字体属性的默认值是normal；可以使用< br >标签手动换行，回车默认是不会换行的；字体属性的简写顺序实在太难记了，一般不用简写。

### 字体样式
* **color** 字体颜色
* **font-family** 字体种类
* **font-size** 字体大小
* **font-style** 斜体 italic oblique
* **font-weight** 字体粗细 blod 100-900
* **text-transform** 字体大小写转换 uppercase lowercase capitalize full-width
* **text-decoration** 上下中划线 underline overline line-through
* **text-shadow** 文本阴影 可以应用多个，以逗号隔开 1px 1px 2px #aaa

### 字体布局
* **text-align** 文本对齐 left right center justify
* **line-height** 行高 不带单位默认为字体的倍数
* **letter-spacing** 字母间距 中文
* **word-spacing** 单词间距 
* **text-indent** 首行留白，可以为负数
* **white-space** 文本空白和换行 nowrap 
* **text-overflow** 文本溢出  clip ellipsis
* **[word-break](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-break)** 单词内部换行 break-all keep-all

## display
### block 
* 可以设置宽高，默认独占一行，宽度默认100%
* 可以自由设置margin 和 padding
* 常见的标签 div p h1-h6 ul ol dl 

### inline
* 宽高靠内容撑开，可以和其他元素在一行
* 无法设置宽高
* margin 和 padding 左右有效 上下无效
* 常见的标签 span a

### inline-block
综合了block 和 inline 的特性
* 可以设置宽高，也可以让内容撑开作为宽高
* 可以和其他元素在一行
* 可以自由设置margin 和 padding
* 常见的标签 img

## float
float的值有**left** **right** **none**；
浮动主要的作用是为了排版，让元素向左或向右对其；
使用浮动后会造成高度塌陷，需要使用clear: both;清除浮动带来的高度塌陷问题；
现在最主流的清除浮动方法：after伪元素清除浮动；
```
.fix {
  zoom:1;
}
.fix::after {
  display: block;
  content: 'clear';
  height: 0;
  clear: both;
  overflow: hidden;
  visibility: hidden;
}

```

## visibility opacity
### visibility
设置元素是否隐藏，但是并不脱离文本流，元素的位置还是被占用的，hidden 隐藏，visible 显示。
### opacity
设置元素的透明度，值为0-1；因为浏览器渲染机制的问题，background: rgba(0,0,0,.1);并不等于background: rgb(0,0,0); opacity: .1; 


## [position](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position#Sticky_positioning)
文档流：正常的元素堆叠效果。
absolute 和 fixed 会脱离文档流，元素并不占用正常文档流的空间。
* **relative**  
静态定位，根据自身定位
* **absolute**
相对定位，根据最近的有定位属性的父元素定位
* **fixed**
固定定位，根据浏览器视口定位
* **sticky**
浏览器滚动到该元素后再悬浮，有点像relative和fixed的结合

**left** **right** **top** **bottom**
规定具体的定位值，可以是负数，可以使用%；

**z-index**
元素的层级，只有有定位属性的元素才可以设置，越大的显示在越上方，可以为负数，小于-1会隐藏元素

## overflow 
内容溢出时的现实方法
* **visible** 默认值，内容可以超出元素
* **hidden** 超出隐藏
* **scroll** 始终显示滚动条
* **auto** 只有在内容超过是显示滚动条
* **overflow-x** 水平方向的内容溢出
* **overflow-y** 垂直方向的内容溢出 