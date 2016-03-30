title: 从手机导出data/data下的数据
date: 2015-11-12 17:00:45
category: Android
tags: 获取data目录下的数据
description: 从手机（不用root）获取 data/data 目录下的用户数据

---

我们调试 App 的时候有时候要去除应用下 data/data/ 的文件，之前我都是运行在虚拟机上，然后再取出数据。今天发现一个好的方法，可以在真机上（不用 root ）直接去除 data/data/ 下的数据。

- 首先打开 Android studio 的 Terminal 界面，或者打开命令行，切换到项目的目录下；
- 然后依次执行下面的命令

`$ adb shell`      #执行adb shell命令连接手机设备

`$ run-as com.packagename`       #执行run-as命令切换当前用户,这里输入你应用的包名

`$ pwd`			#定位当前文件位置

`$ ls`		#查看当前文件夹下的文件

`$ cat databases/xx.db > /sdcard/xx.db`     #使用cat命令导出需要的文件(xx.db)到sd卡

然后你就可以看到你需要的文件输出到手机的 sdcard 指定位置，移动到电脑，就可以查看了。
