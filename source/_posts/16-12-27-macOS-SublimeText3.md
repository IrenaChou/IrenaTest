title: macOS配制SublimeText3运行JavaScript
date: 2016-12-27 13:44:03
tags: 'JavaScript'
---



**本文使用macOS Sierra 版本 10.12.1**

## 运行javaScript

```
1、下载安装Sublime Text 3
```

------

https://download.sublimetext.com/Sublime%20Text%20Build%203126.dmg
安装好   键盘**command + q** 退出Sublime Text 3

<!-- more -->

```
2、下载安装nodejs
```
------

**如果已经存在**
可以在终端运行如下命令查看node的位置
```
where node
```

https://nodejs.org/dist/v6.9.2/node-v6.9.2.pkg

安装nodejs时需要注意如下图中红框标的路径【**先将其复制保存，如果地址跟我文中的地址相同，可以不用复制，下面直接拷贝我写好的就行**】，下面会用到
![安装nodejs时需要注意](http://7xrirn.com1.z0.glb.clouddn.com/blogImagenodejs.png)

1. 打开安装好的Sublime Text 3

2. 按如下图片操作

   ![步骤1](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-1.png)

3. 将如下代码复制粘贴

   ```
   "cmd": ["/usr/local/bin/node","$file"],
   "selector":"*.js"
   ```

   ![步骤2](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-2.png)
   ​

4. 保存起来【**名字后面要用到的，起的规范点哦**】
   ![步骤3](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-3.png)

5. 点击键盘的**command + q**，先将Sublime Text 3退出，打开后按如下图操作
   ![步骤4](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-4.png)

6. **输入如下测试代码，保存成.js文件**

   ```javascript
   console.log('Irena Test')
   ```

   输入键盘的**command + b**  build一下

   ![步骤5](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-5.png)











## 安装Package Control

https://packagecontrol.io/installation

**ctrl + ~ ：调出控制台**

将如下代码复制到控制台

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

![步骤6](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-6.png)

当出现如下图红框中的这两个就可以了

![步骤7](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-7.png)

选择下图红框所指向的位置

![步骤8](http://7xrirn.com1.z0.glb.clouddn.com/blogImagesublime-8.png)

相关插件请参考如下链接

https://packagecontrol.io/browse
