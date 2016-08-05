title: 制作/使用.a文件
date: 2016-04-11 10:38:08
tags:
---


制作步骤：
---
1.  File--New--Project
    按照如下图创建项目
    ![操作](http://7xrirn.com1.z0.glb.clouddn.com/1.png)
2.  按照下图创完成所需类的定义和实现
    ![操作](http://7xrirn.com1.z0.glb.clouddn.com/2.png)    
3.  创建后Command + B 进行编辑，如果device选择的是真机，生成的.a文件就适合真机的
    想要创建适用于模拟器的.a文件，将device改成模拟器就可以      
4.  如果没有生成所需头文件，按下图逐步操作添加  
    ![操作](http://7xrirn.com1.z0.glb.clouddn.com/.a1.png)  
    ![操作](http://7xrirn.com1.z0.glb.clouddn.com/.a2.png)  	
5.  按下图查看制作好的.a文件
    ![2](http://7xrirn.com1.z0.glb.clouddn.com/3.png)



<!-- more -->

使用：
---
1.  将生成的.a文件和.h文件拖到要使用的项目中
    ![2](http://7xrirn.com1.z0.glb.clouddn.com/4.png)
2.  直接使用就可以
    ![2](http://7xrirn.com1.z0.glb.clouddn.com/5.png)


合并.a文件【将模拟器的.a文件和真机的.a文件整合在一起】
---
```
lipo -create IRCode/iOS/iphoneos/libIRTestSDK.a IRCode/iOS/iphonesimulator/libIRTestSDK.a  -output IRCode/iOS/libIRTestSDK.a
```

**其中IRCode/iOS/iphoneos/libIRTestSDK.a** //为真机库。  

**IRCode/iOS/iphonesimulator/libIRTestSDK.a** //为模拟器库 
**IRCode/iOS/libIRTestSDK.a** //为两个合并后存放的路径

然后可以输入命令测试下是否成功  

**lipo -info IRCode/iOS/libIRTestSDK.a**  //下面是输出 armv7 i386 有了两个就表情模拟器和真机都支持  其中armv7为真机架构 i386为模拟器
Architectures in the fat file: SQY/iOS/libGamePus.a are: armv7 i386
