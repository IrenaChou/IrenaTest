title: 验证手机号和银行卡号
date: 2016-03-11 14:09:44
tags:
---

```
//判断一个号码是否为手机号码
BOOL isValidateMobile(NSString *mobile);
```

```
//判断是否为一个合法的银行卡号
BOOL isValidateBankCard(NSString *bankNo);
```

<!-- more -->

```
/*手机号码验证*/
BOOL isValidateMobile(NSString *mobile) {
  //手机号以13, 15,18开头,八个 \d 数字字符
  NSString *phoneRegex = @"^((13[0-9])|(15[^4,\\D])|(18[0,0-9]))\\d{8}$";
  NSPredicate *phoneTest =
      [NSPredicate predicateWithFormat:@"SELF MATCHES %@", phoneRegex];
  return [phoneTest evaluateWithObject:mobile];
}
```

```
// 判断银行卡
BOOL isValidateBankCard(NSString *bankCard) {
  NSString *cardRegex =
      @"/^\\d{16,19}$|^\\d{6}\\d{10,13}$|^\\d{4}\\d{4}\\d{4}\\d{4,7}$/";
  NSPredicate *bankTest =
      [NSPredicate predicateWithFormat:@"SELF MATCHES %@", cardRegex];
  return [bankTest evaluateWithObject:bankCard];
}
```