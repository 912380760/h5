---
title: Git常用命令
date: 2019-09-06 16:26:19
tags:
--- Git

## Git 基本概念
- 本地分支(工作分支/开发分支) 
- 暂存区 commit之后但未push的暂存区域 
- 贮藏区(stash) 临时保存文件修改内容的区域
- 远程分支  
- HEAD 指向现在使用中的分支的最后一次更新

## git checkout
用于切换本地分支
- git checkout <branch> 切换本地分支
- git checkout -b|-B <new_branch> 创建新分支,clone当前分支内容,切换到该分支(保留分支的提交记录)   
如果存在同名分支 -b 会提示错误,-B 会强制创建新分支,并且会覆盖原来存在的同名分支
- git checkout --orphan <new_branch> 将当前内容切换到新分支,当前分支会是一个全新的分支没有任何提交记录(和-b|-B的区别)
- git checkout --merge <branch> 这个命令用于将当前分支修改的内容(修改并没有commit的内容)合并到切换的分支下  
需要注意的问题: 1.合并容易产生冲突 2.切换到新分支后,修改内容会消失



