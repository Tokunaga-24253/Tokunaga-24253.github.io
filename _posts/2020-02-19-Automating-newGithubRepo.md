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

首先我们要考虑的是: 如何在命令行下使用一行指令来顺序进行一系列的动作呢？我们可以想想，当你下载完 python、java 语言环境后，教学里是不是有一个让你在命令行中输入 python/java 来测试是否安装成功吗? 那就是我们所需要的，在命令行中定义一个全局的“函数”，我们输入这个函数名，就能执行这个“函数”。这个“函数”在这里就是.bat 批处理文件。（windows 环境下，mac 中应该另有方法）

你在 bat 文件里写的语句就是你一般在命令行中输入的语句，比如 cd 啊，mkdir 之类的，这是我们实现的基础。第二就是如何在 bat 中接受参数，因为我们想以 create xxx 的形式来创建这个仓库，xxx 就是我们要的名称。就像函数一样，bat 中也可以接收用户输入的参数，以%1%来表示第一个参数，以此类推。

既然我们语法都知道了，那就开始写吧。

```
@cd D:\yuandaima\GitHub
@echo Creating project folder........
@mkdir %1%
@cd %1%
@git init
@echo ## This project needs a proper Readme file, right?>README.md
@git add README.md
@git commit -m 'project_init'
@echo Creating project on github........
@python D:\yuandaima\Python\newResportory\create.py %1%
@echo Connecting.......
@git remote add origin git@github.com:Tokunaga-X/%1%.git
@git push -u origin master
@code .
```

以上就是我们 bat 文件中的全部语句。首先你肯定会注意到所有语句前都有一个“@”,这个符号是用来避免在命令行中显示此语句的，因为我们不想要“用户”看到乱七八糟的信息，我们用 echo 来输出我们想要输出的提示信息。语句从上到下实现了创建本地文件夹、初始化 git、创建远程仓库、连接两端、进行第一次推送、打开 vs-code 的功能。

还有比较重要的一部分就是如何使用 github api 来让 github 创建你所要的仓库。

这就是 python 起作用的时候了，我们创建一个 py 文件，在其中写一个简单的 api 请求。

```
import requests
import sys
data = {
    "name": sys.argv[1]
}
r = requests.post('https://api.github.com/user/repos',
                  auth=('Tokunaga-X', '951753qweasd2846'),
                  json=data)
if r.status_code == 200 | r.status_code == 201:
    print('Successfuly creating new repository on github!')
else:
    print('Failed  to create new repository on github, maybe your have the same name.')
    print(r.text)
```

十行左右的代码，很简单，就不多做解释了。

最后我们要如何让 windows 知道这个 create 指令呢？还要让其在所有路径下都能使用，就像一个全局函数。很简单，把这个 bat 文件所在的路径加入到环境变量中的 path 中，就 OK 了。

![回复](https://raw.githubusercontent.com/Tokunaga-X/githubPictures/master/Others/Result.png)

---

## 后记

两个文件的完整代码在[这里](https://github.com/Tokunaga-X/ProgrammingProjectList/tree/master/auto_repo)可以看见

—— 24253 记于 2020-2-19
