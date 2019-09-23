---
title: webStorm使用技巧
date: 2019-07-18 16:23:19
tags: editor
---

## 安装
建议从官网下载最新版本[webStorm](https://www.jetbrains.com/webstorm/download/#section=windows)

## 注册
修改hosts文件,用自带的文本编辑器可能无法保存host文件,建议用notePad++打开
```
# windows下的位置
C:\Windows\System32\drivers\etc

# 将下面代码放在最后一行
0.0.0.0 account.jetbrains.com

# 网上随意找一个激活码就可以激活了
```

## 常用快捷键
- 删除当前行 Ctrl + Y
- 下方插入新行 Shift + Enter
- 当前文件搜索 Ctrl + F
- 当前文件搜索替换 Ctrl + R
- 全局搜索 Ctrl + Shift + F
- 全局搜索替换 Ctrl + Shift + R
- 全局搜索文件 Ctrl + Shift + N
- 代码检查设置 Ctrl + Shift + Alt + H
- 跳转到指定行 Ctrl + G(输入行数)
- 控制台 Ctrl + F12
- 重命名文件 Shift + F6
- 打开当前文件 右键 -> Show in Explorer
- 展开/关闭左侧项目 Alt + 1
- 版本控制 Alt + 9
- git commit: Ctrl + K
- push到当前远程分支 Ctrl + Shift + K
- 格式化文件 Ctrl + Alt + L
- 格式化选定区域 Ctrl + Alt + I
- 删除文件 Delete

## 常用操作
- 查看文件本地历史记录: VCS | Local History | Show History 左上角的返回标志是还原文件
- 重构命名,WebStorm会自动重命名其所有引用和import语句: Ctrl + Shift + Alt + T -> rename  -> refactor
- webStrom安装插件 File | Settings | plugins 
- webStrom修改主题 File | Settings | 搜索theme
- 解决冲突: 随便右键一个文件选择Git -> Resolve Conflicts...  左边是合并分支,右边是当前分支,中间是修改后的代码.
- 逐行查看文件更改记录 右键文件打断点的行数位置 选择annotate
- 查看版本提交记录和修改 Ctrl + F12(打开控制台) -> Version Control -> log
- webStrom无法识别@符号跳转文件
```js
// 如果是vue-cli 3以上隐藏别名配置的这种情况,在根目录添加alias.config.js文件,再指定webpack配置文件,文件内容如下
const resolve = dir => require('path').join(__dirname, dir);

module.exports = {
    resolve: {
        alias: {
            '@': resolve('src')
        }
    }
};

// 指定webpack配置文件
// file -> setting -> 搜索webpack -> webpack configuration file 
// 在这里输入webpack别名配置文件地址 例: D:\react-learn\vueinit\alias.config.js.
``` 

## webStrom 插件推荐
webStrom本身就已经集成大部分功能而且占用CPU较高不建议安装太多没必要的插件
- Atom OneDark Theme 个人最喜欢的主题,用完一改webstrom丑丑的外观
- codeGlance 右侧代码预览(如果没有显示,尝试使用Ctrl+Shift+G快捷键切换关闭开启)

## 参考资料
[Meet WebStorm - Help | WebStorm](https://www.jetbrains.com/help/webstorm/2019.1/meet-webstorm.html)
