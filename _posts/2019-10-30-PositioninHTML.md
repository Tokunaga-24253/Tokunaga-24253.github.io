---
layout: post
title: JS文件放在HTML尾部是最好的吗？
subtitle: '"#LearnedfromYoutube"'
date: 2019-10-30
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 生活
---

> “🙉🙉🙉 ”

## 前言

我们(前端学习者)常说的页面优化方法最常见的一条就是---把 JS(script)标签放在 html 尾部(body 后面)，把 CSS(link)标签放在 html 头部中。

为什么？

- 因为浏览器在解析 html 文件的时候碰到 js 和 css 标签会进行资源的请求，收到请求后会解析相应的 js/css 文件。**重点**来了：在构建 dom 树的同时会构建 cssom 树，两者都构建好了会合并构建成 render 树，这样我们需要 cssom 树构建地越早越好，同时 css 的下载和解析是不会阻塞 html 树的构建的，所以我们要把 css 放在头部。
- js 就不一样了。如果解析 html 的过程中遇到了 script 标签，那么 dom 树的构建会被暂停，直至 js 文件下载并解析/执行完成后才会继续构建。那么 dom 树构建被延缓了，页面的加载也就会处于一种视觉上的卡住的状态，我们不想要用户看到这个。于是我们要尽量把 js 放在最底部(</body>标签前))

## 正文

前面关于为什么要这样做的原因也解释得挺详细的了。

那么，有没有更好的办法？能够让 js 脚本尽可能地靠后执行呢？

最近 youtube 给我推荐了一个 Google Chrome 团队制作的视频，内容就是关于如何尽可能地让 js 脚本在网页加载时解析执行尽可能靠后。

视频介绍了三个等级的优化方法：

- Good：把不是必要在 head 中加载的脚本（Jquery 需要）放在</body>前。但是就算这样，浏览器也会倾向于提早加载这些脚本。

- Better：给 script 加上 async/defer 属性。两者有些许不同：async 标签让 script 的下载和解析与页面构建并行，但是 script 的执行还是会阻塞页面加载。defer 在 async 的基础上让 script 的执行等待在 html 解析完后在执行，但是视频中展示 script 还是会在可见内容加载后半部分加载，比前面好，但是不是特别好。

- Extreme：当浏览器解析完 html 后，此时可见内容已经加载完了，会触发一个 load 事件，如果我们能够在这个 load 事件后告诉浏览器加载这些 scirpt，那么就完美了。
  示例代码:

```
// jquery
$(window).on('load',function() {
  $('body').append('<script src="script.js">')
})

// no jquery
window.addEventListener('load',function() {
  const script = document.createElement('script');
  script.src = 'script.js';
  document.body.appendChild(script);
})
```

---

—— 24253 记于 2019-3-19
