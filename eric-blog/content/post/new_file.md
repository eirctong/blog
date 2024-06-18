+++
title = 'New_file'
date = 2024-06-16T14:04:10+08:00
keywords = ["blog", "brief"]
cover = "blog"
summary = "this is for brief blog test"
tags = ["blog", "test"]
pin = true
draft = false
+++


这是一个摘要，并且会出现在文章中123123
<!--more-->


Git
变更集
”git add”命令就是用来操作变更集的，当存在多个变更时，我们可以利用”git add”命令，选择将哪些变更加入到本次提交的变更集合中，也就是说，并不是每次提交都要将所有的变更都提交，而是可以有选择性的，只有被加入到变更集中的变更才会被提交， 只不过，上例中的”git add -A”命令并没有进行选择，而是将所有变更作为了一个变更集合，当”git add”命令创建出这个变更集以后，”git commit”命令将这个变更集合提交到了git仓库中。
核心
git只会对修改的部分创建副本，而不会对整个目录创建副本
git处理文件的逻辑：git会将我们的文件和目录转化成一种叫做”git对象”的东西，然后再对这些”git对象”进行管理，从而实现版本管理的目的，这些git对象存放在git的对象库中
我们眼中的文件会被git转化成”块”(blob)
我们眼中的目录会被git转化成”树”(tree)
我们眼中的状态会被git转化成”提交”(commit)
blob、tree、commit都是git对象，是三种不同类型的git对象

- 一个commit就是一个我们所创建的提交，它指向了一个tree，这个tree保存了某一时刻项目根目录中的直接文件信息和直接目录信息，也就是说，
- tree会指向直接文件的blob对象，并且指向直接子目录的tree对象，子目录的tree对象又指向了子目录中直接文件的blob，以及子目录的直接子目录的tree，依此类推。

修改f2的内容，创建一个直接目录，第二次提交，git对象的指向如下所示

这样做的优点：
- 手动创建副本会造成磁盘空间的浪费，即两个副本的差异只有1k时，也需要牺牲整个文件的大小；而git的管理就是只修改改动的部分，如上图，只有file2发生了变化，则创建新的blob对象，而原先的file1对应的blob对象的指向是没有改变的
- 通过引用的方式指向没有改变的file，也可以理解为复用（multiplex）
总结：
一个commit就代表项目的一个状态（相当于手动创建的副本），一个commit背后是一堆git对象，git将这些git对象巧妙的组织在了一起，从而实现了版本管理的目的。
Git区域
”.git”目录就是所谓的”版本库”
除了”.git”目录以外的其他文件和目录组成了”工作区”

版本库的提交
$ git add -A
$ git commit -m "some comment"

回退
git reflog 查询每次提交时的commit_id
git reset --hard commit_id 进行回退
git reflog 检查是否回退成功





HEAD
HEAD指针 ——–> 分支指针 ——–> 最新提交
通常情况下，HEAD指针总是指向了当前分支的最新提交（通过分支指针间接的指向）

git log --oneline --all --graph
用于检查所有的分支的指针，以及当前head所指向的commit

git checkout 37e7e8d
用于根据上一条命令得出的hash值来检出到之前的status

6BFPLX2-XVK+Admin@6BFPLX2-XVK MINGW64 /d/workspace/git/git_test ((9c3083d...))
$ git log --oneline --all --graph
* 0f9ba9a (master) fourth change
* 9c3083d (HEAD) third change
* 37e7e8d second change
* 4dc04b4 First snapshot

差异对比


工作区与暂存区区别：
$ git diff    所有对比
$ git diff -- test1 指定对比

工作区和提交区别：
$ git diff HEAD


Test

将本地存在的git仓库推到远程仓库
Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin git@10.92.4.42:tongyichen/netdevops_auto.git
git push -u origin --all
git push -u origin --tags

将本地仓库提交的内容上传到远程仓库 （常用）
cd existing_folder
git init
git remote add origin git@10.92.4.42:tongyichen/testgit.git
git add .
git commit -m "automate commit"
git push -u origin master

