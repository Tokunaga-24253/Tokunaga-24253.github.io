---
layout:     post
title:      Vue入门心得
subtitle:    "\"Here I come,Vue!\""
date:       2019-04-11
author:     24253
header-img: img/Vue.jpg
catalog: true
tags:
    - 前端学习
    - 2019
---

> “🙉🙉🙉 ”

## 前言

是时候学习一个前端框架了，我在粗略看了看知乎上关于哪个框架好的相关问题并结合杭州前端招聘要求后，选择了*Vue*。

不仅因为*Vue*学习曲线不高，比较适合我，还有这是为了找实习而学的，以后方向究竟是什么还不好说。

打算学习Vue后，决定使用*VScode*进行开发。于是Google：VScode Vue。看了很多教程，发现讲的都有点难懂，还好后来在**YouTube**上找到了一个很好的教程，于是我在这里进行一个梳理，希望能给后来者一点帮助。

------

## 正文

新学者下载使用vue有三个主要方式（主要介绍第三种）：

### 1. 使用CDN

用 `<script>` 标签引入，`Vue` 会被注册为一个全局变量。（CDN是什么，请学习[CDN](https://www.baidu.com/s?ie=UTF-8&wd=CDN%20%E6%9C%8D%E5%8A%A1)）

你可以这样使用：

```<script src="https://cdn.jsdelivr.net/npm/vue"></script>```

Vue 也可以在 **unpkg** 和 **cdnjs** 上获取 (cdnjs的版本更新可能略滞后)。

### 2. 使用npm下载vue

需要先下载NodejS，可以去[NodeJS官网](https://nodejs.org/zh-cn/)下载。

安装时应该是一路点击下一步就行，然后你的电脑应该就可以使用npm了。

```
# 最新稳定版
$ npm install vue
```

### 3. 使用Vue CLI

Vue CLI是一种快速，简单，有效的开启Vue项目的方式。（[什么是Cli](https://cn.vuejs.org/v2/guide/installation.html#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7-CLI)）

我们这边使用npm下载Vue CLI 3.0版本。

```npm install -g @vue/cli```

然后用`vue create HelloVue`创建项目，HelloVue是我取的项目名称，你可以替换成你想要的。

---

如果你还想学接下来的知识，可以去Vue官网[Vue官网](https://cn.vuejs.org/)学习，也可以在网上找更多的视频资料学习，这里我推荐一个视频[Learn Vue 2 in 65 Minutes](https://www.youtube.com/watch?v=78tNYZUS-ps)。

希望能给你们提供一点帮助~
