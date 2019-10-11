## Git 基本概念
- 本地分支  
**工作区** (还未纳入版本控制)  
**暂存区** git add后的区域  
**仓库区** git commit后但并未 push 的区域    
**贮藏区** (stash) 临时保存文件修改的区域  
- 远端分支

## GIT常见问题
- 我的提交信息(commit message)写错了
```
git commit --amend -m 'xxxx'
```
- 我想撤销上一次的提交(commit)
```
## 这里只能撤销并未push到远端分支的commit,撤销后的代码会在工作区
git reset HEAD^
```
- 我的代码写错分支了
```
git checkout --merge branch
```
- 需要回退已经push到远端的代码
```
git revert HASH
```
- 回退单个文件
```

```

