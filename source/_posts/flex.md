---
title: flex
date: 2019-07-12 15:57:38
tags:
---

# 基础知识和术语
## **flex容器(flex container)**
flex布局的容器
## **flex项(flex items)**
flex容器的直接子元素
## **main axis**
flex容器的主轴,flex项沿着主轴排布,注意主轴不一定是水平的,这取决于 **[flex-direction](#flex-direction)** 属性.
## **main-start|main-end**
分别表示主轴的开始位置和结束位置,flex项在容器中会从main-start到main-end排布.
## **main size**
flex项占据主轴的宽度或高度.flex项的main size 属性是要么是"宽度",要么是"高度",这取决于主轴方向.
## **cross axis**
垂直于主轴的轴线称为交叉轴,其方向取决于主轴方向.
## **cross-start|cross-end**
分别表示交叉轴的开始位置和结束位置
## **cross size**
flex项占据交叉轴的宽度或高度.
![avatar](/h5/images/flex.png)


# 父元素属性(flex container)
## flex-direction
定义flex项在flex容器中的排布方向.
- **row**: 行排布,从左到有(默认值)
- **row-reverse**: 反向行布局,从右到左
- **column**: 列布局,从上到下
- **column-reverse**: 反向列布局,从下到上.
![avatar](/h5/images/flex-direction.png)

## flex-wrap
默认情况下,flex项会尽可能尝试排在同一行,通过设置 **flex-wrap** 来决定flex项是否允许换行.
- **nowrap**: 所有的flex项都会在同一行上排布,不换行.(默认值)
- **wrap**: flex项将从上往下根据实际情况换行
- **wrap-reverse**: flex项从下往上根据实际情况换行.
![avatar](/h5/images/flex-wrap.png)

## flex-flow
这是 **[flex-direction](#flex-direction)** 和 **[flex-wrap](#flex-wrap)** 属性的缩写.同时定义flex容器的主轴和交叉轴.默认是 **row nowrap**.

## justify-content
定义flex项沿主轴方向的对齐方式
- **flex-start**: flex项从主轴开始位置(main-start)开始排布(默认值)
- **flex-end**: flex项从主轴的结束位置(main-end)开始布局
- **center**: flex项沿主轴居中排布
- **space-between**: flex项之间间隙均匀,两端没有空间,即我们常说的沿主轴两端对齐
- **space-around**: flex项之间间隙均匀,两端只有一半的空间
- **space-evenly**: flex项之间间隙均匀,两端空间也是均匀的.
![avatar](/h5/images/flex-justify-content.png)

## align-items(这是一个单行属性,当多行的时候时行为可能不准确)
定义flex项沿当前行在交叉轴上排布的默认行为,可以视为交叉轴上的对齐方式.
- **stretch**: 拉伸flex项以填满整个容器(这里需要特别注意: 如果flex项有尺寸属性(height/width/min系列/max系列,那么不会拉伸),(默认值).
- **flex-start**: flex项按照交叉轴的开始位置(cross-start)对齐
- **flex-end**: flex项按照交叉轴的结束位置(cross-start)对齐
- **center**: flex项以交叉轴为中心,居中对齐
- **baseline**: flex项按照他们的文字基线对齐
![avatar](/h5/images/flex-align-items.png)

## align-content(这是一个多行属性,单行不生效)
当交叉轴有剩余空间时, **align-content**可以设置flex容器中的行在交叉轴上如何分配剩余空间,与 **[justify-content](#justify-content)**相反.
- **strech**：多行拉伸以填充满整个剩余空间(默认值)
- **flex-start**: 多行在容器的开始位置排布
- **flex-end**: 多行在容器的结束位置排布
- **center**: 多行在容器的总结位置排布
- **space-between**: 多行均匀分布,两端没有空间
- **space-around**: 多行之间间隙均匀,两端只有一半的空间
- **space-evenly**: 多行之间间隙均匀,两端空间也是均匀的.
![avatar](/h5/images/flex-align-content.png)

# flex项属性(flex items)
## order
flex项按源顺序排布,控制它们在flex容器中显示顺序,默认值是0.

## flex-grow 
定义flex项在有可用剩余空间时拉伸比例,它接受的值作为比例,无单位,它规定了flex项应该占flex容器中可用空间比例.(默认值为0,负值无效).

## flex-shrink
定义flex项的收缩能力.(与flex-grow拉伸正好相反)

## flex-basis
定义了在分配剩余空间之前flex项默认的大小.
- **auto**: 按照其本来大小显示(默认值)
- **length**: 可以是长度值,也可以是数字单位.

## flex
**flex** 是 **[flex-grow](#flex-grow)** 、 **[flex-shrink](#flex-shrink)** 、 **[flex-basis](#flex-basis)** 三个属性的简写.其中第二个参数和第三个参数是可选的,默认值为**0 1 auto**.

## align-self
允许某个单独的flex项覆盖默认的对齐方式(或由 **[align-items](#align-items)** 指定的对齐方式).注意: **float**, **clear** 和 **vertical-align** 对flex项没有任何作用.