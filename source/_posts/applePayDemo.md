title: applePayDemo
date: 2016-03-04 14:03:40
tags:
---


[参考原文](https://developer.apple.com/library/ios/ApplePay_Guide/)

定义
---
```
#import "ViewController.h"
#import <PassKit/PassKit.h>
@interface ViewController ()<PKPaymentAuthorizationViewControllerDelegate>
@end
```

实现
---
```
@implementation ViewController
- (void)viewDidLoad {
  [super viewDidLoad];
}
- (void)applePayTest {
  //设备可用
  // PKPaymentAuthorizationViewController用来显示ApplePay的Controller
  if (![PKPaymentAuthorizationViewController canMakePayments]) {
    //设备不支持
    //不让ApplePay的支付按钮去显示
    return;
  }
  //想当自己的应用支持的卡类型
  /*
   [PKPaymentAuthorizationViewController
   canMakePaymentsUsingNetworks:@[PKPaymentNetworkVisa]]
   */
  //判断支持的卡类型
  if (![PKPaymentAuthorizationViewController canMakePaymentsUsingNetworks:@[
        PKPaymentNetworkVisa,
        PKPaymentNetworkChinaUnionPay
      ]]) {
    NSLog(@"不支持visa和银联");
    //进入设置银行卡的页面
    [[[PKPassLibrary alloc] init] openPaymentSetup];
    return;
  }
  //创建支付请求
  PKPaymentRequest *request = [[PKPaymentRequest alloc] init];
  //显示支付页面
  PKPaymentAuthorizationViewController *vc =
      [[PKPaymentAuthorizationViewController alloc]
          initWithPaymentRequest:request];
  vc.delegate = self;
  //*设置商户的ID(网站配制的id)
  request.merchantIdentifier = @"merchant.com.irena.AppleiPayDemo";
  //*设置国家代码
  request.countryCode = @"CN";
  //*设置支付的卡类型
  request.supportedNetworks = @[ PKPaymentNetworkVisa ];
  //*设置商户的支付标准(必须支持3DS)
  request.merchantCapabilities = PKMerchantCapability3DS;
  //*设置货币单位(中文CNY)
  request.currencyCode = @"CNY";
  ```
<!-- more -->

  ```
  //*设置商品
  // label商品名称
  // amount价格
  NSDecimalNumber *num1 = [NSDecimalNumber decimalNumberWithString:@"4"];
  // 当只有一个1个商品时,显示的是付给当前商品
  PKPaymentSummaryItem *item1 =
      [PKPaymentSummaryItem summaryItemWithLabel:@"水杯" amount:num1];
  PKPaymentSummaryItem *item2 =
      [PKPaymentSummaryItem summaryItemWithLabel:@"红牛" amount:num1];
  //当多个时商品,最后一个商品被当成一个总价去显示
  NSDecimalNumber *sum = [NSDecimalNumber decimalNumberWithString:@"8"];
  PKPaymentSummaryItem *itemSum =
      [PKPaymentSummaryItem summaryItemWithLabel:@"zdjr" amount:sum];
  request.paymentSummaryItems = @[ item1, item2, itemSum ];
  //设置收据必填内容,第一次使用必填
  request.requiredBillingAddressFields =
      PKAddressFieldAll; // billingContact 默认地址
  //设置送货必填的内容
  request.requiredShippingAddressFields = PKAddressFieldAll;
  //设置送货方式
  // summaryItemWithLabel 送货方式
  NSDecimalNumber *methodNum = [NSDecimalNumber decimalNumberWithString:@"4"];
  PKShippingMethod *method1 =
      [PKShippingMethod summaryItemWithLabel:@"顺风" amount:methodNum];
  //*区分同一个送货方式,必须填
  method1.identifier = @"shunfeng";
  //送货方式的详情描述
  method1.detail = @"24小时之内送到";
  request.shippingMethods = @[ method1 ];
  // modal出来,显示支付页面
  [self presentViewController:vc animated:YES completion:nil];
}
```
PKPaymentAuthorizationViewControllerDelegate
---
```
/*
在点击"使用密码支付"的按钮时候调用,开始进行支付调用
 payment:加密后的数据
 */
- (void)
paymentAuthorizationViewController:
    (PKPaymentAuthorizationViewController *)controller
               didAuthorizePayment:(PKPayment *)payment
                        completion:
                            (void (^)(PKPaymentAuthorizationStatus status))
                                completion {
  //把支付信息发送给服务器进行处理
  //第三方或发送给自己的服务器
  //银连https://merchant.unionpay.com/join/product/detail?id=80
  //    NSError *error;
  //    ABMultiValueRef addressMultiValue =
  //    ABRecordCopyValue(payment.billingAddress,kABPersonAddressProperty);
  //    NSDictionary *addressDictionary = (__bridge_transfer NSDictionary *)
  //    ABMultiValueCopyValueAtIndex(addressMultiValue, 0);
  //    NSData *json = [NSJSONSerialization dataWithJSONObject:addressDictionary
  //    options:NSJSONWritingPrettyPrinted error: &error];
  //根据服务器返回的支付状态进行不同的显示,给用户进行不同的显示
  //(调用BLOCK传不同的枚举)
  completion(PKPaymentAuthorizationStatusSuccess);
}
/*
 支付完成
 支付成功或失败后调用的方法
 */
- (void)paymentAuthorizationViewControllerDidFinish:
    (PKPaymentAuthorizationViewController *)controller {
  //把支付的界面关闭
  [self dismissViewControllerAnimated:YES completion:nil];
}
@end
```

*暂时只提Demo，后序在完善*