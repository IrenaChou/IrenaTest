title: iOS 使用 ASI 调webService
date: 2016-05-25 16:34:41
tags:
---
**Web service**是一个平台独立的，低耦合的，自包含的、基于可编程的web的应用程序，可使用开放的XML（标准通用标记语言下的一个子集）标准来描述、发布、发现、协调和配置这些应用程序，用于开发分布式的互操作的应用程序。  
Web Service技术， 能使得运行在不同机器上的不同应用无须借助附加的、专门的第三方软件或硬件， 就可相互交换数据或集成。依据Web Service规范实施的应用之间， 无论它们所使用的语言、 平台或内部协议是什么， 都可以相互交换数据。Web Service是自描述、 自包含的可用网络模块， 可以执行具体的业务功能。Web Service也很容易部署， 因为它们基于一些常规的产业标准以及已有的一些技术，诸如标准通用标记语言下的子集XML、HTTP。Web Service减少了应用接口的花费。  
Web Service为整个企业甚至多个组织之间的业务流程的集成提供了一个通用机制。 




步骤:
1.  添加SystemConfiguration.framework和libz.tbd
2.  将asi中类添加不使用arc标志
3.  下面上代码


[Demo下载](http://7xrirn.com1.z0.glb.clouddn.com/codeASIWebServiceDemo.zip)
---
<!-- more -->
我们使用的是xml传输数据，其中XML创建和解析我使用的是GDataXML，下面先说说xml的生成和解析

通过实体类生成xml字符串，实体类的具体属性就不一一贴出了*具体通过需求而定*
---
```
#pragma mark - xml文件创建
/**
 *  xml文件创建
 *
 *  @return 创建好的XML字符串
 */
- (NSString *)requestXmlStringCreateWithArgs:(NSArray *)args {
  /**
   *  创建一个标签元素   一级标签
   *  如果value不设置值，生成的标签为<soapenv:Header/>
   */
  GDataXMLElement *element =
      [GDataXMLNode elementWithName:@"soapenv:Header" stringValue:@""];
  GDataXMLElement *element12 =
      [GDataXMLNode elementWithName:@"soapenv:Body" stringValue:@""];
  // 创建一个标签元素   二级标签
  GDataXMLElement *element21 =
      [GDataXMLNode elementWithName:@"" stringValue:@""];
  /**
   获取当前类的属性列表
   */
  PayModel *payModel = [[PayModel alloc] init];
  NSArray *propertyList = [payModel propertyNameList];
  [args enumerateObjectsUsingBlock:^(PayModel *obj, NSUInteger idx,
                                     BOOL *_Nonnull stop) {
    GDataXMLElement *arg =
        [GDataXMLNode elementWithName:[NSString stringWithFormat:@"zz%zd", idx]
                          stringValue:@""];
    for (int i = 0; i < [propertyList count]; i++) {
      // 创建一个标签元素   四级标签  存储内容
      if ([obj valueForKey:propertyList[i]] != nil) {
        GDataXMLElement *element41 =
            [GDataXMLNode elementWithName:propertyList[i]
                              stringValue:[obj valueForKey:propertyList[i]]];
        [arg addChild:element41];
      }
    }
    [element21 addChild:arg];
  }];
  // 创建一个属性  根标签属性
  GDataXMLElement *rootElementAttribute1 = [GDataXMLNode
      attributeWithName:@"xmlns:"
            stringValue:@"根据情况而定"];
  GDataXMLElement *rootElementAttribute2 =
      [GDataXMLNode attributeWithName:@""
                          stringValue:@"根据情况而定"];
  // 创建一个根标签
  GDataXMLElement *rootElement =
      [GDataXMLNode elementWithName:@":"];
  //将二级标签添加到一级标签上
  [element12 addChild:element21];
  // 把标签与属性添加到根标签中
  [rootElement addChild:element];
  [rootElement addChild:element12];
  [rootElement addAttribute:rootElementAttribute1];
  [rootElement addAttribute:rootElementAttribute2];
  // 生成xml文件内容
  GDataXMLDocument *xmlDoc =
      [[GDataXMLDocument alloc] initWithRootElement:rootElement];
  NSData *data = [xmlDoc XMLData];
  NSString *xmlString =
      [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
  return xmlString;
}
```
解析xml
---
```
#pragma mark - 解析xml
/**
 *  解析xml
 */
- (void)pareXMLWithXMLString:(NSString *)xmlString {
  GDataXMLDocument *xmlDoc =
      [[GDataXMLDocument alloc] initWithXMLString:xmlString
                                         encoding:NSUTF8StringEncoding
                                            error:nil];
  GDataXMLElement *rootElement = [xmlDoc rootElement];
  for (GDataXMLElement *ele in rootElement.children) {
    if (ele.childCount > 0) {
      for (GDataXMLElement *ele1 in ele.children) {
        for (GDataXMLElement *ele2 in ele1.children) {
          for (GDataXMLElement *ele3 in ele2.children) {
            NSLog(@"标签名：%@\n", ele3.name);
            NSLog(@"内容：%@\n", ele3.stringValue);
          }
        }
      }
    }
  }
}
```

发送请求
---
```
#pragma mark - 发送请求
- (void)webServiceRequestWithsoapMessage:(NSString *)soapMessage {
  NSURL *url = [NSURL URLWithString:urlString];
  //请求发送到的路径
  ASIHTTPRequest *theRequest = [ASIHTTPRequest requestWithURL:url];
  [theRequest addRequestHeader:@"Content-Type"
                         value:@"text/xml; charset=utf-8"];
 [theRequest setRequestMethod:@"POST"];
  [theRequest
      appendPostData:[soapMessage dataUsingEncoding:NSUTF8StringEncoding]];
  [theRequest setDefaultResponseEncoding:NSUTF8StringEncoding];
  [theRequest startSynchronous];
  NSError *error = [theRequest error];
  if (!error) {
    NSMutableData *mData = [NSMutableData
        dataWithData:[theRequest responseData]];  // WebService接口返回的数据
    NSString *theXML = [[NSString alloc]
        initWithBytes:[mData mutableBytes]
               length:[mData length]
             encoding:
                 NSUTF8StringEncoding];  //将返回数据转换为字符串，进行解析（本文中返回的数据为XML数据）
    NSLog(@"%@", theXML);
    /**
     *  解析xml
     */
    [self pareXMLWithXMLString:theXML];
  } else {
    NSLog(@"请求错误：\n%@", error);
  }
}
```