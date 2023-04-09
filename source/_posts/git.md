---
title: git
date: 2023-04-08 23:21:45
tags:
categories: 编程语言及工具
---

# git

## git的安装
### Windows
有一个我觉得非常详细的教程，就贴在这里：
[git安装详细教程（CSDN）](https://blog.csdn.net/qq_52102933/article/details/120387246?ops_request_misc=&request_id=&biz_id=102&utm_term=Windows%E5%AE%89%E8%A3%85%E4%BD%BF%E7%94%A8git&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-3-120387246.142^v82^insert_down38,201^v4^add_ask,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)
按照上面的教程一步一步来安装，基本上是没有问题的。

### Mac
暂时先晾在这，后面再整理

## Git的工作流程
- 克隆 Git 资源作为工作目录。
- 在克隆的资源上添加或修改文件。
- 如果其他人修改了，你可以更新资源。
- 在提交前查看修改。
- 提交修改。
- 在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。


## Git基本操作
Git的作用是什么？**Git 的工作就是创建和保存你项目的快照及与之后的快照进行对比。**

常用的命令有以下六个命令：
- git clone
- git push
- git add
- git commit
- git checkout
- git pull

## Git创建仓库
初始化一个仓库的命令：
- 如果使用当前目录作为Git仓库，使用以下命令：
```shell
    git init
```
- 如果使用指定目录作为git仓库，使用以下命令：
```shell
    git init newrepo

    newrepo是指定目录的路径
```
初始化后，会在newrepo下生成 **.git**的目录，**这个目录存放着所有Git需要的数据和资源**。如果在当前目录中，有几个文件是需要纳入Git当中的话，需要先用git add命令告诉 Git 开始对这些文件进行跟踪，然后再进行提交。

*****

创建仓库可以在空目录下，也可以在非空目录下。**非空目录**下，使用**git add**命令将仓库下的所有文件放入Git中，进行提交即可；**空目录**下，要么就是自己添加文件，让仓库“不空”，要么就是将别的仓库复制下来放进该仓库中，这就叫做克隆。

克隆仓库的命令：
```
    git clone <repo>

    <repo> 是仓库的http地址
```
上面这条克隆命令，是将 **repo**地址下的仓库克隆到了当前目录。

将仓库克隆到指定目录下的命令：
```
    git clone <repo> <directory>

    <repo>是仓库的http地址
    <directory>是本地目录
```

执行了克隆命令后，会在当前目录下创建一个**以克隆的仓库名为文件名的新目录**，新目录下包含一个 **.git**文件，这里的 **.git**文件用于保存下载下来的所有版本记录。


如果想要自己定义新目录的名称，可以输入以下命令：
```
     git clone <repo> 自定义名
```

*****

做完上述的操作之后，就已经可以对远程仓库进行编辑了。不过，这里的编辑只是对克隆至本地的远程仓库进行编辑，如果想要让远程仓库也发生修改的话，就需要将修改过的本地文件回传。这个回传需要我们进行一些配置。

git的配置的命令：
```shell
    git config
```

**编辑git的配置文件**
**只针对当前仓库**
```shell
    git config -e  
```

**针对本地上的所有仓库**
```shell
    git config -e -global
```

**设置提交代码时的用户信息：**
```shell
    git config -global user.name "username"
    git config -global user.email user@useremail.com 
    # 注意这里的-global去掉的话，命令只会对当前仓库有效
```

## Git分支管理
有一张图可以说明Git分支管理的模式
![git分支管理](https://static.runoob.com/images/svg/git-brance.svg)

使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

**创建分支的命令**
```shell
    git branch (branchname)
```

**切换分支的命令**
```shell
    git checkout (branchname)
```
这里还有一种情况：需要创建一个新分支的同时切换到新分支下，执行以下命令：
```
    git checkout -b (branchname)
```
*****
这里会有一个问题：在进行切换分支时，Git会将该分支最后提交的快照来替换你工作目录的内容，所以说多个分支不需要多个目录

**合并分支的命令：**
```shell
    git merge
```

**删除分支的命令：**
```shell
    git checkout -d (branchname)
```

## Git查看提交历史
**常用的一般有两个命令：**
- git log ---查看历史提交记录 
- git blame < blame> ---以列表形式查看指定文件的历史修改记录

**git log**
**查看历史记录的简洁的版本**
```shell
    git log -oneline
```

**查看历史中什么时候出现了分支、合并**
```shell
     git log -graph -oneline
```

**逆向显示所有日志**
```shell
    git log -reverse -oneline
```

**查找指定用户的提交日志**
```shell
    git log -author=name -oneline
```

**指定日期，可以执行几个选项：--since 和 --before，也可以用 --until 和 --after**

```shell
    git log -oneline -before={2.weeks.ago} -after={2021-04-09} 
```

**还有很多git log命令，可以进入这个网站进行查询：**[Git log命令](https://git-scm.com/docs/git-log)

*****

**git blame**
作用是：**查看指定文件的修改记录**


## Git标签
创建一个带注解的标签
```shell
    git tag -a v1.1
```

查看所有标签
```shell
    git tag
```

指定标签信息命令：
```shell
    git tag -a <tagname> -m "标签内容"
```

PGP签名标签命令：
```shell
    git tag -s <tagname> -m "标签内容"
```

## Git 和 Github

上面的Git命令都是在本地执行，有些时候，我们需要将自己的代码分享给其他人或者和别人一起开发，那么这个时候，我们就需要将代码放入一个大家或者双方都可以访问的地方，比如说Github，Gitee。
![Github](https://www.runoob.com/wp-content/uploads/2015/03/Git-push-command.jpeg)

**这里将Github作为远程仓库，记录用Git连接Github的过程**

***未完待续***

