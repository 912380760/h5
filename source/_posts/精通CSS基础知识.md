---
title: 精通CSS基础知识
date: 2020-08-19 18:23:23
tags: CSS
---

## 组织代码
- 关注点分离  
关注点分离的思想,即"分成小块,松散结合",每个"小块"都是一个模块,专注做好一件事情.

### 渐进增强  
为低版本的浏览器提供可用的内容,然后再为支持新特性的浏览器添加更多交互优化.
- 浏览器前缀
```css
.myThing {
    -webkit-transform: translate(0, 10px);
    -moz-transform: translate(0, 10px);
    -ms-transform: translate(0, 10px);
    transform: translate(0, 10px);
}
```
- 条件规则与检测脚本
如果希望根据浏览器是否支持某个CSS特性来提供不同的样式,可以选择@supports.还可以通过JavaScript来检测支持情况,比如使用Modernizr这个库.原理是通过给html添加支持信息,依据这些信息来编写CSS.
```css
@supports (display: grid) {
/* 在支持grid布局的浏览器中要应用的规则 */
}
```

### 结构化、语义化
- ID和class属性   
给元素添加类名时,即使类名明确用于样式,也不要体现出其视觉效果.正确的类名应该表示组件的类型.  
一般不建议把ID属性作为CSS的接入点.
- 结构化元素  
除了main之外,所有其他元素都可以在一个文档出现多次.
```html
<section>区块</section>
<header>头部</header>
<footer>底部</footer>
<nav>导航</nav>
<article>文章</article>
<aside>侧边栏</aside>
<main>主区域</main>
```
- div和span
在无需表示语义,仅需添加样式的情况中可以使用div和span,区别是div是块元素,span是文本元素.

- <i\>和<b\>
<i\>、<b\>与<em\>、<strong\>的区别是语义,<i\>、<b\>没有语义,<em\>、<strong\>有强调自己包含内容的意义.
