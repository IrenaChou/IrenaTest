title: iOS 9+ 通讯录 Contacts Framework
date: 2016-07-27 11:05:03
tags:
---
iOS9的联系人相关框架 Contacts Framework
---
**iOS 9.0**介绍了Contacts和Contacts UI frameworks（ Contacts.framework和ContactsUI.framework ） ，这对于通讯簿提供现代化的面向对象的替换和Address Book UI frameworks.**这个框架是线程安全的** [要了解更多信息](https://developer.apple.com/reference/contacts).

<!-- more -->

**CNContactStore**:是线程安全的类，它可以读取并保存联系人，组和容器。它代表了用户的联系人数据库。它封装了所有的I / O操作和负责获取和联系人和群组的保存。由于联系人存储方法是同步的，所以建议您使用他们在后台线程。

**CNSaveRequest**：该类定义了一个保存请求操作联系人。该类存储每个操作的请求。可以批量多次更改到一个保存请求（注意，这些更改仅适用于对象）。在重叠的多个并发或保存请求变更的情况下，最后的改变获胜。如果您尝试添加一个对象（即，联系人或组，）已经存在于CNContactStore，CNErrorCodeInsertedRecordAlreadyExists出现错误和CNErrorUserInfoAffectedRecordsKey阵列更新为包含您试图添加的对象。如果您尝试更新或删除对象，它是不存在的联系人存储，保存请求不执行更新或删除，则CNErrorCodeRecordDoesNotExist发生错误，CNErrorUserInfoAffectedRecordsKey阵列更新为包含您尝试更新或删除对象。而保存请求正在执行，不能存取保存请求对象。

**CNContactPickerDelegate**
---
CNContactPickerDelegate提供了单次选择单个联系人和多个联系人的方法，实现了单次选择多个联系人的方法，选择单个联系人的方法就会失效

**需要注意的**：
---
```
      /**
     *  此处需要注意的是
     *- (void)deleteContact:(CNMutableContact *)contact;
     *方法需要的是CNMutableContact，如果传CNContact会报如下错误
     *-[CNContact setSnapshot:]: unrecognized selector sent to instance
     *0x1488be1a0
     * 解决错误的方法就是使用CNMutableContact
     [saveRequest deleteContact:self.contact]; //错误的
     解决方法如下
     */
     [saveRequest deleteContact:[self.contact mutableCopy]];
```
Demo提供
---
[Demo提供](http://7xrirn.com1.z0.glb.clouddn.com/codeBookAddressTestComplete.zip)  


下面提供一个添加联系人的代码，如需其它方法的使用，请看Demo

```
 //创建一个可变对象添加到联系人
  CNMutableContact *contact = [[CNMutableContact alloc] init];
  //将资料图片作为NSData对象
  //  contact.imageData = [NSData data];
  //设置名字
  contact.givenName = @"John";
  //设置姓氏
  contact.familyName = @"Appleseed";
  CNLabeledValue *homeEmail =
      [CNLabeledValue labeledValueWithLabel:CNLabelHome
                                      value:@"john@example.com"];
  CNLabeledValue *workEmail =
      [CNLabeledValue labeledValueWithLabel:CNLabelWork
                                      value:@"j.appleseed@icloud.com"];
  contact.emailAddresses = @[ homeEmail, workEmail ];
  //
  /**
   *  设置电话号码
   */
  contact.phoneNumbers = @[
    [CNLabeledValue
        labeledValueWithLabel:CNLabelPhoneNumberiPhone
                        value:[CNPhoneNumber phoneNumberWithStringValue:
                                                 @"(408) 555-0126"]]
  ];
  /**
   设置地址
   */
  CNMutablePostalAddress *homeAdress = [[CNMutablePostalAddress alloc] init];
  //街道
  homeAdress.street = @"1 Infinite Loop";
  //城市
  homeAdress.city = @"Cupertino";
  //国家代码
  homeAdress.state = @"CA";
  //邮编
  homeAdress.postalCode = @"95014";
  contact.postalAddresses =
      @[ [CNLabeledValue labeledValueWithLabel:CNLabelHome value:homeAdress] ];
  /**
   设置生日
   */
  NSDateComponents *birthday = [[NSDateComponents alloc] init];
  birthday.day = 1;
  birthday.month = 4;
  birthday.year = 1988;
  contact.birthday = birthday;
  //初始化方法
  CNSaveRequest *saveRequest = [[CNSaveRequest alloc] init];
  //保存新创建的contact
  [saveRequest addContact:contact toContainerWithIdentifier:nil];
  //更新用户的联系人数据库
  CNContactStore *store = [[CNContactStore alloc] init];
  [store executeSaveRequest:saveRequest error:nil];

```