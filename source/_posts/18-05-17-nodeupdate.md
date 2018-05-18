---
title: 升级nodejs版本
date: 2018-05-17 16:00:22
tags: 'JavaScript'
---

*原文链接是在windows下的，笔者未在windows下进行如下操作*
**本文是使用macOS High Sierra 10.13.4**

*运行* **n stable** *的时候会报一个错误，本文直接使用正确的命令进行描述*
[原文链接：windows下](https://jingyan.baidu.com/article/574c52197e42b96c8d9dc115.html)

<!-- more -->

查看当前nodejs的版本
---
```
─irena@irena-Pro ~ ‹ruby-2.4.1›
╰─$ node -v
v6.7.0
```

升级之前还需要安装n模块，n模块是专门用来管理nodejs的版本
---
```
╭─irena@irena-Pro ~ ‹ruby-2.4.1›
╰─$ npm install -g n                                                        1 ↵
/usr/local/bin/n -> /usr/local/lib/node_modules/n/bin/n
+ n@2.1.10
added 1 package in 1.687s
```

还可以直接输入n stable，升级到nodejs最新稳定的版本
---
描述打印中已经明确说明了 **installed : v10.0.0**
```
╭─irena@irena-Pro ~ ‹ruby-2.4.1›
╰─$ sudo n stable                                                           1 ↵
Password:
     install : node-v10.0.0
       mkdir : /usr/local/n/versions/node/10.0.0
       fetch : https://nodejs.org/dist/v10.0.0/node-v10.0.0-darwin-x64.tar.gz
######################################################################## 100.0%
   installed : v10.0.0
```
