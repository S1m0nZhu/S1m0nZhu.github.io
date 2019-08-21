---
title: git学习笔记
date: 2019-08-21 12:38:59
tags: git github
---

按照



​	虽然使用github有几个月了，但是都是照着网上别人的教程按部就班的操作，对git版本管理工具并没有一个完整的功能认识和实践操作，今天从网上搜集了一些较为完整的git使用教程，对git进行一次体系化地学习，为以后提高学习工作效率打下基础。

下面，我将从简介、安装、常用命令、替换工具几个方面对git进行一次全方位梳理，希望对你有所帮助。

Git诞生于 2005 年，是目前世界上最先进的分布式版本控制系统（没有之一）。

直接记录快照，而非差异比较
Git 和其他版本控制系统的主要差别在于，Git 只关心文件数据的整体是否发生变化，而大多数其他系统则只关心文件内容的具体差异。

https://git-scm.com/figures/18333fig0105-tn.png

近乎所有操作都是本地执行
在 Git 中的绝大多数操作都只需要访问本地文件和资源，不用连网。但如果用 CVCS 的话，差不多所有操作都需要连接网络。因为 Git 在本地磁盘上就保存着所有当前项目的历史更新，所以处理起来速度飞快。

时刻保持数据完整性
在保存到 Git 之前，所有数据都要进行内容的校验和（checksum）计算，并将此结果作为数据的唯一标识和索引

多数操作仅添加数据
常用的 Git 操作大多仅仅是把数据添加到数据库。

文件的三种状态
好，现在请注意，接下来要讲的概念非常重要。对于任何一个文件，在 Git 内都只有三种状态：已提交（committed），已修改（modified）和已暂存（staged）。已提交表示该文件已经被安全地保存在本地数据库中了；已修改表示修改了某个文件，但还没有提交保存；已暂存表示把已修改的文件放在下次提交时要保存的清单中。

https://git-scm.com/figures/18333fig0106-tn.png

## 安装

在 Linux 上安装
如果要在 Linux 上安装预编译好的 Git 二进制安装包，可以直接用系统提供的包管理工具。在 Fedora 上用 yum 安装：

$ yum install git-core

在 Ubuntu 这类 Debian 体系的系统上，可以用 apt-get 安装：

$ apt-get install git

##常用命令


使用Git前，需要先建立一个仓库(repository)。您可以使用一个已经存在的目录作为Git仓库或创建一个空目录。

使用您当前目录作为Git仓库，我们只需使它初始化。

git init
使用我们指定目录作为Git仓库。

git init newrepo
从现在开始，我们将假设您在Git仓库根目录下，除非另有说明。

添加新文件
我们有一个仓库，但什么也没有，可以使用add命令添加文件。

git add filename
可以使用add... 继续添加任务文件。

提交版本
现在我们已经添加了这些文件，我们希望它们能够真正被保存在Git仓库。

为此，我们将它们提交到仓库。

git commit -m "Adding files"
如果您不使用-m，会出现编辑器来让你写自己的注释信息。

当我们修改了很多文件，而不想每一个都add，想commit自动来提交本地修改，我们可以使用-a标识。

git commit -a -m "Changed some files"
git commit 命令的-a选项可将所有被修改或者已删除的且已经被git管理的文档提交到仓库中。

千万注意，-a不会造成新文件被提交，只能修改。

发布版本
我们先从服务器克隆一个库并上传。

git clone ssh://example.com/~/www/project.git
现在我们修改之后可以进行推送到服务器。

git push ssh://example.com/~/www/project.git
取回更新
如果您已经按上面的进行push，下面命令表示，当前分支自动与唯一一个追踪分支进行合并。

git pull
从非默认位置更新到指定的url。

git pull http://git.example.com/project.git

删除
如何你想从资源库中删除文件，我们使用rm。

git rm file
分支与合并
分支在本地完成，速度快。要创建一个新的分支，我们使用branch命令。

git branch test
branch命令不会将我们带入分支，只是创建一个新分支。所以我们使用checkout命令来更改分支。

git checkout test
第一个分支，或主分支，被称为"master"。

git checkout master
对其他分支的更改不会反映在主分支上。如果想将更改提交到主分支，则需切换回master分支，然后使用合并。

git checkout master
git merge test

如果您想删除分支，我们使用-d标识。

git branch -d test