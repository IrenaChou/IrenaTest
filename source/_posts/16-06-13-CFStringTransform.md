title: iOS 汉字转换拼音 CFStringTransform
date: 2016-06-13 14:21:38
tags:
---
[参考原文](http://nshipster.cn/cfstringtransform/)

**CFStringTransform** 是 Core Foundation 中的一部分
```
CF_EXPORT
Boolean CFStringTransform(CFMutableStringRef string, CFRange *range, CFStringRef transform, Boolean reverse)
```
这个函数传入以下参数，并返回一个 Boolean 来表示转换是否成功：
**string**: 需要转换的字符串。由于这个参数是 CFMutableStringRef 类型，一个 NSMutableString 类型也可以通过自由桥接的方式传入。  
**range**: 转换操作作用的范围。这个参数是 CFRange，而不是 NSRange。  
**transform**: 需要应用的变换。这个参数使用了包含下面将提到的字符串常量的 ICU transform   string。  
**reverse**: 如有需要，是否返回反转过的变换。  

**CFStringTransform** 中的 transform 参数涉及的内容很多。这里有个它能做什么的概述：
<!-- more -->
去掉重音和变音符
---
Énġlišh långuãge lẳcks iñterêßţing diaçrïtičş. 如此类的字符串，把扩展的拉丁字符集正则化为 ASCII 友好型的表示，它非常有用。用 **kCFStringTransformStripCombiningMarks** 变换来去掉任意字符串中弯弯扭扭的符号。

为 Unicode 字符命名
---

**kCFStringTransformToUnicodeName** 让你可以找出特殊字符的 Unicode 标准名，包括 Emoji。例如："🐑💨✨" 被转换成 "{SHEEP} {DASH SYMBOL} {SPARKLES}"，而 "🐷" 变成了 "{PIG FACE}"。

不同拼写之间转写
---

除了英语这个重大例外（和它那令人愉快的拼写不一致），书写系统一般是将语言音调编码成一致的符号表示。欧洲语言一般使用拉丁字母（外加一些变音符），俄罗斯用西里尔字母，日本用平假名和片假名，泰国、韩国和阿拉伯国家也都有自己的字母。

虽然每种语言都有特殊的音调列表，也许有些其他语言会缺失，所有主要书写系统的交集已经足以让你高效的在不同字母之间转写（不要跟翻译搞混了）。

**CFStringTransform** 可以在拉丁语和阿拉伯语、西里尔语、希腊语、韩语（韩国）、希伯来语、日语（平假名和片假名）、普通话、泰语之间来回转写。

*并且这只是用了核心类库中常量定义！直接传入一个ICU transform表达式，CFStringTransform 还可以在拉丁语和阿拉伯语、亚美尼亚语、注音、西里尔字母、格鲁吉亚语、希腊语、汉语、韩语、希伯来语、平假名、印度语（梵文，古吉拉特语，旁遮普文，卡纳达语，马拉雅拉姆语，奥里雅语，泰米尔语，特卢固）、朝鲜语、片假名、叙利亚语、塔纳文、泰语之间转写。*
![不同拼写之间转写](http://7xrirn.com1.z0.glb.clouddn.com/pinyin-1.png)

平时可能会遇到的问题
---
字符串变换的一个更实际的应用是正则化不可预知的用户输入。即使你的应用并不单独处理其他语言，你也应当能智能地处理用户向你的应用输入的任何内容。

例如，你想在设备上建立一个可搜索的电影索引，它包含世界各地的人的问候：
  * 首先，应用 **kCFStringTransformToLatin** 变换将所有非英文文本转换为拉丁字母表示。
Hello! こんにちは! สวัสดี! مرحبا! 您好! → Hello! kon'nichiha! s̄wạs̄dī! mrḥbạ! nín hǎo!
  * 然后，应用 **kCFStringTransformStripCombiningMarks** 变换来去除变音符和重音。
Hello! kon'nichiha! s̄wạs̄dī! mrḥbạ! nín hǎo! → Hello! kon'nichiha! swasdi! mrhba! nin hao!
  * 最后，用 **CFStringLowercase** 转为小写，**并用CFStringTokenizer** 分词用作文本的索引。
(hello, kon'nichiha, swasdi, mrhba, nin, hao)

**通过对用户输入的文本使用同样的变换，你就可以实现一个通用的搜索，无论搜索文本或内容是什么语言！**


**下面我提供一个包含如下两个方法的Category**
**[Category下载地址](http://pan.baidu.com/s/1c27aX9I)**
```
/**
 *  汉字转成没有声调有空格的拼音
 *  (空格可根据需求调整return的withString后的字符串)
 *  @param wordStr 需要拼音的汉字(词组/句子)
 *
 *  @return 拼音
 */
+ (NSString *)transformToPinYin:(NSString *)wordStr {
  NSMutableString *mutableString = [NSMutableString stringWithString:wordStr];
  //带声调
  CFStringTransform((CFMutableStringRef)mutableString, NULL,
                    kCFStringTransformToLatin, NO);
  //  //不带声调
  CFStringTransform((CFMutableStringRef)mutableString, NULL,
                    kCFStringTransformStripDiacritics, NO);
  //你好 -> ni hao -> nihao
  return [mutableString stringByReplacingOccurrencesOfString:@" "
                                                  withString:@"    "];
}
/**
 *  汉字转成有声调有空格的拼音
 *  (空格可根据需求调整return的withString后的字符串)
 *  @param wordStr 需要拼音的汉字(词组/句子)
 *
 *  @return 带声调的拼音
 */
+ (NSString *)transformToPinYinHaveTone:(NSString *)wordStr {
  NSMutableString *mutableString = [NSMutableString stringWithString:wordStr];
  //带声调
  CFStringTransform((CFMutableStringRef)mutableString, NULL,
                    kCFStringTransformToLatin, NO);
  //你好 -> ni hao -> nihao
  return [mutableString stringByReplacingOccurrencesOfString:@" "
                                                  withString:@"    "];
}
```