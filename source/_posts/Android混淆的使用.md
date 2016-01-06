title: Android混淆的使用
date: 2016-01-06 22:46:49
category: 技术
tags:  [ProGuard,混淆]
description: Android项目开发的时候，我们使用混淆可以加密我们的App,增加我们App被破解的难度，同时也可以减小我们App的体积

---
##混淆的用法 


- `-keep [,modifier,...] class`  不混淆某些类别

- `-keepclassmembers [,modifier,...] class`  不混淆类的成员

- `-keepclasseswithmembers [,modifier,...] class`  不混淆类及其成员

- `-keepnames class`   不混淆类及其成员名

- `-keepclassmembernames class`  不混淆类的成员名

- `-keepclasseswithmembernames class`  不混淆类及其成员名

- `-dontwarn [class_filter]`		不提示warnning

在 Android 开发中，不需要被混淆（就是需要添加混淆规则的）的有哪些呢？

##下列内容不希望被混淆

1. 反射用到的类

2. JNI方法

3. Parcelable的子类和Creator静态成员变量不混淆，否则会产生android.os.BadParcelableException异常

4. 使用GSON、fastjson等框架时，所写的JSON对象类不混淆，否则无法将JSON解析成对应的对象

5. 有用到WEBView的JS调用也需要保证写的接口方法不混淆

##### Example

Webview调用js通讯

    -keep @interface android.webkit.JavascriptInterface
    -keep class android.webkit.JavascriptInterface {*;}
    -keepattributes *JavascriptInterface*
    -keepclassmembers class [your Class name]$[yourJavaScriptInterface]{
       <methods>;
    }

第三方类库

    -keep class butterknife.** { *; } 
    -dontwarn butterknife.internal.**
    -keep class **$$ViewBinder { *; } 不混淆以ViewBinder结尾的类

参考文档：

SDK\tools\proguard\（本地SDK路径）

http://proguard.sourceforge.net/index.html#manual/usage.html

http://malinkang.com/blog/2015/09/21/android-proguard/