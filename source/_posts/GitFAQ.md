---
title: git命令
date: 2018-10-26 23:09:50
tags: Git
categories: 版本控制
---

### 【git回车换行设置】---避免Windows自动将Linux的换行符转为Windows风格，造成文件二进制不一致

> 执行git config --list，查看所有设置
> 确保 core.autocrlf=false
> 如果不是则用如下命令修改：
> git config --global core.autocrlf false

### 修改文件名
```
git mv originfilename changed_filename
git commit -m ""
```

### stash的使用

有时候我们在工作区进行开发并且不想提交的时候，这时我们又想pull最新代码；或者又想切到另外一个分支上修改紧急bug的时候
git stash可以暂存当前的工作区内容：

```
git stash save "stash information."
```

等我们切到另外分支修改完了bug之后，可以切回之前分支【一定要先切回原分支再执行下面的pop或apply命令】，然后恢复之前工作区的内容继续开发：
```
git stash pop
```

也可以查看stash的Git栈信息：
```
git stash list
```

当我们的stash栈列表里面有很多，并且我们想要找到对应的版本号并且将我们想要的版本号为stash@{2}的工作内容取出来：
```
git stash apply stash@{2}
```

也可以查看版本号为stash@{2}的工作内容：
```
git stash show stash@{2}
```

可以将栈清空：
```
git stash clear
```

### 查看某次提交中某个文件的改动情况
```
git show commit-id filename
```

### 查看分支历史
```
git reflog show --date=iso branchname
```

### git-rebase

> 当从master拉完分支，修改后，发现需要合入master分支上最新的commit时，可以先提交该分支上的修改，然后checkout到master上，git pull到最新，然后切回分支，执行 git rebase master 即可。

### 回退节点
```
git reset --hard commitid
```

### 【git clean】删除untracked files
```
git clean -f
```