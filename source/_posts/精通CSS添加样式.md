---
title: 精通CSS添加样式
date: 2020-08-19 19:04:03
tags:
---

## CSS选择符
- 类型选择符  
```css
p {
    color: black;
}
```
- 后代选择符
```css
blockquote p {
    padding-left: 2em;
}
```
- id选择符
```css
#intro {
    font-weight: bold;
}
```
- class选择符
```css
.data-posted {
    color: #ccc;
}
```
- 子选择符
```css
#nav > li {
    padding-left: 20px;
}
```
- 相邻同辈选择符
```css
/* 同级h2紧跟着的p */
h2 + p {
    font-size: 1.4rem;
}
```
- 一般同辈选择符
```css
/* 同级h2后面所有的p */
h2 ~ p {
    font-size: 20px;
}
```
- 通用选择符
```css
/* .product 下的所有元素 */
.product > * {
    /* ... */
}
```
- 属性选择器
理论上能对class属性使用这个选择符
```css
/* ^匹配以某些字符开头的属性值 */
a[herf^="http:"] {
    /* ... */
}

/* $匹配以某些字符结尾的属性值 */
a[herf$=".jpg"] {
    /* ... */
}

/* *匹配包含某些字符的属性值 */
a[herf*="/about/"] {
    /* ... */
}

/* ~匹配以空格分隔的字符串中的的属性值 */
a[rel~="next"] {
    /* ... */
}

/* |匹配开头或者开头加短划线的的属性值,如下列例子匹配: en和en-us */
a[lang|="en"] {
    /* ... */
}
```

- 伪元素  

- 伪类  

