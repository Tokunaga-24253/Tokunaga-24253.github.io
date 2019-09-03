---
layout: post
title: Dark-Theme实现
subtitle: '"You eye will be grateful~"'
date: 2019-09-03
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 2019
  - 大学学习
---

> “🙉🙉🙉 ”

## 前言

之前一直有接触到手机 APP 的夜间模式，也曾经对微博没有夜间模式这个功能颇有怨言。想必大家都有在黑暗中看手机的时候把，就算你把屏幕亮度调最小，白光还是会或多或少地让你的眼睛感到一点不适。所以我在浏览我的个人网站时，突然想要学习并在项目中加入夜间模式这个功能。  
下面就是我的实现·

## 正文

预览：![gif](https://raw.githubusercontent.com/Tokunaga-X/Tokunaga-X.github.io/master/img/dark-theme.gif)

思路：

- html:提供一个按钮来与用户互动，赋予其切换正常/夜间模式的功能。
- css:根据不同的模式，赋予文字、背景相应的颜色。
- js:为按钮提供事件监控，控制 css 变化。

不同方法：

- 简单暴力版：创建两个 css class，一旦按钮切换，使用\*选择符为所有元素改变文字颜色以及背景颜色。（缺点：只适用于单色页面，有多种颜色的页面需要一个个元素改变，较麻烦）

```
// 类似这样
.dark-theme {
  background-color: black;
  color: white;
}
```

- 改进版：使用 css 变量进行控制颜色变化，在 html 标签中定义变量，然后在另一个 html 中重写变量来控制变换。

```
//css
html {
  height: 100%;
  font-family: "Montserrat";

  display: grid;
  align-items: center;
  justify-items: center;

  --bg: #fcfcfc;
  --bg-panel: #ebebeb;
  --color-headings: #0077ff;
  --color-text: #333333;
}

html[data-theme="dark"] {
  --bg: #333333;
  --bg-panel: #434343;
  --color-headings: #3694ff;
  --color-text: #b5b5b5;
}
//html
<html lang="en" data-theme="light">
//js
checkbox.addEventListener("change", function() {
      if (this.checked) {
        document.documentElement.setAttribute("data-theme", "dark");
      } else {
        document.documentElement.setAttribute("data-theme", "light");
      }
    });
```

PS：document.documentElement 属性返回页面根节点(一般是 html 标签)，这里你也可以用 body(document.body) 标签或者最大的那个 div 标签，只要能包裹住你想要控制颜色变换的区域就行。

你也可以加入 transition 属性使变换更加'smooth'。

See full code [here](https://codepen.io/designcourse/pen/OGVZjr)

---

—— 24253 记于 2019-9-3
