---
layout:     post
title:      Beautiful-CSS
subtitle:    "\"值得收藏的CSS特效\""
date:       2019-07-17
author:     24253
header-img: img/Learning.jpg
catalog: true
tags:
    - CSS
    - 2019
---

> “🙉🙉🙉 ”

## 前言

经常看到一些'高级'的CSS特效，在这边收录一下，以便提高自己。

## 正文

---

渐变背景颜色加转换：  

展示：![gif1](../img/cssAnimation1.gif)

css代码：
```
xxx {
    background-image: linear-gradient(to left, #12CBC4, #0652DD, #12CBC4);
    background-size: 200%;
    color: #fff;
    transition: 0.6s;
}
xxx:hover {
    background-position: right;
}
```
重点：利用CSS3中的**linear-gradient**函数来创建一个渐变的颜色背景，再用**background-size**属性放大一倍，使显示一半的图像，再在*hover*中使用**background-position**属性控制图像的显示方向从右开始。

PS:关于[linear-gradient](https://www.runoob.com/cssref/func-linear-gradient.html)[background-position](http://www.w3school.com.cn/cssref/pr_background-position.asp)的详细介绍。

---

利用：before/after做出来的hover效果

css代码:
```
xxx {
    color: inherit;
    letter-spacing: 1px;
    position: relative;
    margin: 0 3rem;
    padding: 5px 0;
}
xxx:last-child {
    margin-right: 40px;
}
xxx::before,
xxx::after
{
    content: '';
    width: 100%;
    height: 2px;
    background-color: crimson;
    left: 0;
    position: absolute;
    //scale动画
    transform: scaleX(0);
    //设置动画时间
    transition: all .5s;
}
xxx::before
{
    //上半部分
    top: 0;
    //
    transform-origin: left;
}
xxx::after
{
    //下半部分
    bottom: 0;
    transform-origin: right;
}
xxx:hover::before,
xxx:hover::after
{
    transform: scaleX(1);
}
```

---



## 后记

—— 24253 记于 2019-3-19


