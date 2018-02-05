---
title: git 学习
date: 2018-02-05 10:28:48
tags:
---
## merge与rebase的区别
#### git merge 
用pull命令把远端分支上的修改拉下来并且和你的修改合并，结果看起来就像是一个新的“合并的提交”
#### git rebase
rebase 意为垫底的意思 --rebase选项告诉git把本地的提交移到同步了中央仓库修改后的master分支的顶部，rebase命令会把你功能分支的每个commit取消掉，然后放到master的提交的后面。
***
在rebase的过程中，也许会出现冲突，在这种情况下，git会停止rebase，在解决完冲突后，用git-add命令去更新这些内容的索引，然后，无需执行git-commit，只需执行git rebase --continue。如果碰到了冲突，但发现搞不定，执行 git rebase --abort（abort 中止计划）