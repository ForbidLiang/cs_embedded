# git入门使用

>auther：forbid  
data：2020  
version：1.0  
附加说明：该文章的内容很多来自网络上的资料，这个不用于商业用途，如有侵权等问题请联系本人。

<!-- TOC -->

- [git入门使用](#git入门使用)
  - [下载安装：](#下载安装)
  - [基本概念](#基本概念)
    - [工作区和暂存区](#工作区和暂存区)
    - [git管理](#git管理)
  - [本地使用](#本地使用)
    - [git配置：](#git配置)
    - [初始化git](#初始化git)
    - [添加与提交](#添加与提交)
    - [**查看状态**](#查看状态)
    - [删除文件](#删除文件)
  - [关于branch](#关于branch)
    - [查看当前分支](#查看当前分支)
    - [创建分支](#创建分支)
    - [切换分支](#切换分支)
    - [合并分支](#合并分支)
    - [删除分支](#删除分支)
    - [解决冲突](#解决冲突)
    - [分支管理策略](#分支管理策略)
    - [bug分支](#bug分支)
  - [关于版本](#关于版本)
    - [查看提交日志](#查看提交日志)
    - [版本回退](#版本回退)
    - [版本前进](#版本前进)
  - [结合远端使用](#结合远端使用)
    - [ssh与https](#ssh与https)
    - [连接上你远端的git仓库](#连接上你远端的git仓库)
    - [本地的仓库与远端的连接](#本地的仓库与远端的连接)
    - [提交到远端的库](#提交到远端的库)
    - [克隆远端的仓库](#克隆远端的仓库)
    - [查看远端库的信息](#查看远端库的信息)
  - [常见问题](#常见问题)
    - [错误1](#错误1)
    - [错误2](#错误2)
  - [resources](#resources)

<!-- /TOC -->



## 下载安装：

[官网](https://git-scm.com/downloads)

win：在官网上下载安装



## 基本概念

### 工作区和暂存区

工作区:  就是你电脑看到的目录

暂存区: `git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。



### git管理

git管理的“修改” ， 而不是文件。



## 本地使用



### git配置：



查看配置信息

```
git config -l
```



```
$ git config --global user.name "your Name"
$ git config --global user.email "your email"

sample:
$ git config --global user.name xaioming
$ git config --global user.email 123@qq.com
```





### 初始化git

当你把你的电脑文件设置为仓库时， 需要将其初始化



在git中进入文件目录,使用

```
git init
```

即可（初始化）将其设置为仓库





### 添加与提交

**添加**

```
git add  "filename"		//逐个添加文件
git add -A  			//添加当前目录的所有文件
git add .				//添加当前目录中所有文件更改
```



**提交**

```
git commit -m "提交说明"  //提交暂存的文件
//如果没有"提交说明",那么不用-m

git commit filename -m 'commit message'		//添加文件并提交一次
```



### **查看状态**

这个可以查看当前仓库的状态

```
git status
```



查看日志

```
git log

git log --graph  	 	//用git log --graph命令可以看到分支合并图
```





为什么会有**添加**和**提交**呢?

因为.......





### 删除文件

加入你删除文件

一：你真的要删除

```
git rm "filename" 		//从改版本中删除

sample：git rm  哈哈.txt
```



二：不小心删除了, 可以将文件恢复

```
git checkout -- "filename"  


sample: git checkout -- 哈哈.txt
```







## 关于branch







### 查看当前分支

```
git branch
```



### 创建分支

```
git branch "branch-name"

git checkout -b branch-name  origin/branch-name    //创建远程origin的dev分支到本地
```



### 切换分支

```
git checkout "branch-name"
git checkout -b branch-name  origin/branch-name    //创建远程origin的dev分支到本地


or

(推荐使用这个)
git switch -c "branch-name"		//切换分支
git switch master 				//直接切换到master分支
```



### 合并分支

```
git merge "branch-name"
//git merge命令用于合并指定分支到当前分支
```



### 删除分支

```
git branch -d "branch-name"


git branch -d "branch-name"   //强制删除分支
```





### 解决冲突

你和小明协作开发,大家都有一个分支

你突然发现, 小明他将他自己的分支合并上去了,

你内容可能和他有冲突,那你怎么办?



就是master分支和你的分支有冲突了!



先试下,将分支合并到master,如果有冲突会失败

有冲突的

* 使用git status 查看哪里有冲突, 然后手动修改(在master分支修改)
* commit你的master



### 分支管理策略

合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

```
git merge --no-ff -m "merge with no-ff"  branch-name
```



### bug分支

假如你现在在这个分支工作,但是还没有做完, 所以你还有提交,   同时需要你临时修改个bug(开个bug分支)



Git提供了一个`stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

```
git stash
```

现在，用`git status`查看工作区，就是干净的, 因此可以放心地创建分支来修复bug。



bug修复完了,接着回到原来的分支干活了



```
git stash list			//查看stash
```

恢复原来的工作现场

```
git stash apply			//恢复stash
git stash drop			//删除stash


git stash pop			//恢复的同时把stash内容也删了
```



但是还有个问题

你的bug在master修复了,但是你的分支还有这个bug

git专门提供了一个`cherry-pick`命令，让我们能复制一个特定的提交到当前分支

```
git cherry-pick "commit的id号"
```



多人协作

```
git checkout -b branch-name  origin/branch-name    //创建远程origin的dev分支到本地
```

你的小伙伴基于你的分支进行开发提交,   然后最新提交和你试图推送的提交有冲突,怎么办?

先用`git pull`把最新的提交从`origin/dev`抓下来



如果pull失败，原因是没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接

```
git branch --set-upstream-to=origin/branch-name  branch-name
```





> 多人协作的工作模式通常是这样：
>
> 1. 首先，可以试图用`git push origin `推送自己的修改；
> 2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
> 3. 如果合并有冲突，则解决冲突，并在本地提交；
> 4. 没有冲突或者解决掉冲突后，再用`git push origin `推送就能成功！
>
> 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to  origin/`。



## 关于版本

你commit一次,那么就是一个版本,所以你可以不用总是commit

> 就像游戏通关, 你commit就是保存游戏, 所以当然是重要的才保存,比如说你打通这一关了,或是这次玩的进度很多了

所以commit时, commit的提交说明就其实蛮有必要的, 不然都不知道,你为什么这次commit了什么, 想回退版本都不明不白的





### 查看提交日志

(查看你保存的游戏进度)

```
git log		//这个显示最近到最远提交的日志

git log --pretty=oneline		//这个可以精简显示
```





### 版本回退

回到当初的游戏进度



```
git reset --hard "版本号(commit的id)"

//sample:  git reset --hard 1078sa
//这个版本号(commit的id)可以通过log查看的得知
//这个id很长,只需要填写前面几位就可以了
//head,就像指针,把头指向你当前的

```





### 版本前进

如果你回退了版本,但是你想回到之前的版本怎么办? 这时候你就需要的知道你之前的版本号,可是log只会记载你当前和之前的版本



使用命令,记录了你的每一次命令

```
git reflog
```







## 结合远端使用

连接你远端的仓库, 这里以使用SSH方式为例(因为ssh协议比较快)



### ssh与https



### 连接上你远端的git仓库

以GitHub为例



1.生成秘钥

```
ssh-keygen -t rsa -C "email"

sample: ssh-keygen -t rsa -C  123@qq.com
```

一路回车，使用默认值即可，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥



2.在你的GitHub账户中添加公钥



为什么使用SHH key?

> 因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的.
>
> 
>
> (GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。)





### 本地的仓库与远端的连接



```
sample:  git remote add origin git@github.com:你的账户名/远端仓库名字.git

//远程库的名字就是origin，这是Git默认的叫法，也可以改成别的
```



### 提交到远端的库

```
git push -u origin master   //由于远程库是空的，我们第一次推送master分支时，加上了-u参数

git push origin master   //推送到远端的仓库

git push origin "branch-name"   //可以推送你其他的分支上去
```



### 克隆远端的仓库

```
git clone git@github.com:账户名/远端仓库名字.git
```



### 查看远端库的信息

```
 git remote
 
 git remote -v		//显示更详细的信息
```





## 常见问题



### 错误1



出现错误：Permission denied (public key) 





你提交或克隆时出现错误



* 先测试下和你github账户的连接

  ```
  ssh -v git@github.com    //使用这个测试
  
  或(建议用第一个)
  
  ssh -T git@github.com 
  ```

  

* 假如连接失败,那么说明(你的github账户上的秘钥  和  你本地的秘钥内容或秘钥文件位置不符)

  (懒得去找了,直接新建个秘钥吧)



* 新建秘钥

  ```
  cat  路径   //使用这个查看你秘钥的内容,是看公钥的内容
  ```

  

* 最后把新的秘钥放在github上吧,一般没问题了吧.....





### 错误2

错误提示

```
fatal: The remote end hung up unexpectedly
```



可能造成的原因

因为上传代码是中端，导致缓存区堆放有文件，下次上传是缓存区就不够大了，所以可以扩大缓存区和回收垃圾，建议回收垃圾。





解决：

1.缓冲区设置

```
git config http.postBuffer 524288000
```



2.垃圾回收修复

```
git gc --aggressive
```







## resources

[廖雪峰老师git](https://www.liaoxuefeng.com/wiki/896043488029600)
[.gitignore 文件](https://www.liaoxuefeng.com/wiki/896043488029600/900004590234208)

tool：  
[git](https://git-scm.com/)
[source tree](https://www.sourcetreeapp.com/)
[码云](https://gitee.com/)
[giihub]()
[github desktop]()

[how to use source tree](https://www.jianshu.com/p/8a3988057d0f)
    