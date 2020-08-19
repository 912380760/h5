---
title: Git无法clone项目问题汇总
date: 2020-08-19 18:11:26
tags: Git
---

## Git clone失败方法汇总
- 提高git下载速度
```
git config --global http.postBuffer 524288000
```
- 修改clone深度
```
git clone https://XXX.git --depth 1
// git clone 是克隆所有历史版本
// 而 --depth 1 是克隆最近一次的commit， 1 代表克隆深度
```
使用这个方法能减少git clone的大小，但是clone下来的项目只有master分支，且因为版本不完整，不能进行正常的提交。  
解决办法:
```
git pull --unshallow
// 拉取完整项目，但是依然没有master外其他分支
```
修改git config文件拉取所有远程分支
```
vim .git/config
```
按照如下示例修改：
```
修改前：
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = https://github.com/ReactiveX/rxjs
    fetch = +refs/heads/master:refs/remotes/origin/master
[branch "master"]
    remote = origin
    merge = refs/heads/master

修改后：
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = https://github.com/ReactiveX/rxjs
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```
再运行
```
git fetch -v
```
## vim安装和操作
- [vim下载地址](https://github.com/vim/vim-win32-installer/releases)，选择一个zip包下载后解压即
- 添加环境变量 我的电脑-属性-高级系统设置-环境变量-Path  
点击编辑-新建-C:\Users\lucien\Desktop\vim\vim82(输入你解压后的地址)
- vim分为插入模式和正常模式，正常模式只能阅读不能修改，按i进入插入模式，按esc退出。
- 退出命令:q
- 保存退出:wq

## 参考链接
[git clone --depth=1 之后怎样获取完整仓库?](https://segmentfault.com/q/1010000000409170)
[vim 操作命令大全](https://blog.csdn.net/weixin_37657720/article/details/80645991)