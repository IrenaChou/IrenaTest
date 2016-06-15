title: 弹框－发送邮件
date: 2016-03-11 14:50:28
tags:
---
调用
---
```
    /**
     *  需要弹框发邮件
     */
    if ([self isSendMail]) {
      [self sendEmailAction];
    }
```

<!-- more -->

```
- (BOOL)isSendMail {
  Class mailClass = (NSClassFromString(@"MFMailComposeViewController"));
  if (!mailClass) {
    NSLog(@"不支持应用内发送邮件功能");
    return NO;
  }
  //获取用户是否设置了邮件账户：
  if ([MFMailComposeViewController canSendMail]) {
    // 用户已设置邮件账户
    [self sendEmailAction]; // 调用发送邮件的代码
    return NO;
  }
  return YES;
}
- (void)sendEmailAction {
  // 邮件服务器
  MFMailComposeViewController *mailCompose =
      [[MFMailComposeViewController alloc] init];
  // 设置邮件代理
  [mailCompose setMailComposeDelegate:self];
  // 设置邮件主题
  [mailCompose setSubject:@"邮件标题"];
  // 设置收件人
  [mailCompose setToRecipients:@[ [_emailText text] ]];
  /**
   *  设置邮件的正文内容
   */
  NSString *emailContent = @"邮件内容";
  [mailCompose setMessageBody:emailContent isHTML:NO];
  /**
   *  添加附件
   */
  //  UIImage *image = [UIImage imageNamed:@"image"];
  NSData *imageData = UIImagePNGRepresentation(_image);
  [mailCompose addAttachmentData:imageData
                        mimeType:@""
                        fileName:@"custom."
                                 @"png"];
  // 弹出邮件发送视图
  [self presentViewController:mailCompose animated:YES completion:nil];
}
```

```
// MFMailComposeViewControllerDelegate的代理方法：
- (void)mailComposeController:(MFMailComposeViewController *)controller
          didFinishWithResult:(MFMailComposeResult)result
                        error:(NSError *)error {
  switch (result) {
  case MFMailComposeResultCancelled: // 用户取消编辑
    NSLog(@"Mail send canceled...");
    break;
  case MFMailComposeResultSaved: // 用户保存邮件
    NSLog(@"Mail saved...");
    break;
  case MFMailComposeResultSent: // 用户点击发送
    NSLog(@"Mail sent...");
    break;
  case MFMailComposeResultFailed: // 用户尝试保存或发送邮件失败
    NSLog(@"Mail send errored: %@...", [error localizedDescription]);
    break;
  }
  // 关闭邮件发送视图
  [self dismissViewControllerAnimated:YES completion:nil];
}
```