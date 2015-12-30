title: 使用Hexo+GitHub搭建个人博客
date: 2015-12-28 20:23:48
category: 技术
tags: Blog搭建
description: 使用 Node.js-Hexo 框架搭建个人 Blog
---
 准备工作：
 安装node.js 参考[官方文档](https://nodejs.org/en/)

## 1.安装hexo
安装node.js之后，可以直接打开node带的cmd工具，输入下面命令安装hexo

`npm install hexo-cli -g`

顺便介绍几个 hexo 的常用命令 

   - 初始化一个项目 `hexo init <fileName>`

   - 安装项目依赖 `cd <fileName> && npm install`
   
   - 生成静态文件 `hexo generate` 或 `hexo g`

   - 启动项目  `hexo server` 或 `hexo s`
   
   - 一键部署 `hexo deploy` 或 `hexo d`
   
### 下面说几个需要注意的地方

 一键部署需要另外安装模块，比如部署到github就需要安装 hexo-deployer-git 模块,执行

`npm install hexo-deployer-git --save`

就安装到本地了，之后我们只用在命令行输入 `hexo d` 就可以将我们的Blog部署到远程服务器。这个下面我们会再说。我们也可以将 `hexo-deployer-git` 这个 modules 写入到到项目的 package.json 文件里，这样移动项目就不用每次都安装这个依赖了。这里就不细讲了，需要了解可以去学习一下 node.js 的包管理。

国内有时候连不上npm或者连得上但是下载很慢，这里推荐使用[ cnmp ](http://npm.taobao.org/)(淘宝NPM镜像).

执行下面这个命令

`npm install -g cnpm --registry=https://registry.npm.taobao.org`

安装 cnpm 模块，以后再执行 npm 命令时，使用 cnmp 代替 npm 就可以了。

## 2. 新建Blog

工具安装的差不多之后，就可以打造属于自己的blog了

### 初始化项目，并安装依赖的modules
	$ hexo init MyBlog

	$ cd MyBlog && npm install

### 生成静态web文件 && 部署本地服务器

	$ hexo g
	$ hexo s 

打开浏览器输入 `localhost:4000` 就可以看到你的Blog了。 

## 3. 部署到GitHub

现在我们的个人Blog还是部署在本地的，接下来我们将我们的Blog部署到GitHub上，当然你也可以部署到其他的地方，这里就不再多说了。

上面我们提到使用 `hexo-deployer-git` 这个模块部署，使用这个模块我们只用一个命令就可以部署到github上，省去了输入 git 命令的麻烦，当然你要是不嫌麻烦也可以不用。下面我们来介绍如何使用  `hexo-deployer-git` ：

打开你项目目录下的 -config.yml 文件,添加如下配置

	deploy:
 	 	type: git
  		repo: <repository url>
  		branch: [branch]
  		message: [message]

![](./img/png1.png)

按照上面的配置以后，回到项目的目录下，输入

`hexo deploy`

就可以将我们的blog部署到 github 上了

如果有什么不懂得可以参考[deploy使用说明](https://hexo.io/zh-cn/docs/deployment.html)

