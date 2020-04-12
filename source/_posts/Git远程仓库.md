---
title: Git远程仓库
toc: true
date: 2020-02-26 15:08:59
tags: git
categories: git
author: lixuanfeng
---

Git 并不像 SVN 那样有个中心服务器。目前我们使用到的 Git 命令都是在本地执行，如果你想通过 Git 分享你的代码或者与其他开发人员合作。 你就需要将数据放到一台其他开发人员能够连接的服务器上。

<!-- more -->

## 查看远程分支

加上-a参数可以查看远程分支，远程分支会用红色表示出来（如果你开了颜色支持的话）：

```shell
$ git branch -a
  master
* fenzhi
  remotes/origin/master
```

### 添加远程库

要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用,命令格式如下：

```shell
git remote add [shortname] [url]
```

## 查看当前的远程库

要查看当前配置有哪些远程仓库，可以用命令：

```shell
git remote
$ git remote
origin
$ git remote -v
origin	git@github.com:tianqixin/w3cschool.cc.git (fetch)
origin	git@github.com:tianqixin/w3cschool.cc.git (push)
```

执行时加上 -v 参数，你还可以看到每个别名的实际链接地址。

## 重命名远程分支

在git中重命名远程分支，其实就是先删除远程分支，然后重命名本地分支，再重新提交一个远程分支。

例如下面的例子中，我需要把 devel 分支重命名为 develop 分支：

```shell
$ git branch -av
```

## 提取远程仓库

Git 有两个命令用来提取远程仓库的更新。
1、从远程仓库下载新分支与数据：

```shell
git fetch
```

该命令执行完后需要执行git merge 远程分支到你所在的分支。

2、从远端仓库提取数据并尝试合并到当前分支：
git pull

该命令就是在执行 git fetch 之后紧接着执行 git merge 远程分支到你所在的任意分支。

假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行 git fetch [alias] 告诉 Git 去获取**它有你没有的数据**，然后你可以执行 git merge [alias]/[branch] 以将服务器上的任何更新（假设有人这时候推送到服务器了）合并到你的当前分支。

## 推送到远程仓库

推送你的新分支与数据到某个远端仓库命令:

```shell
git push [alias] [branch]
```

以上命令将你的 [branch] 分支推送成为 [alias] 远程仓库上的 [branch] 分支，实例如下。

```shell
$ git merge origin/master
Updating 7d2081c..f5f3dd5
Fast-forward
 "w3cschool\350\217\234\351\270\237\346\225\231\347\250\213\346\265\213\350\257\225.txt" | 1 +
 1 file changed, 1 insertion(+)
bogon:w3cschoolcc tianqixin$ vim w3cschoolphp中文网测试.txt 
bogon:w3cschoolcc tianqixin$ git push origin master
Everything up-to-date
```

## 删除远程分支和tag

在Git v1.7.0 之后，可以使用这种语法删除远程分支：

```shell
$ git push origin --delete <branchName>
```

删除tag这么用：

```shell
git push origin --delete tag <tagname>
```

否则，可以使用这种语法，推送一个空分支到远程分支，其实就相当于删除远程分支：

```shell
git push origin :<branchName>
```

这是删除tag的方法，推送一个空tag到远程tag：

```shell
git tag -d <tagname>
git push origin :refs/tags/<tagname>
```

两种语法作用完全相同。