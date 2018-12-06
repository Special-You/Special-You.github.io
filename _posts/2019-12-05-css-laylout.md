---
title: css 布局
date: 2018-12-06 13:21:04
tags: css
categories: css
---

## 前言

## 1.圣杯布局
##### 三栏布局；主要内容写在前面，最先载入，但布局位于非最前。两侧定宽，分别位于中间主体两侧（外），中间流式（自动宽度）。
##### HTML代码

```
<body>
  <div class="container">
    <div class="main">Main Content</div>
    <div class="left">Left Side</div>
    <div class="right">Right Bar</div>
  </div>
</body>
```
##### HTML内容出现顺序：main、left、right，要求首先载入主体（重要）内容，然后加载侧边栏；
### 三个都左浮动，左右定宽，中间宽度自适应

##### 思路：为两侧设置相对定位（`position: relative`），同时父元素两侧留空白`padding`

```
.container {
  color: #fff;
 
  padding: 0 250px 0 200px; /* 为两侧留白 */
}
.main {
  float: left;
  background-color: #f00;
  height: 200px;
  
  width: 100%; /* 注意一定要有宽度，auto也不行，因为已经成为inline-block */
}
.left {
  float: left;
  height: 200px;
  background-color: #0f0;
 
  width: 200px;
  margin-left: -100px; /* Float to left */
 
  position: relative;
  left: -200px; /* 找回自身空间 */
}
.right {
  float: left;
  height: 200px;
  background-color: #00f;
 
  width: 250px;
  margin-left: -250px; /* Float to right */
 
  position: relative;
  right: -250px; /* 找回自身空间 */
}

```

## 2.双飞翼布局

#### HTML代码

```
<body>
  <div class="container">
    <div class="main"><div class="wrap">Main Content</div></div>
    <div class="left">Left Side</div>
    <div class="right">Right Bar</div>
  </div>
</body>
```
#### 为main添加wrap元素
```
.container {
  color: #fff;
 
  /*padding: 0 250px 0 200px;*/
}
.main {
  float: left;
  background-color: #f00;
  height: 200px;
  
  width: 100%; /* 注意一定要有宽度，auto也不行，因为已经成为inline-block */
}
.left {
  float: left;
  height: 200px;
  background-color: #0f0;
 
  width: 200px;
  margin-left: -100%; /* Float to left */
 
  /*position: relative; */
  /*left: -200px; */
}
.right {
  float: left;
  height: 200px;
  background-color: #00f;
 
  width: 250px;
  margin-left: -250px; /* Float to right */
 
  /*position: relative;*/
  /*right: -250px; */
}
.wrap {
  padding: 0 250px 0 200px;
}

```

## 3. 多列等高布局

```
.left, .content, .right {
    padding-bottom: 2000px;
    margin-bottom: -2000px;
}
.main {
overflow: hidden;
}
```
#### padding补偿法：
首先把列的**padding-bottom**设为一个足够大的值，再把列的**margin-bottom**设一个与前面的padding-bottom的正值相抵消的**负值**，**父容器设置超出隐藏**，这样子父容器的高度就还是它里面的列没有设定padding-bottom时的高度，当它里面的任一列高度增加了，则父容器的高度被撑到它里面最高那列的高度，其他比这列矮的列则会用它们的padding-bottom来补偿这部分高度差。因为背景是可以用在padding占用的空间里的，而且边框也是跟随padding变化的，这样就成功的使得三者列高最起码看起来是等高的。这样也就满足了我们的需求。





