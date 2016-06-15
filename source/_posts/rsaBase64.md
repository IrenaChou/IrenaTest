title: iOS Rsa
date: 2016-03-14 14:01:29
tags:
---
[生成秘匙参考原文](http://witcheryne.iteye.com/blog/2171850)
---
[ OC Demo 下载 ](http://pan.baidu.com/s/1gews7mV)
---

加密图解
---
 ![效果显示](http://7xrirn.com1.z0.glb.clouddn.com/rsa.png)

**本文主要讲解iOS方面的RSA加解密，demo也是针对iOS的加解密，具体demo可由文章最上面点OC Demo下载链接下载**

加解密的具体代码较分散，就不一一在文件中展示，如需要可在文章开头下载

**其中公钥和私钥文件由下面的这段代码块生成，如果你只包含加密，无需解密，可不使用下面代码块，加密文件服务器由服务器端提供**
```
#!/usr/bin/env bash
echo "Generating RSA key pair ..."
echo "2048 RSA key: private_key.pem"
openssl genrsa -out private_key.pem 2048
```

```
echo "create certification require file: rsaCertReq.csr"
openssl req -new -key private_key.pem -out rsaCertReq.csr
```
<!-- more -->
```
echo "create certification using x509: rsaCert.crt"
openssl x509 -req -days 3650 -in rsaCertReq.csr -signkey private_key.pem -out rsaCert.crt
```

```
echo "create public_key.der For IOS"
openssl x509 -outform der -in rsaCert.crt -out public_key.der
```

```
echo "create private_key.p12 For IOS. Please remember your password. The password will be used in iOS."
openssl pkcs12 -export -out private_key.p12 -inkey private_key.pem -in rsaCert.crt
```

```
echo "create rsa_public_key.pem For Java"
openssl rsa -in private_key.pem -out rsa_public_key.pem -pubout
echo "create pkcs8_private_key.pem For Java"
openssl pkcs8 -topk8 -in private_key.pem -out pkcs8_private_key.pem -nocrypt
echo "finished."
```
**Tips:**
在创建证书的时候, terminal会提示输入证书信息. 根据输入对应信息就OK. 
在创建p12密匙时, 会提示输入密码, 此时的密码必须记住, 之后解密会用到.
如果上面指令有问题,请参考最新的openssl官方文档, 以官方的为准. 

