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

## 一、安装

在 Linux 上安装
如果要在 Linux 上安装预编译好的 Git 二进制安装包，可以直接用系统提供的包管理工具。在 Fedora 上用 yum 安装：

$ yum install git-core

在 Ubuntu 这类 Debian 体系的系统上，可以用 apt-get 安装：

$ apt-get install git

##二、常用命令


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

##三、使用场景（1）

删除master分支下的所有历史版本与log，只保留当前的版本，并同步至GitHub

###方法一
先新建一个名为latest_branch的分支，然后将当前master分支中的所有文件添加到latest_branch分支中，接着等待移动完毕后删除master分支，最后把latest_branch这个分支的分支名改为master。
具体实现：

1、切换到latest_branch分支下
git checkout --orphan latest_branch
2、 添加所有文件
git add -A
3、 提交更改
git commit -am "清除所有历史版本以减少仓库大小，请重新从远程拷贝此仓库"
4、 删除分支
git branch -D master
5、将当前分支重命名
git branch -m master
6、最后，强制更新存储库。
git push -f origin master

小技巧
将如下代码保存在一个bat文件里，然后双击运行即可。

git checkout --orphan latest_branch
git add -A
git commit -am "清除所有历史版本以减少仓库大小，请重新从远程拷贝此仓库"
git branch -D master
git branch -m master
git push -f origin master

###方法二
不推荐使用，可能导致git存储库出现问题。思路：直接删除.git文件再初始化仓库

1. 先删除.git文件夹
2. 然后初始化Git（user为你的用户名，repo为你的仓库名）
   git init git remote add origin git@github.com:user/repo
3. 提交当前版本的代码：
   git add * git commit -am 'message'
   最后，强制更新到GitHub：git push -f origin master

##四、git branch 和 git checkout

　　1.Git branch

　　　　一般用于分支的操作，比如创建分支，查看分支等等，

　　　　1.1 git branch

　　　　　　不带参数：列出本地已经存在的分支，并且在当前分支的前面用"*"标记

　　　　1.2 git branch -r

　　　　　　查看远程版本库分支列表

　　　　1.3 git branch -a

　　　　　　查看所有分支列表，包括本地和远程

　　　　1.4 git branch dev

　　　　　　创建名为dev的分支，创建分支时需要是最新的环境，创建分支但依然停留在当前分支

　　　　1.5 git branch -d dev

　　　　　　删除dev分支，如果在分支中有一些未merge的提交，那么会删除分支失败，此时可以使用 git branch -D dev：强制删除dev分支，

　　　　1.6 git branch -vv 

　　　　　　可以查看本地分支对应的远程分支

　　　　1.7 git branch -m oldName newName

　　　　　　给分支重命名

　　2. Git checkout


　　　　2.1 操作文件

　　　　　　2.1.1 git checkout filename 放弃单个文件的修改

　　　　　　2.1.2 git checkout . 放弃当前目录下的修改

　　　　2.2 操作分支

　　　　　　2.2.1 git checkout master 将分支切换到master

　　　　　　2.2.2 git checkout -b master 如果分支存在则只切换分支，若不存在则创建并切换到master分支，repo start是对git checkout -b这个命令的封装，将所有仓库的分支都切换到master，master是分支名，

　　　　2.3 查看帮助

　　　　　　git checkout --help

　　　　　　当然git checkout还有许多命令，但这些已经能满足我们日常开发所需

##五、rebase

什么是 rebase?
git rebase 你其实可以把它理解成是“重新设置基线”，将你的当前分支重新设置开始点。这个时候才能知道你当前分支于你需要比较的分支之间的差异。
原理很简单：rebase需要基于一个分支来设置你当前的分支的基线，这基线就是当前分支的开始时间轴向后移动到最新的跟踪分支的最后面，这样你的当前分支就是最新的跟踪分支。这里的操作是基于文件事务处理的，所以你不用怕中间失败会影响文件的一致性。在中间的过程中你可以随时取消rebase 事务。
官方解释:  https://git-scm.com/book/zh/v2/Git-分支-变基
git rebase 和 git merge 有啥区别？
rebase会把你当前分支的 commit 放到公共分支的最后面,所以叫变基。就好像你从公共分支又重新拉出来这个分支一样。
举例:如果你从 master 拉了个feature分支出来,然后你提交了几个 commit,这个时候刚好有人把他开发的东西合并到 master 了,这个时候 master 就比你拉分支的时候多了几个 commit,如果这个时候你 rebase master 的话，就会把你当前的几个 commit，放到那个人 commit 的后面。




rebase

merge 会把公共分支和你当前的commit 合并在一起，形成一个新的 commit 提交





merge

注意:

不要在公共分支使用rebase
本地和远端对应同一条分支,优先使用rebase,而不是merge

抛出问题:
为什么不要再公共分支使用rebase?
因为往后放的这些 commit 都是新的,这样其他从这个公共分支拉出去的人，都需要再 rebase,相当于你 rebase 东西进来，就都是新的 commit 了

1-2-3 是现在的分支状态
这个时候从原来的master ,checkout出来一个prod分支
然后master提交了4.5，prod提交了6.7
这个时候master分支状态就是1-2-3-4-5，prod状态变成1-2-3-6-7
如果在prod上用rebase master ,prod分支状态就成了1-2-3-4-5-6-7
如果是merge
1-2-3-6-7-8
........ |4-5|
会出来一个8，这个8的提交就是把4-5合进来的提交

merge和rebase实际上只是用的场景不一样
更通俗的解释一波.
比如rebase,你自己开发分支一直在做,然后某一天，你想把主线的修改合到你的分支上,做一次集成,这种情况就用rebase比较好.把你的提交都放在主线修改的头上
如果用merge，脑袋上顶着一笔merge的8,你如果想回退你分支上的某个提交就很麻烦,还有一个重要的问题,rebase的话,本来我的分支是从3拉出来的,rebase完了之后,就不知道我当时是从哪儿拉出来的我的开发分支
同样的,如果你在主分支上用rebase, rebase其他分支的修改,是不是要是别人想看主分支上有什么历史,他看到的就不是完整的历史课,这个历史已经被你篡改了
常用指令

git rebase -I dev 可以将dev分支合并到当前分支
这里的”-i“是指交互模式。就是说你可以干预rebase这个事务的过程，包括设置commit message，暂停commit等等。
git rebase –abort 放弃一次合并
合并多次commit操作:
1 git rebase -i dev
2 修改最后几次commit记录中的pick 为squash
3 保存退出,弹出修改文件,修改commit记录再次保存退出(删除多余的change-id 只保留一个)
4 git add .
5 git rebase --continue

