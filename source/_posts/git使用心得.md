title: "git使用心得"
date: 2015-11-23 23:22:41
tags:技术 git
---

 `git init`  

将当前文件夹初始化成git仓库
	
 `git clone <address>`
 
从< address >检出仓库，< address > 可以是本地仓库，也可以是远程仓库

`git remote add origin <server>`

如果仓库不是检出的，可以指定远程仓库,server是远程仓库地址

`git add <fileName>`  `git add .`

将更改的文件提交到暂存区 `git add .` 是添加（除去ignore）所有改动的文件

`git commit -m "message"`

将add后的文件提交到head中，等待push到远程仓库

`git push <origin> <master>`

将commit的文件提交到远程仓库，其中origin 是本地的文件 master是远程的指定分支

`git pull`


``