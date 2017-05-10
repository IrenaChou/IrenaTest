---
title: IRCategoryCollection
date: 2017-05-10 13:16:45
tags:
---

[IRCategoryCollection](https://github.com/IrenaChou/IRCategoryCollection)

功能说明
---

整合category

此库只是整合Category，方便多个项目重复使用
有些category是由其它作者提供的，由于时间过长，有些原文链接已经找不到了，

原文链接：
**UIButton+IRImageTitleSpacing**： https://github.com/mokong/MKButtonStyle
*原文名字叫 UIButton+ImageTitleSpacing* 为了避免重复发生，添加了IR前缀

<!-- more -->
大致包括如下：

NSString
---
**字符串【NSString】**：
* 【 **IRVerify** 】验证
* 【 **IRDate** 】日期转换
* 【 **IRPinYin** 】转换成拼音
* 【 **IRTrans** 】与十六进制和Ascii转换

**IRVerify验证主要包括如下验证**：
* 身份证合法性
* 手机号的合法性
* 银行卡号的合法性
* 数字字符串是否为整数
* 数字字符串是否为浮点型
* 金额的合法性【保留两位小数】


UIButton
---
**UIButton**：
* 【 **IRImageTitleSpacing** 】设置button的titleLabel和imageView的布局样式，及间距

NSDictionary/NSArray
---
**NSDictionary/NSArray**：
* 【 **IRLOG** 】控制台打印中文

UIColor
---
**UIColor**：
* 【 **IRExtend** 】十六进制的颜色值转为objective-c的颜色

UIView
---
**UIView**：
* 【 **IRLayoutMethods** 】

**UIViewController**：
* 【 **IRNavigationBarBackgrounTransparent** 】状态栏是否显示背景色

UIImage
---
**UIImage**：
* 【 **IREx** 】[去除图片渲染效果](http://irenachou.github.io/2016/09/21/16-09-21-imageWithRenderingMode/)
* 【 **IRQRCode** 】通过二维码字符串生成可扫描的二维码图片，[具体详情](http://irenachou.github.io/2016/11/08/16-11-08-qrcodecreate/)




使用
---
通过 **Cocoapods** 导入

```
pod 'IRCategoryCollection'
```

剩下的只要import相应的头文件就Ok了，相应的category实现都可以看到
