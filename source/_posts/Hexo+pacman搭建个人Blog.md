title: Hexo+pacman搭建个人Blog
date: 2016-01-01 23:12:30
category: Node.js
tags: Blog搭建
description: 使用 pacman 给 Hexo 搭建的 Blog 更换主题
---
Hexo 社区给我们提供很多个性化主题 ，各种主题让我眼花缭乱，最后我选择了 [Pacman]() 作为 Blog 的主题。

这个主题网上的教程挺多的，而且用起来也挺顺手的，这里就挑几个地方记下来

### 添加页面 
使用 hexo new page "pageName" 就会添加一个页面，然后在 pacman 的 _config.yml 里面 meun 选项下添加一个选项就可以

### widgets
这个是主页面的小挂件，pacman 为我们提供了很多控件，这里就不说了。

### 添加订阅（rss）

最近了 pacman 好像已经安装了 rss modules,如果你的上面没有安装，执行下面就可以了

	npm install hexo-generator-feed

### 添加站内地图
	
	npm install hexo-generator-sitemap



突然发现这个blog写的很详细 
可以参考[这个](http://jerrychia.com/2015/03/28/hexo-use-pacman-theme/)