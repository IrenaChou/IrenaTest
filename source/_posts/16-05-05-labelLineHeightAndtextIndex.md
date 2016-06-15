title: 自定义Label行高和首行缩进
date: 2016-05-05 14:29:39
tags:
---
首行缩进和控制行距放到了**UILabel+LineSpacing_textIndex Category**里


缩进和自定义行间距的效果如下图
* ![首行缩进](http://7xrirn.com1.z0.glb.clouddn.com/Label2.png)
* ![自定义行间距](http://7xrirn.com1.z0.glb.clouddn.com/Label1.png)

<!-- more -->
**下面的两段代码是方法调用，Category的具体代码，在文章的最后面，或是点击下载Category链接下载**
---
首行缩进使用，具体代码可以[下载Category](http://pan.baidu.com/s/1ge4APvP)
---
首行缩进是根据文字个数进行缩进，传的TypeNum为要缩进的文字数
```
#import "UILabel+LineSpacing_textIndex.h"
#import "ViewController.h"
@interface ViewController ()
@property(weak, nonatomic) IBOutlet UILabel *contentLabel;
@end
@implementation ViewController
- (void)viewDidLoad {
  [super viewDidLoad];
  self.contentLabel.text = @"简单点说话的方式简单点"
                           @"递进的情绪请省略"
                           @"你又不是个演员"
                           @"别设计那些情节"
                           @"没意见我只想看看你怎么圆"
                           @"你难过的太表面 像没天赋的演员"
                           @"观众一眼能看见"
                           @"该配合你演出的我演视而不见"
                           @"在逼一个最爱你的人即兴表演"
                           @"什么时候我们开始收起了底线"
                           @"顺应时代的改变看那些拙劣的表演"
                           @"可你曾经那么爱我干嘛演出细节";
  //首行缩进
  [self.contentLabel textIndexWithTypeNum:2];
}
@end
```
---
修改行间距的方法调用，具体代码可以[下载Category](http://pan.baidu.com/s/1ge4APvP)
---
```
#import "UILabel+LineSpacing_textIndex.h"
#import "ViewController.h"
@interface ViewController ()
@property(weak, nonatomic) IBOutlet UILabel *contentLabel;
@end
@implementation ViewController
- (void)viewDidLoad {
  [super viewDidLoad];
  self.contentLabel.text = @"简单点说话的方式简单点"
                           @"递进的情绪请省略"
                           @"你又不是个演员"
                           @"别设计那些情节"
                           @"没意见我只想看看你怎么圆"
                           @"你难过的太表面 像没天赋的演员"
                           @"观众一眼能看见"
                           @"该配合你演出的我演视而不见"
                           @"在逼一个最爱你的人即兴表演"
                           @"什么时候我们开始收起了底线"
                           @"顺应时代的改变看那些拙劣的表演"
                           @"可你曾经那么爱我干嘛演出细节";
  //修改行距
  [self.contentLabel lineSpaceingWithLineSpacingNum:12];
}
@end
```
下面是Category中的代码
---

首行缩进的方法调用
---
```
/**
 *  根据传入的字数确认首行缩进的字数
 *
 *  @param typeNum 首行缩进的字数
 */
- (void)textIndexWithTypeNum:(NSUInteger)typeNum {
  NSMutableAttributedString *attributedString =
      [[NSMutableAttributedString alloc] initWithString:self.text];
  NSMutableParagraphStyle *paragraphStyle =
      [[NSMutableParagraphStyle alloc] init];
  paragraphStyle.alignment = NSTextAlignmentLeft;
  CGFloat labelFont = [[self font] pointSize];
  CGSize whSize = [self.text sizeWithAttributes:@{
    NSFontAttributeName : [UIFont systemFontOfSize:labelFont]
  }];
  [paragraphStyle
      setFirstLineHeadIndent:whSize.height * typeNum -
                             typeNum *
                                 2.5];  //首行缩进 根据用户昵称宽度在加5个像素
  [attributedString addAttribute:NSParagraphStyleAttributeName
                           value:paragraphStyle
                           range:NSMakeRange(0, [self.text length])];
  self.attributedText = attributedString;
}
```
设置行间距
---
```
/**
 *  设置行间距
 *
 *  @param lineSpacingNum 行间距值
 */
- (void)lineSpaceingWithLineSpacingNum:(NSUInteger)lineSpacingNum {
  NSMutableAttributedString *attributedString =
      [[NSMutableAttributedString alloc] initWithString:self.text];
  NSMutableParagraphStyle *paragraphStyle =
      [[NSMutableParagraphStyle alloc] init];
  paragraphStyle.maximumLineHeight = lineSpacingNum;  //最大的行高
  [attributedString addAttribute:NSParagraphStyleAttributeName
                           value:paragraphStyle
                           range:NSMakeRange(0, [self.text length])];
  self.attributedText = attributedString;
  [self sizeToFit];
}
@end
```