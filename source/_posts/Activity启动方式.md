title: Activity 启动方式
date: 2014-11-19 22:20:50
tags: Android启动方式
category: Android
description: Activity 是 Android 的四大组件之一，在 Android 系统中是通过栈的方式对多个 Activity 进行管理。启动方式决定了 Android 系统在启动一个 Activity 时，对栈该进行什么样的操作。
---
Activity 是 Android 的四大组件之一，在 Android 系统中是通过栈的方式对多个 Activity 进行管理。启动方式决定了 Android 系统在启动一个 Activity 时，对栈该进行什么样的操作。

## Activity 启动方式

### standard方式

如果不在manifest文件中声明 activity 的 launchmode，默认就是 standard 类型。这种类型很简单粗暴，每次新建一个 activity，都会在栈顶重新创建一个新的 activity，优点是简单，每次都用新的，缺点是耗资源。

### singleTop 方式

之所以除了 standard 类型都带有 single 的前缀，google 应该是想说明其他几种方式都有单例模式的影子，singleTop如其名，在将要运行一个 activity 时，先看看栈顶的activity是不是要运行的那个，如果是就不建新的了，直接用，如果不是，就建一个新的放到栈顶。暂时没想到应用场景，activity 自己调自己的时候多么，不然一样要新建 activity。

### singleTask 方式

这个狠，运行一个 activity 之前，先看栈里面有没有这个 activity，没有的话，新建一个放到栈顶，有，直接拉到栈顶用，而且秒杀原来在它上面的所有 activity，有点像拉大车，优点是省资源，而且如果一个 app 需要在从 home 页进去n层深的页面一下子会到 home 页，按返回键直接退出客户端，你就用它吧。

### singleInstance 方式

这种类型的 activity 在运行后会被安排到单间，除了第一次创建的时候调用 oncreate，后面不会再调，但是会调用 onNewIntent 。网上的技术文章都说像是浏览器，确实有点像，就这么理解吧。
但是发现声明成 singleInstance 类型的 activity 中调用 startActivityForResult方法有问题，会瞬间返回一个 resultcode = 0 的错误结果，从 log 看，应该是在启动另一个 activity 之前就返回了，可见startActivityForResult在此类享受单间待遇的 activity 中已经变成不确定因素了，所以最好别用。根本原因未知，还在调查中。

 

## Intent 的常用 Flag 参数

### FLAG_ACTIVITY_CLEAR_TOP

例如现在的栈情况为：A B C D 。D此时通过 intent 跳转到B，如果这个 intent 添加 FLAG_ACTIVITY_CLEAR_TOP 标记，则栈情况变为：A B。如果没有添加这个标记，则栈情况将会变成：A B C D B。也就是说，如果添加了 FLAG_ACTIVITY_CLEAR_TOP 标记，并且目标Activity 在栈中已经存在，则将会把位于该目标 activity 之上的 activity 从栈中弹出销毁。这跟上面把B的 Launch mode 设置成 singleTask 类似。

### FLAG_ACTIVITY_NEW_TASK

例如现在栈1的情况是：A B C。C通过 intent 跳转到D，并且这个 intent 添加了 FLAG_ACTIVITY_NEW_TASK 标记，如果D这个 Activity 在 Manifest.xml 中的声明中添加了 Task affinity ，并且和栈1的affinity不同，系统首先会查找有没有和D的 Task affinity 相同的 task 栈存在，如果有存在，将D压入那个栈，如果不存在则会新建一个D的affinity的栈将其压入。如果D的 Task affinity 默认没有设置，或者和栈1的 affinity 相同，则会把其压入栈1，变成：A B C D，这样就和不加 FLAG_ACTIVITY_NEW_TASK 标记效果是一样的了。 注意如果试图从非activity的非正常途径启动一个 activity ，比如从一个service中启动一个 activity ，则 intent 比如要添加 FLAG_ACTIVITY_NEW_TASK 标记。

### FLAG_ACTIVITY_NO_HISTORY

例如现在栈情况为：A B C。C通过 intent 跳转到D，这个 intent 添加FLAG_ACTIVITY_NO_HISTORY 标志，则此时界面显示D的内容，但是它并不会压入栈中。如果按返回键，返回到C，栈的情况还是：A B C。如果此时D中又跳转到E，栈的情况变为：A B C E，此时按返回键会回到C，因为D根本就没有被压入栈中。

### FLAG_ACTIVITY_SINGLE_TOP

和上面 Activity 的 Launch mode 的 singleTop 类似。如果某个 intent 添加了这个标志，并且这个 intent 的目标 activity 就是栈顶的 activity ，那么将不会新建一个实例压入栈中。


摘自 <http://blog.sina.com.cn/s/blog_643d78190101amc7.html>

摘自 <http://www.cnblogs.com/playing/archive/2011/05/14/2046445.html> 


