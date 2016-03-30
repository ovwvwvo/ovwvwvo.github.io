title: git tag 的使用
date: 2015-10-18 17:06:02
category: git
tags: git tag
description: 使用 git 管理项目的时候，一个版本结束的时候，我们需要为当前状态添加 tag ,用来方便以后的查看和使用...
---
## git tag

* 查看tag
`git tag` 列出所有标签
`git show [tagname]` 查看标签信息

* 添加标签
`git tag -a [tagname] ` 添加标签
`git tag -a [tagname] -m "message"` 添加带备注的标签
`git tag -a [tagname]  [SHA-1校验码]` 添加标签到之前的的位置

* 删除标签
`git tag -d [tagname]` 删除标签
`git push origin :[tagname]` 删除远程仓库标签

* 发布标签
`git push origin [tagname]` 将标签推送到远程仓库
`git push origin --tags`  将所有标签推送到远程仓库

* 切换到标签
`git checkout [tagname]` 切换到指定标签