title: git 使用
date: 2015-10-26 16:43:12
category: git
tags: [ git,项目管理 ]
description: 学习Git的使用
---
`git init`  将当前文件夹初始化成git仓库
	
`git clone <address>` 从< address >检出仓库，< address > 可以是本地仓库，也可以是远程仓库

`git remote add origin <server>` 如果仓库不是检出的，可以指定远程仓库,server是远程仓库地址

`git status`  查看状态

`git diff` 查看变更的内容

`git add <fileName>`  `git add .` 将更改的文件提交到暂存区 `git add .` 是添加（除去ignore）所有改动的文件

`git mv <old> <new>`  更改文件名

`git rm <file>` 删除文件

`git commit -m "message"` 将add后的文件提交到head中，等待push到远程仓库

`git push <remote> <master>` 将commit的文件提交到远程仓库

`git pull` 下载代码并快速合并

`git reset --hard HEAD` 撤消工作目录中所有未提交文件的修改内容（hard只是其中一个可选项，后面再细说）

`git checkout HEAD <file>` 撤销指定的未提交文件的修改内容

`git revert <commit>` 撤销指定的提交

`git log` 查看提交历史

`git log -p <file>` 查看指定文件的提交历史

`git branch` 显示所有的本地分支

`git checkout <branch/tag>` 切换到指定分支/标签

`git branch <branch>` 创建新分支

`git branch -d <branch>` 删除本地分支

`git tag` 显示所有本地标签

`git tag <tagName>` 创建标签

`git tag -d <tagName>` 删除标签

`git remote -v` 查看远程版本库信息

`git remote show <remote>` 查看指定远程版本库信息

`git fetch <remote>` 从远程库获取代码

`git push <remote> :<branch/tagName>` 删除远程分支/标签

`git push --tags` 上传所有标签