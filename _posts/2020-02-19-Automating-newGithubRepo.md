---
layout: post
title: 自动化新建github仓库
subtitle: '"Make life easier, why not?"'
date: 2020-02-19
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 2020
  - Python
  - Windows
---

> “🙉🙉🙉 ”

## 前言

今天在 Youtube 上面看到了[Automating My Projects With Python](https://www.youtube.com/watch?v=7Y8Ppin12r4&t=674s)这个视频。

![视频封面](https://raw.githubusercontent.com/Tokunaga-X/githubPictures/master/Others/Thumbs.png)

视频的主要内容是教你如何使用命令行指令和 python 来自动化新建 git 仓库并上传到 github 上面去。

要知道平常我们要新建一个项目要分好几步进行：

1. 在本地新建文件夹
2. 用 git init 来引入 git
3. 新建 README 文件后进行 git add 和 git commit 动作
4. 到 github 网页上去新建仓库
5. 使用 git remote add origin 【你的 git 仓库 url】和 git push -u origin master 来连接两个仓库并且进行第一次上传

挺麻烦的是吧，当然你还可以使用 github desktop 这个应用程序来使这个过程稍微简单一点，只是稍微。

所以如果能像他一样，在命令行中输入 create xxx(项目名称)就可以自动创建好本地 git 文件夹与 github 端仓库并连接，那该有多爽！

## 正文

有兴趣的同学自己去看一下视频最好，以防没耐心或者没法翻墙的同学着急，我在这里简单概括一下视频里的方法:  
① 使用.bat 文件来进行本地项目文件夹的新建以及 git init、创建 README.md

② 使用 python 来模拟网页动作，比如打开浏览器，跳转至 github，输入用户名和密码，点击登录，跳转到仓库不停的点击按钮直至创建完仓库

③ 最后继续使用命令行来进行两端的连接(git remote、git push -u)

本来我都想开始 ctrl-c + ctrl-v 了，但是瞄了一眼评论区，发现有个网友提出了一点改进意见。

![评论](https://raw.githubusercontent.com/Tokunaga-X/githubPictures/master/Others/Comment.png)

翻译：您可以使用 Github API，而无需使用 selenium 这个工具，会更简单。

作者也进行了回复

![回复](https://raw.githubusercontent.com/Tokunaga-X/githubPictures/master/Others/Reply.png)

翻译：是的，您是对的，我只是从未进行过网络抓取，所以我想练习一下 但是可以肯定的是，API 是一个更平滑的选择 ：)

这么一看，再去翻看了一下 GitHub Api 的文档，感觉这个改进很有必要。于是决定自己实现一下。

---

## 后记

两个文件的完整代码在[这里](https://github.com/Tokunaga-X/ProgrammingProjectList/tree/master/auto_repo)可以看见

—— 24253 记于 2020-2-19
