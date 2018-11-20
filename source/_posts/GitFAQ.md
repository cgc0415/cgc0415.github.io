---
title: git命令
date: 2018-10-26 23:09:50
tags: Git
categories: 版本控制
---
### git工作流示意图
{% asset_img git-workflow.jpg pic:git工作流示意图 %}
### git clone
远程操作的第一步，通常是从远程主机克隆一个版本库，这时就要用到`git clone`命令。
```
$ git clone <版本库的网址>
```
比如：
```
$ git clone git@github.com:cgc0415/hello-world.git
```
该命令会在本地主机生成一个目录，与远程主机的版本库同名。如果要指定不同的目录名，可以将目录名作为`git clone`命令的第二个参数。
```
$ git clone <版本库的网址> <本地目录名>
```
### git remote
为了便于管理，Git要求每个远程主机都必须指定一个主机名。`git remote`命令就用于管理主机名。
不带选项的时候，`git remote`命令列出所有远程主机。
```
$ git remote
origin
```
使用`-v`选项，可以参看远程主机的网址。
```
$ git remote -v
origin  git@github.com:cgc0415/hello-world.git (fetch)
origin  git@github.com:cgc0415/hello-world.git (push)
```
上面命令表示，当前只有一台远程主机，叫做origin，以及它的网址。
### git pull
`git pull`命令的作用是，取回远程主机某个分支的更新，再与本地的指定分支合并。它的完整格式稍稍有点复杂。
```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```
比如，取回`origin`主机的`next`分支，与本地的`master`分支合并，需要写成下面这样。
```
$ git pull origin next:master
```
在某些场合，Git会自动在本地分支与远程分支之间，建立一种追踪关系（tracking）。比如，在`git clone`的时候，所有本地分支默认与远程主机的同名分支，建立追踪关系，也就是说，本地的`master`分支自动"追踪"`origin/master`分支。
如果当前分支与远程分支存在追踪关系，且远端只有一个追踪分支，则直接执行`git pull`就可以。

```
$ git pull
```
上面命令表示，当前分支自动与唯一一个追踪分支进行合并。
### git push
`git push`命令用于将本地分支的更新，推送到远程主机。它的格式与`git pull`命令相仿。
```
$ git push <远程主机名> <本地分支名>:<远程分支名>
```
如果省略远程分支名，则表示将本地分支推送到与之存在"追踪关系"的远程分支（通常两者同名），如果该远程分支不存在，则会被新建。
```
$ git push origin master
```
上面命令表示，将本地的master分支推送到origin主机的master分支。如果后者不存在，则会被新建。
如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。
```
$ git push origin :master
# 等同于
$ git push origin --delete master
```
上面命令表示删除origin主机的master分支。
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做`git pull`合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用`--force`选项。
```
$ git push --force origin master
```
上面命令使用`--force`选项，结果导致远程主机上更新的版本被覆盖。除非你很确定要这样做，否则应该尽量避免使用`--force`选项。

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
### 删除文件或文件夹
删除文件
```
git rm filename
```
删除foldername文件夹及其下所有的文件
```
git rm foldername -r -f
```
执行完git rm后，最后再git commit -m ""，然后push即可
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