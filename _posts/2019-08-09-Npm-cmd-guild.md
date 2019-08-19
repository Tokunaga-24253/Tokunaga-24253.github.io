---
layout: post
title: HelloBlog
subtitle: '"学习并记录npm指令"'
date: 2019-03-19
author: 24253
header-img: img/Learning.jpg
catalog: true
tags:
  - 2019
  - 大学学习
---

> “🙉🙉🙉 ”

## 前言

介绍并记录基础的 npm 命令。

什么是[NPM](https://www.npmjs.cn/)？  
*npm*是**node**的包管理工具，基本上如果你写**JavaScript**的话，你就要和它打交道。  
同样的，如果你要用 npm，你要先下载 NODE，npm 包含在 node 安装包中。

## 正文

## npm -v

功能：查询当前电脑 npm 的版本。

---

## npm init

功能：生成一个 package.json 文件，这个文件是用来定义项目中包(package)的信息的，执行该命令后终端会依次询问 name, version, description 等字段。

PS：如果想跳过询问阶段，追加--yes 或者-y 参数，其作用与一路敲回车相同。

---

## npm install ** / npm uninstall **

缩写：npm i ** / npm un **

功能：安装/删除包。  
不加参数的话，默认下载在当前项目中。  
加--global/-g 参数，会进行全局安装，包安装在你的 npm 目录下。

可以一次安装多个包

```
$ npm i express momemt lodash mongoose body-parser webpack
```

可以安装我们所想要版本的包，使用@加上版本号即可。

```
$ npm install underscore@1.8.2
```

---

。。。。。。

---

## 后记

—— 24253 记于 2019-8-9
