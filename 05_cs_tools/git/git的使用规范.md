git 的使用规范
-------------

>auther：forbid  
data：2020/10/29   
version：1.0  
附加说明：该文章的内容很多来自网络上的资料，这个不用于商业用途，如有侵权等问题请联系本人。

<!-- TOC -->

- [仓库目录与文件](#仓库目录与文件)
  - [仓库目录](#仓库目录)
  - [文件名字](#文件名字)
- [README内容](#readme内容)
- [commint](#commint)
  - [提交规则](#提交规则)
    - [header](#header)
    - [body：针对本次commint的详细描述，可以分成多行。](#body针对本次commint的详细描述可以分成多行)
    - [footer](#footer)
  - [Revert撤销commint](#revert撤销commint)
  - [分支](#分支)
  - [参考资料](#参考资料)

<!-- /TOC -->


# 仓库目录与文件

## 仓库目录

- README.md：每个项目必须包含一个README.md文件。  
- src：源码文件。  
- doc：存放详细的API文档。  
- dist：项目输出目录,所有编译生成，提供给用户使用的文件。  
- build：所有工具类的脚本应当放在此目录。  
- test：所有测试相关的代码应当放在此目录。  


## 文件名字

- 小写
- 某些说明文件名大写（README）
- 使用英文，半角
- 多单词时使用连线（-）分隔

# README内容

结构：软件手册是一部完整的书，建议采用下面的结构。  
- 简介（Introduction）： [必备] [文件] 提供对产品和文档本身的**总体的、扼要的**说明。
  
- 快速上手（Getting Started）：[可选] [文件] 如何最快速地使用产品。  

- 入门篇（Basics）： [**必备**] [目录] 又称”使用篇“，提供初级的使用教程。  
    - 环境准备（Prerequisite）：[必备] [文件] 软件使用需要满足的前置条件。  
    - 安装（Installation）：[可选] [文件] 软件的安装方法。
    - 设置（Configuration）：[必备] [文件] 软件的设置。


- 进阶篇（Advanced)：[可选] [目录] 又称”开发篇“，提供中高级的开发教程

- API（Reference）：[可选] [目录|文件] 软件 API 的逐一介绍

- FAQ：[可选] [文件] 常见问题解答

- 附录（Appendix）：[可选] [目录] 不属于教程本身、但对阅读教程有帮助的内容
  - Glossary：[可选] [文件] 名词解释
  - Recipes：[可选] [文件] 最佳实践
  - Troubleshooting：[可选] [文件] 故障处理
  - ChangeLog：[可选] [文件] 版本说明
  - Feedback：[可选] [文件] 反馈方式



# commint

## 提交规则
每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。
```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
其中，Header 是必需的，Body 和 Footer 可以省略。
不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

### header

- type:用于说明 commit 的类别，只允许使用下面7个标识。
  > feat：新功能（feature）  
fix：修补bug  
docs：文档（documentation）  
style： 格式（不影响代码运行的变动）  
refactor：重构（即不是新增功能，也不是修改bug的代码变动）  
test：增加测试  
chore：构建过程或辅助工具的变动  
- scope：scope用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。
- subject：试commint目的的简短描述（不超过30字符）。  
    - 以动词开头，使用第一人称现在时，比如change而不是changed或changes。  
    - 第一个字母小写。  
    - 结尾不加句号。
- subject

### body：针对本次commint的详细描述，可以分成多行。  
注意点：  
1. 使用第一人称。
2. 说明代码变动的动机，以及与以前的行为的对比。

### footer
- 不兼容变动
- 关闭issue


## Revert撤销commint



## 分支
- master 分支

    - 主分支，永远处于**稳定状态**，对应当前线上版本
    - 以 **tag 标记一个版本**，因此在 master 分支上看到的每一个 tag 都应该对应一个线上版本
    - **不允许在该分支直接提交代码**

- develop 分支

    - 开发分支，包含了项目最新的功能和代码，所有开发都依赖 develop 分支进行

    - **小的改动**可以直接在 develop 分支进行，改动**较多时**切出新的 feature 分支进行

    >注： 更好的做法是 develop 分支作为开发的主分支，也不允许直接提交代码。小改动也应该以 feature 分支提 merge request 合并，目的是保证每个改动都经过了强制代码 review，降低代码风险

- feature 分支

    - 功能分支，开发**新功能的分支**
    - 开发新的功能或者改动较大的调整，从 develop 分支切换出 feature 分支，分支名称为 feature/xxx
    - 开发完成后**合并回 develop 分支**并且删除该 feature/xxx 分支

- release 分支

    - 发布分支，新功能合并到 develop 分支，准备发布新版本时使用的分支
    - 当 develop 分支完成功能合并和部分 bug fix，**准备发布新版本时，切出一个 release 分支，来做发布前的准备**，分支名约定为release/xxx
    - 发布之前发现的 bug 就直接在这个分支上修复，确定准备发版本就合并到 master 分支，完成发布，同时合并到 develop 分支

- hotfix 分支

    - 紧急修复线上 bug 分支
    - 当线上版本出现 bug 时，从 master 分支切出一个 hotfix/xxx 分支，完成 bug 修复，然后将 hotfix/xxx 合并到 master 和 develop 分支(如果此时存在 release 分支，则应该合并到 release 分支)，合并完成后删除该 hotfix/xxx 分支

以上就是在项目中应该出现的分支以及每个分支功能的说明。 其中稳定长期存在的分支只有 master 和 develop 分支，别的分支在完成对应的使命之后都会合并到这两个分支然后被删除。简单总结如下：

- master 分支: 线上稳定版本分支
- develop 分支: 开发分支，衍生出 feature 分支和 release 分支
- release 分支: 发布分支，准备待发布版本的分支，存在多个，版本发布之后删除
- feature 分支: 功能分支，完成特定功能开发的分支，存在多个，功能合并之后删除
- hotfix 分支: 紧急热修复分支，存在多个，紧急版本发布之后删除



## 参考资料
- [git官方文档](https://docs.github.com/cn/free-pro-team@latest/github/writing-on-github/basic-writing-and-formatting-syntax)  
- [Commit message 和 Change log 编写指南阮一峰](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
- [web1（关于分支）](https://jaeger.itscoder.com/dev/2018/09/12/using-git-in-project.html)