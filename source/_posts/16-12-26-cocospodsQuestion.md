title: 使用cocospods遇到的问题
date: 2016-12-26 14:47:17
tags:
---



1. `[!] Unable to add a source with url https://github.com/CocoaPods/Specs.git named master-1.``You can try adding it manually in ~/.cocoapods/repos or via pod repo add.`
   - ![问题1](http://7xrirn.com1.z0.glb.clouddn.com/blogImagecocoapods-Q1.png)
   - 问题解决：**您电脑上的Xcode大于一个，需自己手动选择一个使用版本**，具体做法如下
   - ![问题1](http://7xrirn.com1.z0.glb.clouddn.com/blogImagecocoapods-A1.png)
   - sudo xcode-select -switch **/Applications/Xcode7.3.app**【拖拽你要使用的xcode替换/Applications/Xcode7.3.app】


1. `ERROR:Could not find a valid gem 'cocoapods' (>= 0), here is why:`

   `Unable to download data from https://ruby.taobao.org/ - SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (https://ruby.taobao.org/specs.4.8.gz)`

   - 问题解决：**由于淘宝源已停止维护，我们需要更换新源**，具体做法如下
     - 查看源：`gem sources -l`
     - 删除源：`gem sources --remove https://ruby.taobao.org/`
     - 添加源：`gem sources -a https://gems.ruby-china.org/`

2. `Generating Pods project Abort trap: 6`

   - ![问题1](http://7xrirn.com1.z0.glb.clouddn.com/blogImagecocoapods-Q2.png)
   - 问题解决：**安装最新发布版本**，具体做法如下
   - `sudo gem install cocoapods --pre`

   ​