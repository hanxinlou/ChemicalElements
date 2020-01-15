---
title: HTML+CSS实现元素周期表
date: 2020/1/14 19:07:00
updated: 
categories: 
- DEMO
tags: 
- HTML
- CSS
---

逛B站的时候看到一个视频[「CSS 案例」元素周期表](https://www.bilibili.com/video/av80244004)
这不是2030年Adobe全家桶嘛
有点好看嘿嘿嘿
于是跟着Up主自己写了一份元素周期表
记录下自己写的时候的思路

### 实现效果图
<img src="/ChemicalElements/image.png">

### 1.拆解网页
- 首先将整个页面拆成顶部(`element-top`)和底部(`element-bottom`)两部分，如图
<img src="/ChemicalElements/image1.png">
```html
<html>
    <title>元素周期表</title>
    <body>
        <div class="element-top"></div>
        <div class="element-bottom"></div>
    </body>
```

- 顶部可以拆分成18列(`col`)，如图
<img src="/ChemicalElements/image2.png">
```html
<div class="element-top">
    <!--总共18个<div> -->
    <div class="col"></div>
    ...
    <div class="col"></div>
</div>
```

- 底部可以拆分成2行(`line`)，如图
<img src="/ChemicalElements/image3.png">
```html
<div class="element-bottom">
    <div class="line"></div>
    <div class="line"></div>
</div>
```

- 顶部每一列都可以拆分成对应的元素(`element`)，如图
<img src="/ChemicalElements/image4.png">
```html
<div class="col">
    <div class="element">H</div>
    ...
    <div class="element">Fr</div>   
</div>
```

- 底部每一行也都可以拆分成对应的元素(`element`)，如图
<img src="/ChemicalElements/image5.png">
```html
<div class="line">
    <div class="element">La</div>
    ...
    <div class="element">Lu</div>
</div>
```

### 布局
- 顶部采用`flex`布局并设置`justify-content`为`center`使得`col`位于父布局的中心
<img src="/ChemicalElements/image6.png">
```css
.element-top{
    display: flex;
    justify-content: center;
}
```

- 顶部的每一列采用顶部采用`flex`布局、设置`flex-direction`为` column`、`justify-content`为`flex-end`使得`element`纵向排列并位于父布局的底部
<img src="/ChemicalElements/image7.png">
```css
.col{
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
}
```

- 底部的每一行采用`flex`布局并设置`justify-content`为`center`使得`element`位于父布局的中心
<img src="/ChemicalElements/image8.png">
```css
.line{
    display: flex;
    justify-content: center;
}
```

### 设置盒模型属性

-  选择所有元素设置共同属性
```css
*{
    /* *就是选择所有元素 */
    margin: 0;
    padding: 0;
    /* border-box:width 和 height 属性包括内容，内边距和边框，但不包括外边距 */
    box-sizing:border-box;
} 
```

- 设置顶部盒模型属性
```css
.element-top{
    width: 80rem;
    height: 25rem;
    margin: 5rem 8rem 3rem 8rem;
    background : lightblue
}
```

**Tip:** 为了更好地观察布局和盒模型可以添加`background`属性，以下每个盒模型均添加，完成所有盒模型之后再删除即可

- 设置顶部每一列盒模型属性
```css
.col{
    width: 4rem;
    height: 100%;
    margin: 0rem 0.2rem;
    background : lightgray
}
```

- 设置底部部盒模型属性
```css
.element-bottom{
    width: 80rem;
    height: 25rem;
    margin: 3rem 8rem 3rem 7.5rem;
    background : lightgreen
}
```

- 设置底部每一行盒模型属性
```css
.line{
    width: 100%;
    height: 4rem;
    margin: 0.5rem;
}
```

### 设置盒模型颜色
根据效果图发现不同类别的元素其配色是不同的，所以新建颜色的类选择器来区分这些配色不同的元素
比如**氢**一类的元素其颜色的类选择器如下
```css
.base-color{
    background: rgb(0, 33, 63);
    color: rgb(154, 206, 255);
    border: 4px solid rgb(154, 206, 255);
}
```
以此新建`color-1、color-2...`共10个类选择器来区分

### 字体大小问题
做到这一步其实已经算是完成了但是一看效果图这个字体怎么这么小？！！！
<img src="/ChemicalElements/image10.png">
噢我忘了设置字体大小
新建2个字体大小的类选择器`font-size1、font-size2`
```css
.fontsize-1{
    font-size: 30px ;
}
.fontsize-2{
    font-size: 27px ;
}
```

如果没有设置两个选择器你可能因为某些元素是三个英文字母所以越过边界而抓狂
<img src="/ChemicalElements/image9.png">

所以还是乖乖建两个来区分吧

到这里就画完~~2030Adobe全家桶~~元素周期表了
原Up主还做了点击的特效，我有空研究下再更新23333