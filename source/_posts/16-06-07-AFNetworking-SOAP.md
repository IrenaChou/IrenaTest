title: iOS Web service SOAP消息(基于AFNetworking)
date: 2016-06-07 16:39:16
tags:
---
**Web service**是一个平台独立的，低耦合的，自包含的、基于可编程的web的应用程序，可使用开放的XML（标准通用标记语言下的一个子集）标准来描述、发布、发现、协调和配置这些应用程序，用于开发分布式的互操作的应用程序。
Web Service技术， 能使得运行在不同机器上的不同应用无须借助附加的、专门的第三方软件或硬件， 就可相互交换数据或集成。依据Web Service规范实施的应用之间， 无论它们所使用的语言、 平台或内部协议是什么， 都可以相互交换数据。Web Service是自描述、 自包含的可用网络模块， 可以执行具体的业务功能。Web Service也很容易部署， 因为它们基于一些常规的产业标准以及已有的一些技术，诸如标准通用标记语言下的子集XML、HTTP。Web Service减少了应用接口的花费。
Web Service为整个企业甚至多个组织之间的业务流程的集成提供了一个通用机制。


**下面分别是AFNetworking 2.6和3.0的关键代码，如想要Demo的，留言给我**

<!-- more -->
AFNetworking 3.0
---
```
#pragma mark - 发送请求
/**
 *  发送请求
 */
- (void)webServiceRequestWithsoapMessage:(NSString *)soapMessage {
  NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url11];
  [request addValue:@"text/xml; charset=utf-8"
      forHTTPHeaderField:@"Content-Type"];
  [request setHTTPMethod:@"POST"];
  [request setHTTPBody:[soapMessage dataUsingEncoding:NSUTF8StringEncoding]];
  NSURLSessionConfiguration *configuration =
      [NSURLSessionConfiguration defaultSessionConfiguration];
  AFURLSessionManager *manager =
      [[AFURLSessionManager alloc] initWithSessionConfiguration:configuration];
  manager.responseSerializer = [AFXMLParserResponseSerializer serializer];
  NSURLSessionDataTask *dataTask =
      [manager dataTaskWithRequest:request
                 completionHandler:^(NSURLResponse *response, id responseObject,
                                     NSError *error) {
                   if (error) {
                     NSLog(@"Error: %@", [error description]);
                   } else {
                     [responseObject setDelegate:self];
                     [responseObject parse];
                   }
                 }];
  [dataTask resume];
}
```

   
AFNetworking 2.6
---
```
#pragma mark - 发送请求
/**
 *  发送请求
 */
- (void)webServiceRequestWithsoapMessage:(NSString *)soapMessage {
  NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
  [request addValue:@"text/xml; charset=utf-8"
      forHTTPHeaderField:@"Content-Type"];
  [request setHTTPMethod:@"POST"];
  [request setHTTPBody:[soapMessage dataUsingEncoding:NSUTF8StringEncoding]];
  AFHTTPRequestOperation *operation =
      [[AFHTTPRequestOperation alloc] initWithRequest:request];
  operation.responseSerializer = [AFXMLParserResponseSerializer serializer];
  [operation setCompletionBlockWithSuccess:^(
                 AFHTTPRequestOperation *_Nonnull operation,
                 id _Nonnull responseObject) {
    NSLog(@"请求成功：%@", [responseObject description]);
    /**
     *  解析xml
     */
    [responseObject setDelegate:self];
    [responseObject parse];
  }
      failure:^(AFHTTPRequestOperation *_Nonnull operation,
                NSError *_Nonnull error) {
        NSLog(@"请求失败%@", error);
      }];
  [operation start];
}
```
*如果需要Demo，请在文章下面给我留言*

