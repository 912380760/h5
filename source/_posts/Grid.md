---
title: Grid
date: 2019-07-09 16:17:40
tags: css
---

## 重要术语
* 网格容器(Grid Container)
应用 **display: grid** 的元素.

* 网格项(Grid Item)
网格容器的直接子元素.这里**item**就是网各项,但是**sub-item**不是.
```html
<div class="container">
    <div class="item"></div> 
    <div class="item">
    <p class="sub-item"></p>
        </div>
    <div class="item"></div>
</div>
```
* 网格线(Grid Line)
构成网格结构的分界线.它们既可以是垂直的(列网格线column grid lines),也可以是水平的(行网格线row grid lines).

* 网格轨道(Grid Track)
两条相邻网格线之间的空间,你可以把它们想象成网格的行或者列.

* 网格单元格(Grid Cell)
网格线之间形成的单元格

* 网格区域(Grid Area)
任意数量的网络单元格组成的网络区域

## grid-template-columns / grid-template-rows
值:
- **track-size**: 长度值,百分比,或者等份网络容器可用空间(fr单位)
- **line-name**: 任意名称
使用空格分隔值列表,用来定义网格的行和列.这些值表示网格轨道大小,它们之间的[]表示网格线.  
```css
/*不填写网格线名称时,网格线会自动分配正数和负数(倒数)名称.*/
.container {
    grid-template-columns: 40px 50px auto 50px 40px;
    grid-template-rows: 25% 100px auto;
}
```
![avatar](/h5/images/grid-columns.png)

```css
/*明确的指定网格线(Grid Line)名称*/
.container {
    grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
    grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```
![avatar](/h5/images/grid-columns2.png)

```css
/*一条线可以有多个名称,名称可以相同*/
.container {
    grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}

/*如果你定义多重复值,可以使用repeat()表示法来简化定义*/
.container {
    grid-template-columns: repeat(3, 20px [col-start]);
}
/*等价于*/
.container {
    grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
}

/*fr单位用等份网络容器剩余空间来设置网络轨道的大小*/
.container {
    grid-template-columns: 1fr 1fr 1fr;
}
/*剩余可用空间是出去所有非灵活网各项之后计算得到的*/
.container {
    grid-template-columns: 1fr 50px 1fr 1fr;
}
```

## grid-template-areas
指定网格区域名称来定义网格模板,点号(.)代表空单元格.这个语法本身可视作网格的可视化结构.
值:
- **grid-area-name**: 网格区域名称
- **.**(点号): 代表空的单元格
- **none**: 不定义网格区域
```css
.container {
    grid-template-columns: 50px 50px 50px 50px;
    grid-template-rows: auto;
    grid-template-areas: 
        "header header header header"
        "main main . sidebar"
        "footer footer footer footer";
}
```
当你使用这种语法时,区域两端的网格线会自动命名,如你的网格区域的名字是header,该区域的起始行和起始列的名称将为header-start,而最后一行网格线和最后一列的名称为header-end.
![avatar](/h5/images/grid-areas.png)

## grid-template
**grid-template-rows**, **grid-template-columns**, **grid-template-areas**的简写属性. 
```css
.container {
    grid-template:
        [row1-start] "header header header" 25px [row1-end]
        [row2-start] "footer footer footer" 25px [row2-end]
        / auto 50px auto;
}
/*等价于*/
.container {
    grid-template-rows: [row1-start] 25px [row1-end row2-start] 25px [row2-end];
    grid-template-columns: auto 50px auto;
    grid-template-areas: 
        "header header header" 
        "footer footer footer";
}
```
由于**grid-template**不会充值隐式网格属性(**grid-template-rows**, **grid-template-columns**, **grid-template-areas**),建议使用**grid**属性而不是**grid-template**.

## grid-column-gap/grid-row-gap
 指定网格线的大小,只能在列/行之间创建间距，网格外部边缘不会有这个间距.  
 注意这两个属性在现代浏览器已经可以删除grid-前缀,重命名为**column-gap**和**row-gap**.
 ```css
.container {
    grid-template-columns: 100px 50px 100px;
    grid-template-rows: 80px auto 80px; 
    grid-column-gap: 10px;
    grid-row-gap: 15px;
}
```
![avatar](/h5/images/grid-gap.png)
 
## grid-gap
**grid-column-gap**和**grid-row-gap**的简写
如果grid-column-gap没定义,被设置为等同于grid-column-gap的值
```
.container{
    grid-gap: <grid-row-gap> <grid-column-gap>;
}

.container{
    /* 设置 grid-column-gap 和 grid-row-gap */  
    grid-column-gap: 10px;
    grid-row-gap: 10px; 
    
    /* 等价于 */  
    grid-gap: 10px 10px;
    
    /* 等价于 */  
    grid-gap: 10px;
}
```

## justify-items
沿着行轴线对其网格项(相反的属性是**align-items**),此值适用于容器内所有网格项.
值:
- **start**: 左侧对齐
- **end**: 右侧对齐
- **center**: 水平居中对齐
- **stretch**: 填满单元格的宽度(默认值)
```
.container {
    justify-items: start | end | center | stretch;
}
```
![avatar](/h5/images/justify-items.png)

## align-items
沿着列轴线对其网格项
- **start**: 顶部对齐
- **end**: 底部对齐
- **center**: 垂直居中对齐
- **stretch**: 填满单元格的宽度(默认值)
![avatar](/h5/images/align-items.png)

## place-items
**align-items** 和 **justify-items** 的简写形式.
```
.container {
    place-items: <align-items> <justify-items>;
}
```

## justify-content
你的网格大小小于网格容器大小是,设置网格容器内的网格对齐方式.此属性是沿着行轴线对齐网格.
值:
- **start**: 左侧对齐
- **end**: 右侧对齐
- **center**: 水平居中对齐
- **stretch**: 调整网格项的宽度,允许该网格填充满整个网格容器的宽度
- **space-around**: 每个网格项之间间隙均匀,左右两端只有一半的空间
- **space-between**: 每个网格项之间间隙均匀,左右两端没有空间
- **space-evenly**: 每个网格项之间间隙均匀,左右两端空间也是均匀的.
![avatar](/h5/images/justify-content.png)

## align-content
你的网格大小小于网格容器大小是,设置网格容器内的网格的对齐方式,此属性是验证列轴线对齐网路.
值:
- **start**: 顶部对齐
- **end**: 底部对齐
- **center**: 垂直居中对齐
- **stretch**: 调整网格项的高度,允许该网格填充满整个网格容器的高度
- **space-around**: 每个网格项之间间隙均匀,上下两端只有一半的空间
- **space-between**: 每个网格项之间间隙均匀,上下两端没有空间
- **space-evenly**: 每个网格项之间间隙均匀,上下两端空间也是均匀的.
![avatar](/h5/images/align-content.png)

## place-content
**align-content**和**justify-content**的简写形式.除了Edge之外所有主要浏览器都支持**place-content**简写属性.

## grid-auto-columns / grid-auto-rows
任何自动生成的网络轨道(隐式轨道)的大小,当网格中的网格多于单元格时,或者网格项位于显示网格之外,会创建隐式轨道.
```html
<div class="container">
    <div class="item-a">item-a</div>
    <div class="item-b">item-b</div>
</div>

<style>
/*生成一个2*2的网格*/
.container {
    grid-template-columns: 60px 60px;
    grid-template-rows: 90px 90px
}
.item-a {
    grid-column: 1 / 2;
    grid-row: 2 / 3;
}
/*.item-b 从第 5 条列网格线开始到第 6 条列网格线结束，*/
.item-b {
    grid-column: 5 / 6;
    grid-row: 2 / 3;
}
</style>
```
![avatar](/h5/images/grid-auto.png)

## grid-auto-flow
如果你没有明确放置网格项,自动放置算法会自动放置这些网格项
值:
**row**: 依次填充每行,根据需要添加新行(默认值)
**column**: 依次填入每列,根据需要添加新列
**dense**: 在稍后出现较小的网格项时,尝试填充网格项中较早的空缺
请注意,**dense**只会更改网格项的可视顺序,并可能导致它们出现乱序,这对可访问性不利.

```html
<section class="container">
  <div class="item-a">item-a</div>
  <div class="item-b">item-b</div>
  <div class="item-c">item-c</div>
  <div class="item-d">item-d</div>
  <div class="item-e">item-e</div>
</section>

<style>
/*定义一个5列2行的网格*/
.container {
    display: grid;
    grid-template-columns: 60px 60px 60px 60px 60px;
    grid-template-rows: 30px 30px;
}

/*指定两个item位置*/
.item-a {
    grid-column: 1;
    grid-row: 1 / 3;
}
.item-e {
    grid-column: 5;
    grid-row: 1 / 3;
}
</style>
```
![avatar](/h5/images/auto-flow1.png)

```css
/*把 grid-auto-flow 设成了 column*/
.container {
    display: grid;
    grid-template-columns: 60px 60px 60px 60px 60px;
    grid-template-rows: 30px 30px;
    grid-auto-flow: column;
}
```
![avatar](/h5/images/auto-flow2.png)

## grid 
以下属性的简写: **[grid-template-rows](#grid-template-columns-grid-template-rows)**, **[grid-template-columns](#grid-template-columns-grid-template-rows)**, **[grid-template-areas](#grid-template-areas)**, **[grid-auto-rows](#grid-auto-columns-grid-auto-rows)**, **[grid-auto-columns](#grid-auto-columns-grid-auto-rows)**, 和 **[grid-auto-flow](#grid-auto-flow)**. 
以下两个紧挨着的代码是等效的
```css
.container {
  grid: 100px 300px / 3fr 1fr;
}
.container {
  grid-template-rows: 100px 300px;
  grid-template-columns: 3fr 1fr;
}

.container {
  grid: auto-flow / 200px 1fr;
}
.container {
  grid-auto-flow: row;
  grid-template-columns: 200px 1fr;
}

.container {
  grid: auto-flow dense 100px / 1fr 2fr;
}
.container {
  grid-auto-flow: row dense;
  grid-auto-rows: 100px;
  grid-template-columns: 1fr 2fr;
}

.container {
  grid: 100px 300px / auto-flow 200px;
}
.container {
  grid-template-rows: 100px 300px;
  grid-auto-flow: column;
  grid-auto-columns: 200px;
}

.container {
  grid: [row1-start] "header header header" 1fr [row1-end]
        [row2-start] "footer footer footer" 25px [row2-end]
        / auto 50px auto;
}
.container {
  grid-template-areas: 
    "header header header"
    "footer footer footer";
  grid-template-rows: [row1-start] 1fr [row1-end row2-start] 25px [row2-end];
  grid-template-columns: auto 50px auto;    
}

```