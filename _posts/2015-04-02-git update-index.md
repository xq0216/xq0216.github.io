---
layout: post
title: Git忽略本地文件修改的方法
categories: []
tags: [git]
published: True

---

在使用git时，对于本地配置文件，肯定不必提交，但总是在'git status'中看到文件修改，让我眼里不爽。

找了半天，终于找到完全在本机忽略本地文件修改的办法：

	git update-index --assume-unchanged build/conf/a.conf

要恢复的话，方法如下：

	git update-index --no-assume-unchanged build/conf/a.conf

如果想知道当前被忽略修改的本地文件列表，使用如下命令：

	git ls-files -v | grep -e "^[hsmrck]"