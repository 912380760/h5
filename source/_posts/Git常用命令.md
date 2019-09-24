---
title: Git常用命令
date: 2019-09-06 16:26:19
tags: Git
---

## Git 基本概念
- 分支
**本地分支**(工作分支/开发分支)
**远端分支**  
**HEAD** 当前分支引用的指针（上一次提交的快照，下一次提交的父结点）
- 文件状态
未纳入版本控制  
已纳入版本控制
冲突文件
- 存储
**工作区** (还未纳入版本控制)
**暂存区** git add后的区域
**仓库区** git commit后但并未 push 的区域  
**贮藏区** (stash) 临时保存文件修改的区域

## git add
用于将变化的文件从工作区提交到暂存区,可以使用**git status**命令查看目前的暂存区放置了哪些文件.
- ** git add <file\> ** 将指定文件放入暂存区
- ** git add <directory\> ** 将指定目录下所有的变化放入暂存区
- **git add .** 将当前目录所有变化的文件放入暂存区
### 参数
- **-f** 强制添加某个文件,不管 **.gitignore** 是否包含这个文件
 ```
 git add -f <fileName>
 ```
- **-u** 参数表示只添加暂存区已有的文件(包括删除操作),但不添加新增的文件
- **-A | --all** 参数表示追踪所有操作
- **-p** 进入交互模式,指定哪些修改需要添加到暂存区,即使是同一个文件,也可以只提交部分改动.

## git commit 
将暂存区中的变化提交到仓库区  
- **-m** 用于指定commit信息,是必须的,如果省略 **-m** 参数,**git commit** 会自动打开文本编辑器,要求输入
```
# 跳过 git add 暂存区,直接将指定文件从工作区提交到仓库区 
git commit <filename> -m 'message'
```
- **-am** 将所有修改和删除的文件添加进暂存区(不包括新增文件),指定commit信息后推送到仓库区
- **--amend** 修改最近一次的提交信息 
```
git commit --amend -m "New commit message"**
```
- [为什么要先 git add 才能 git commit ？](https://www.zhihu.com/question/19946553/answer/29033220)

## git reset
将HEAD引用指向给定提交
- **--mixed** git reset默认模式，将修改的代码添加入工作区
- **--soft** 将修改的代码加入暂存区（add后还未commit）
- **--hard** 将修改的代码丢弃
```
#撤销commit修改，存储代码
git reset <HEAD> #回退到指定commit
git stash #存储代码

#回退已push到远程分支的代码，并舍弃修改
git reset --hard <HEAD> #回退到指定提交，丢弃修改
git push -f origin <branchName> #强制将远端分支的HEAD指向本地分支 （有很大的风险，push到远程分支后，HEAD后commit会在远程分支上会消失）
```

## git push
将代码推送到远端分支
- **git push** 将当前分支推送到默认的master分支
- **git push origin <branchName>** 将当前分支推送到指定的远端分支
### 参数
- **--delete** 删除指定的远程分支
```
git push origin --delete <branchName>
```

## git branch 
分支操作命令,需要特别注意,**git branch**操作的都是当前分支
**git branch** 列出所有本地分支
**git branch <new branch>** 新建分支,clone当前分支内容到新分支,与 **git checkout -b** 的区别是并不会切换到新分支
### 参数
- **-a** 列出所有本地分支和远程分支
- **-d | -D** 删除本地分支
```
#删除本地分支,前提是该分支没有为合并的变动
git branch -d <branchName>

#强制删除本地分支,不管有没有未合并变化
git branch -D <branchName>
```
- **-m** 重命名本地分支(远程分支)
```
# 为当前分支重命名
git branch -m <branchName>

# 为指定分支重命名
git branch -m <new branchName> <old branchName>

# 为远程分支重命名,其实就是先删除远程分支，然后重命名本地分支，再重新提交一个远程分支。
git checkout <old branchName> #切换到远程分支
git pull #拉去最新的分支内容
git branch -m <new branchName> <old branchName> #修改本地分支名称
git push origin --delete <old branchName> #删除远程分支
git push origin <new branchName> #推送当前分支到远端
```

## git checkout
用于切换分支和恢复文件  
**checkout** 分支时需要将当前改动 **commit** 或者 **stash** 起来, 不然会有以下两个问题:  
如果已纳入版本控制的文件有改动将无法切换,  
未纳入版控的文件将随着 **checkout** 到新的分支
- **git checkout <branch>** 切换本地分支
- **git checkout <commitID>** 切换到指定快照(commit),在快照上修改无法提交到此快照上,提交需要 **git checkout <new branch>** 把快照切换到新分支.
- **git checkout tags/1.1.4** 切换到某个tags
### 参数
- **-b | -B** 创建新分支,clone当前分支内容,切换到该分支(保留分支的提交记录) **git checkout -b <new branch>**     
如果存在同名分支 -b 会提示错误,-B 会强制创建新分支,并且会覆盖原来存在的同名分支
- **--orphan**  将当前内容切换到新分支,当前分支会是一个全新的分支没有任何提交记录(和-b|-B的区别)
```
git checkout --orphan <new_branch>
```
- **--merge** 将当前分支工作区的修改内容(修改并没有commit的内容)合并到切换的分支下  
```
#需要注意的问题
#1.合并可能产生冲突
#2.切换到新分支后,前分支的修改内容会消失
git checkout --merge <branch>
```
- -\- 用于恢复文件
``` 
# 放弃工作区对该文件的修改
git checkout -- <filename>

# 指定从某个commit恢复指定文件
git checkout <commitID>~ -- <filename>
```
- **-p** 进入交互模式,只恢复部分变化

## git stash
将工作区和暂存区的修改添加到储藏区
- **git stash** 将工作区和暂存区的修改添加到储藏区，已经commit到仓库区的代码并不会被储藏
- **git stash list** 查看现有的储藏列表
- **git stash apply <stashName>** 应用储藏, 不指定stashName会应用最近的储藏

## git merge
将指定分支与当前分支合并（注意这里的合并是相反的，还有需要注意的是需要合并远程分支而不是本地分支）
