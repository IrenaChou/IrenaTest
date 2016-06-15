title: 使用U盘装MAC OS X
date: 2016-02-29 16:05:24
tags:
---

我装的是OS X EI Capitan
有两种方法：
一，网络恢复
    必须在能用国外的网的基础上才可以（我是开的vpn），我选择的是第二种方法
二，将U盘设置成启动盘，直接安装
  安装的先决条件
  1. 准备一个不小到8G的盘  
  2. 将盘插入电脑的usb口中，打开`磁盘工具`  
  3. 将盘抹掉，如下图  
  4. ![1](http://7xrirn.com1.z0.glb.clouddn.com/irena1.png)
  

<!-- more -->
继续上面的步骤：
  * 从App Store下载完整的 OS X 安装器（就是重新下一下）  
    ![2](http://7xrirn.com1.z0.glb.clouddn.com/irena2.png)
  * 一定要将如下文件放到finder-application(应用程序中)  
  ![3](http://7xrirn.com1.z0.glb.clouddn.com/irena3.png)
  * 这个文件一般由双击.dmg包打开后就可以看见
  * 然后在终端执行如下代码，下面代码中的123为盘的名称    
  * ```终端:sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/123 --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app```
  * 将上面的代码粘贴到终端后*回车*，会让选择y或n，输入y
  * 需要等待一会我大概是30分钟左右吧
  * 完成后推出磁盘
  


使用u盘安装
  * 将u盘插到电脑上
  * 重启电脑，一直按option(alt)键
  * 选择你的安装盘
  * 继续...
  * 你可能会出现如下问题
  * 不能验证这个“安装 os x ei capitan”应用程序副本,它在下载过程中可能已遭破坏
  * 这个问题的解决方法就是，系统时间改成OS X EI Capitan安装包右面的时间，重启安装即可
  * 修改时间的终端命令：date 100114102015.30
      10是月，01是日，14是时，10是分，2015是年，30是秒
       注意:只要年月日一样就行  
   ![4](http://7xrirn.com1.z0.glb.clouddn.com/irena4.png)



遇到问题的解决：
1. 给苹果打电话求助     `*电话：400-666-8800*`
2. 使用搜索引擎 `（就是不管他问题说的多明显，一定要先百度，因为有可能和你想的并不相同）`