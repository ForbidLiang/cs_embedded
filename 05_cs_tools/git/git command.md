# git command 


>auther：forbid  
data：2020  
version：0.1 
附加说明：该文章的内容很多来自网络上的资料，这个不用于商业用途，如有侵权等问题请联系本人。

<!-- TOC -->

- [git command](#git-command)
  - [版本控制：](#版本控制)
  - [分支管理](#分支管理)
  - [远程仓库](#远程仓库)
  - [对本地库文件操作](#对本地库文件操作)
  - [创建版本库](#创建版本库)

<!-- /TOC -->

## 版本控制：


| 版本控制 |      |
| -------- | ---- |
| git  tag -d 版本号 | 删除标签|
| git push origin --tags  | 推多个标签|
| git push origin 版本号 | 推送版本到远端|
| git tag -a 版本号） -m “description” | 创建版本|
| git tag | 查看版本号|





## 分支管理

***

| 分支管理  ||
| ---- | ---- |
| git rebase | 整理日志|
|git branch --set-upstream-to=origin/分区名字 分区名字 | 指定本地分支与远端分支的连接|
|  git checkout -b dev origin/分区名字 |  拉去库的某个分支（前提是已经克隆了库）|
| git push origin 分支名字 | 推送分支|
| git brach -d 分支名字-vulcan | 删除分支， -D是强制删除|
| git cherry-pick （提交的名字） |  比如说master做了修改，想也把，分支改了  |
| git stash  pop | 回复的同时删除|
| git stash drop | 删除工作|
| git stash apply |  回复工作区但是不删除stash|
| git stash list | 列出工作区的列表|
| git  stash | 将当前的工作器区存储起来，比如正在一个分支上切换到其他的分支去修改bug|
| git log --graph --pretty=oneline --abbrev-commit | 查看日志通过 图 简介 缩写commit |
| git branch -d （分支名字） | 删除分支|
| git  merge （分支名字） | 合并分支|
| git brach | 查看当前分支|
| git brach （分支名字）| 创建分支|
| git switch -c （分支名字） | 切换分支|
| git switch master | 切换到主分支|
| git checkout （分支名字） |  切换分支|
| git check  -b （分支名字） | 创建和切换分支|





## 远程仓库

| 远程仓库  ||
| ---- | ---- |
| git clone git@github.com:自己的用户名/克隆库的名称..git | 克隆库|
| git remote rm (name) | 删除本地远端库的|
| git remote  | 查看指定远端库的地址|
| git remote | 查看远端的库|
| git push origin master | 非第一次提交|
| git push **-u** origin master | 第一次提交|
| git remote add origin git@github.com:用户名/仓库名.git | 克隆远端的仓库|





## 对本地库文件操作


| 对本地库文件操作  ||
|--| --|
| git rm （filename） | 删除仓库中的文件|
| git checkout --（filename）| 误删文件可以在版本库中将文件（filename）恢复过来|
| git checkout --（filename）| 将文件回退到最近一次修改（无论是在暂存区还是没有添加到暂存区|
| git  reflog | 查看整的命令，git log只是记录“使用中的过程”|
| cat （filename） | 查看文件|
| git reset hard HEAD~（回退到前几次版本） | 回退版本（~也可用^表示,一个^表示一次）|
|  git reset --hard (version) | 回退到哪个版本|
| git log | 查看日志 （简介显示 --pretty=oneline）|
| git diff （filename）| 查看文件更改的内容|
| git diff HEAD --(filename) | 查看工作去与版本库中最新版本的区别|
| git status | 查看现在git的内容，是否有更改这些|





## 创建版本库

| 创建版本库 |  |
|--| --|
| git commit -m “说明内容” |提交文件，如果没说明内容则不用-m|
| git add file | 添加文件|
| git init | 初始化仓库|
| mkdir （filename） | 创建文件|
| rm | 删除文件|