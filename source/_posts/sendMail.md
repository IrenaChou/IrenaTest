title: sendMail 发邮件 
date: 2016-02-16 14:17:03
tags:
---
 
使用SKPSMTPMessage无需弹框发送邮件
--

```
//使用SKPSMTPMessage无需弹框发送邮件
我使用的是
1.导入头文件
#import "NSData+Base64Additions.h"
#import "SKPSMTPMessage.h"
  SKPSMTPMessage *mail = [[SKPSMTPMessage alloc] init];
  [mail setSubject:@"标题"];                 // 设置邮件主题
  [mail setToEmail:@".com"];                 // 目标邮箱
  [mail setFromEmail:@".com"];               // 发送者邮箱
  [mail setRelayHost:@"smtp.qq.com"];        // 发送邮件代理服务器
  [mail setRequiresAuth:YES];
  [mail setLogin:@".com"];                   // 发送者邮箱账号
  [mail setPass:@""];                        // 发送者邮箱密码
  [mail setWantsSecure:YES];                 // 需要加密
  [mail setDelegate:self];
```
<!-- more -->

```
  //设置邮件正文内容：
  NSString *content =
      [NSString stringWithCString:"邮件内容" encoding:NSUTF8StringEncoding];
  NSDictionary *plainPart = @{
    kSKPSMTPPartContentTypeKey : @"text/plain",
    kSKPSMTPPartMessageKey : content,
    kSKPSMTPPartContentTransferEncodingKey : @"8bit"
  };
  // 添加附件
  NSString *vcfPath =
      [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
  NSData *vcfData = [NSData dataWithContentsOfFile:vcfPath];
// _image 截取的图片 
  vcfData = UIImagePNGRepresentation(_image);
  NSDictionary *vcfPart = [NSDictionary
      dictionaryWithObjectsAndKeys:
          @"text/directory;\r\n\tx-unix-mode=0644;\r\n\tname=\"test.png\"",
          kSKPSMTPPartContentTypeKey, @"attachment;\r\n\tfilename=\"test.png\"",
          kSKPSMTPPartContentDispositionKey, [vcfData encodeBase64ForData],
          kSKPSMTPPartMessageKey, @"base64",
          kSKPSMTPPartContentTransferEncodingKey, nil];
  //    执行发送邮件代码：
  [mail
      setParts:@[ plainPart, vcfPart ]]; // 邮件首部字段、邮件内容格式和传输编码
  [mail send];
#pragma SKPSMTPMessage 代理方法
- (void)messageSent:(SKPSMTPMessage *)message {
  NSLog(@"%@", message);
}
- (void)messageFailed:(SKPSMTPMessage *)message error:(NSError *)error {
  NSLog(@"message - %@\nerror - %@", message, error);
}
```
skpsmtpmessage邮件标题中文乱码问题
--
解决主题使用中文乱码问题

SKPSMTPMessage.m的sendParts里:
修改:

```
NSData *messageData = [message dataUsingEncoding:NSASCIIStringEncoding allowLossyConversion:YES];
为
NSData *messageData = [message dataUsingEncoding:NSUTF8StringEncoding allowLossyConversion:YES];
```


