---
title: CocoaPods制作与版本更新
date: 2017-04-21 16:04:35
tags:
---

**IRMakeCocoapodsLibaryTest** 这个是我制作的一个Demo，亲们可以先用 **Podfile** 先看一下，使用一下
```
pod 'IRMakeCocoapodsLibaryTest'
```
[这是IRMakeCocoapodsLibaryTest在github上的代码](https://github.com/IrenaChou/IRMakeCocoapodsLibaryTest)

言归正传，开始创建仓库
---
按照如下gif的步骤:
  1.  在github上进行项目的创建
  2.  将创建好的项目clone到本地
  3.  在clone下来的项目中创建一个OC项目
![创建仓库](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_1.gif)

<!-- more -->

创建项目到本地仓库
---
创建一个项目放到clone到本地的仓库内， 注意：**一定要为创建的项目添加Class prefix**，不加如果有相同的类名会报错，很麻烦 **【图中我只修改了一部分的类前缀，具体按项目文件修改】**
**创建的项目名跟远程项目名相同**
这一步相对简单，如果有问题可以看下图：
![创建项目](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_2.gif)


为项目添加 **.podspec** 文件并进行相关设置
---
```
pod spec create IRMakeCocoapodsLibaryTest<根据你的项目名更改>
```
按如下图片步骤操作：
  1.  打开终端，输入 **cd 目录** 进入到本地仓库
  2.  输入 **pod spec create IRMakeCocoapodsLibaryTest<此处要改成您自己的项目名>**
![为项目添加.podspec](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_3.png)

打开.podspec文件进行相关设置
下图是.podspec文件的设置及说明，根据自己的项目进行配制

![.podspec文件的设置](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_4.png)

这是我的本地仓库目录
![本地仓库目录](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_5.png)

文件按文件夹区分开管理
----
由于最近另一个公开库的文件较多，所以设置了子文件夹，下面是我另一个公开库的.podspec文件【 **大家如果不要看可以直接点击左侧目录跳过** 】

[下图中的.podspec文件下载](https://github.com/IrenaChou/podspec.Appraisals)

![本地仓库目录](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_51.png)


pod验证及代码提交
---
```
 pod lib lint
```
出现如下图的passed validation.就验证通过了， **如果报了问题，仔细看问题描述，根据描述修改**
![验证](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_6.png)

**上传到github远程仓库**
```
//添加
git add .

//提交 -m 后面为描述说明
git commit -m 'version 0.0.1'

//推到远程仓库
git push

//打上标签
git tag 0.0.1

//将标签上传到远程仓库
git push --tags
```


上传{project}.podspec到CocoaPods官方仓库中【搞完这个才是真正的完成】
----
按照git的规则,要想向别人的仓库中添加文件,fork一份,添加修改,然后push给作者,等待审核,然而这条路已经被堵死了..
CocoaPods为我们提供了另外一个更方便安全的方法 [trunk](http://blog.cocoapods.org/CocoaPods-Trunk/#transition)

1. 注册trunk
```
pod trunk register *youremail*@gmail.com '*yourname*' --description='iMac' --verbose
```
youremail@gmail.com 换成你自己的，此处我用的是与github相同的emial
yourname 换成你的名字

**以上命令是注册所需的,替换你的邮箱,用户名,以及描述内容, --verbose可以输入详细的debug**

*完成后需要到邮箱验证一下才能继续往下做*

注册完成后可以使用如下命令查看注册信息
```
pod trunk me
```

提交{project}.podspec
---
```
pod trunk push IRMakeCocoapodsLibaryTest.podspec
```
这条命令做了如下三件事:
  * 验证本地的podspec文件,也可以使用 pod lib lint验证
  * 上传podspec文件到trunk服务
  * 将{project}.podspec文件转为{poject}.podspec.json文件

使用
---
```
pod search IRMakeCocoapodsLibaryTest
```
**查询后按键盘上的Q键退出**
![使用](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_7.png)


search不到库或是search不到最新版本解决
---
*下面是我个人遇到的问题，和解决方法*
**当上面所有的步骤都走的很顺利，没有报错/报错顺利的解决完了，却发现search不到新库**

[参考自github上的回答](https://github.com/CocoaPods/CocoaPods/issues/4865)

在 **terminal** 下运行如下命令
```
//删除cocoapods的索引
rm ~/Library/Caches/CocoaPods/search_index.json

//然后重新search
pod search IRMakeCocoapodsLibaryTest
```

**版本更新成功，却seach不到新版本**

在 **terminal** 下运行如下命令
```
pod repo update --verbose
pod search IRMakeCocoapodsLibaryTest
```



更新版本
---
添加新功能或是修改bug的时候，必然要更新版本的，下面说说版本更新
大概步骤如下：
  1.  修改或添加项目文件喽
  2.  将.podspec文件中的s.version更新成自己对应的版本，如s.version=0.0.5
  3.  **pod lib lint**,验证一下
  4.  在将本地仓库提交到远程仓库
      ```
      git add .
      git commit -m 'version 0.0.5'
      git push
      git tag 0.0.5<更新的版本>
      git push --tags
      pod trunk push IRMakeCocoapodsLibaryTest.podspec
      ```
  5.  更新完在pod search IRMakeCocoapodsLibaryTest一下就看到版本号更新了，大功告成
  *下图我已经更新过几个版本了，所以版本号是0.0.5*
  ![查询结果](http://7xrirn.com1.z0.glb.clouddn.com/CocoaPods_8.png)


  使用
  ---
  创建一个项目使用一下自己创建好的pods吧


参考：http://www.jianshu.com/p/98407f0c175b
