title: Android Studio 下获取 Sha1
date: 2015-02-12 10:26:35
category: 技术
tags:  [Android Studio,Sha1]
description: 在使用一些第三方库的时候，需要我们提供需要开发者提供SHA1证书指纹数据，这个在 eclipse 很容易就找到了，但是 Android Studio 却不是那么容易找到 ...

---
- 打开 cmd ，进入到 .android 目录下，一般在 C:\Users\用户名\ 目录下

![](http://7xpk47.com1.z0.glb.clouddn.com/sha1_01.png)

- 输入 `keytool -list -keystore debug.keystore` 

   debug.keystore 这个是android sdk 提供的默认签名文件

   ![](http://7xpk47.com1.z0.glb.clouddn.com/sha1_02.png)

- 这是会提示你输入秘钥口令，不用管它，直接确定就可以，如果不行就输入 android（这个是 debug.keystore 的默认秘钥口令）
