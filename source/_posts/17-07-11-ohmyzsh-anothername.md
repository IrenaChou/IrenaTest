---
title: 别名永久生效与ohmyzsh下别名配制
date: 2017-07-17 10:15:25
tags: 'Linux'
---

*当前系统：macOS Sierra*

简介
---
**别名** 是另一个名字
*就像有一个人叫张三，有一天你给张三起了个别名叫张小三，以后你叫这个张三和张小三的就全是这个人，但是他的身份证上的名字还是张三，并不会变*

```
alias rn='react-native'
```
也即，输入rn后，被自动定向到react-native这个命令了。 **别名** 的作用就是，给命令起一个别名，方便记住，但并不会改变原命令，你可以使用原命令 **react-native** 也可以使用你起的别名 **rn**。

<!-- more -->

为命令定义别名
---
*例：为react-native创建一个别名*
```
// 语法：
// alias 你起的别名='原命令名字'

alias rn='react-native'
```

查看别名
---
可以查看具体某一个命令的 **别名** ，使用
*例：下面是查看别名rn*
```
// 语法：
// alias 你起的别名

alias rn
```

查看全部别名
删除 **别名**【此处的删除只是删除临时 **别名** ，永久删除与创建相反即可】
---
*例：删除下面为rn的别名*
```
// 语法：
// unalias 你起的别名

unalias rn
```

别名永久生效
----
没有做过永久化的 **别名** 只有在创建 **别名** 的当前终端窗口有效，一但关闭此窗口或是新开一个窗口，均不生效，所以要长久使用，先要把他存起来

下面是做一些配置文件的修改方式例出如下几种：
1.  **激活Finder** ，按键盘的 **command+shift+G** 输入文件目录
2.  **激活Finder** ，点击左上角的菜单，前往--前往文件夹，输入文件目录
3.  使用终端的vim

下面使用vim的方式进行修改：
1.  打开新终端窗口，输入 **vim ~/.bashrc** 命令，后回车
2.  输入键盘上的 **i** ，将你要保存的 **别名** 输入到文件上
    ```
    alias rn='react-native'
    ```
3.  【保存退出】输入键盘上的 **:wq** 后回车
4.  在终端输入 **source ~/.bashrc** 回车

如果没有生效：
1.  打开新终端窗口，输入如下命令，后回车
    ```
    vim ~/.bash_profile
    ```
2.  按上面的方法在里面添加一行 **source ~/.bashrc** 后保存退出


oh-my-zsh 永久保存 别名 指定指令别名
---

**修改方式与修改别名永久保存相同，只是文件不同**：
1.  vim ~/.zshrc
2.  输入你要保存的别名命令，如
    ```
     alias rn='react-native'
    ```
3.  source ~/.zshrc


[参考自：](http://blog.csdn.net/jianglei421/article/details/8510723)
