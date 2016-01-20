title: 给APK文件签名
date: 2014-12-20 21:29:24
category: Android
tags: Android签名
description: 为我们的App签名
---
## 给APK文件签名

下面使用的工具都在 \Java\jdk1.7.0_17\bin 下，如果你已经配置了java环境变量,就可以直接在命令行下使用了，如果没有的话，你需要在命令行下将工作目录切换到 Java\jdk1.7.0_17\bin 执行
###生成证书
如果有证书可以略过这一步，直接进入下一步

`keytool -genkey -v -alias CERT -keyalg RSA -keysize 2048 -validity 10000 -keystore CERT.keystore`

参数说明：
    CERT.keystore ---- 证书保存的文件名
    CERT ---- 证书的别名
    10000 ---- 10000天的有效期
    2048 ---- 默认为1024 bits，Android 建议使用2048 bits或更高

证书生成后使用如下命令可以查看证书的信息：

`keytool -list -alias CERT -keystore CERT.keystore`

### 给APK文件签名

`jarsigner -verbose -keystore CERT.keystore to_sign.apk CERT`

参数说明：
    CERT.keystore ---- 证书保存的文件名 
    CERT ---- 证书的别名 
    to_sign.apk ------待签名的apk文件

签名过程需要输入证书的密码,按要求输入即可

待签名的apk文件根根目录下如果有文件夹“META-INFO”，请先删除（重新签名就需要这样做）。
如果不想创建过程输出太多信息，可以删除“-verbose” 。
上述签名会直接覆盖原来的文件，如果不想被覆盖而签名为另外的新文件 signed.akp，只需将 to_sign.apk 改为 -signedjar to_sign.apk signed.akp 即可。

签名后可以使用如下命令验证是否签名成功：

`jarsigner -verify to_sign.apk`

如果需要查看更详细的验证信息，可使用：

`jarsigner -certs -verbose -verify to_sign.apk`

### 优化APK
如果不需要，这一步可以不做，但推荐执行

使用 zipalign 工具优化已签名的apk文件

`zipalign -v 4 unaligned.apk aligned.apk`

---
到此结束