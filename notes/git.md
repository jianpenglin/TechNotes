# Git教程

<!-- GFM-TOC -->
* [一、Git介绍](#Git介绍)
* [二、git安装连接github](#git安装连接github)
* [三、问题解决](#问题解决)
* [四、Git常用命令](#Git常用命令)
<!-- GFM-TOC -->

## Git介绍

1. svn是集中式，git是分布式
2. github会保存本地git的所有操作记录

## git安装连接github

1. 填写新仓库名称，备注信息。点击创建即可完成
2. 在用户注册主目录(c:\Users\Administrator)下，打开Git Bash,输入命令
```shell
$ cd ~/
$ ssh-keygen -t rsa -C "fff.ff.com" //123是注册Github的邮箱，直接回车
```
3. 接下来到GitHub上，打开“Account settings”--“SSH Keys”页面，然后点击“Add SSH Key”，填上Title，在Key文本框里粘贴 id_rsa.pub文件里的全部内容
4. 验证是否成功，在git bash里输入下面的命令
```shell
$ ssh -T git@github.com
```
如果初次设置的话，会出现界面，输入yes 同意即可
5. 开始设置username和email，因为github每次commit都会记录他们
```shell
$ git config --global user.name "name"//你的GitHub登陆名
$ git config --global user.email "123@123.com"//你的GitHub注册邮箱
```
6. 在本地硬盘比如G盘 创建TechNotes目录
7. 进入G:\TechNotes，右键鼠标弹出菜单，选择Git Bash Here
8. 初始化
```shell
$ git init
```
9.  关联一个远程库命令
```shell
$ git remote add origin git@github.com:myname/example.git //关联一个远程库命令，
git@github.com:myname/example.git 这个是自己远程库
```
10.   从服务器拉取工程
```shell
$ git pull origin master
```
11. 推送master分支
```shell
$ git push -u origin master //关联后,第一次推送master分支的所有内容命令，此后，每次本地提交后，
就可以使用命令git push origin master推送最新修改
```

## 问题解决

- 如果输入$ git remote add origin git@github.com:fff（github帐号名）/demo（项目名）.git

    提示出错信息：fatal: remote origin already exists.

    解决办法如下：

    1、先输入$ git remote rm origin

    2、再输入$ git remote add origin git@github.com:fff/demo.git 就不会报错了！

    3、如果输入$ git remote rm origin 还是报错的话，error: Could not remove config section 'remote.origin'. 我们需要修改gitconfig文件的内容

    4、找到你的github的安装路径

    5、找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！

    如果输入$ ssh -T git@github.com
    出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。

    解决办法如下：

    1、先输入$ ssh-agent，再输入$ ssh-add ~/.ssh/id_key，这样就可以了。

    2、如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。

    3、最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。
    如果输入$ git push origin master

    提示出错信息：error:failed to push som refs to .......

    解决办法如下：

    1、先输入$ git pull origin master //先把远程服务器github上面的文件拉下来

    2、再输入$ git push origin master

    3、如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git repository以及fatal: Could not read from remote repository.

    4、则需要重新输入$ git remote add origin git@github.com:jianpenglin/demo.git


- 使用git在本地创建一个项目的过程
```shell
    $ makdir ~/demo    //创建一个项目demo
    $ cd ~/demo       //打开这个项目  
    $ git init             //初始化  
    $ touch README  
    $ git add README        //更新README文件  
    $ git commit -m 'first commit'     //提交更新，并注释信息“first commit”  
    $ git remote add origin git@github.com:fff/demo.git     //连接远程github项目  
    $ git push -u origin master     //将本地项目更新到github项目上去
```

gitconfig配置文件  
        Git有一个工具被称为git config，它允许你获得和设置配置变量；这些变量可以控制Git的外观和操作的各个方面。这些变量可以被存储在三个不同的位置：
        1./etc/gitconfig 文件：包含了适用于系统所有用户和所有库的值。如果你传递参数选项’--system’ 给 git config，它将明确的读和写这个文件。
        2.~/.gitconfig 文件 ：具体到你的用户。你可以通过传递--global 选项使Git 读或写这个特定的文件。
        3.位于git目录的config文件 (也就是 .git/config) ：无论你当前在用的库是什么，特定指向该单一的库。每个级别重写前一个级别的值。因此，在.git/config中的值覆盖了在/etc/gitconfig中的同一个值。
    在Windows系统中，Git在$HOME目录中查找.gitconfig文件（对大多数人来说，位于C:\Documents and Settings\$USER下）。它也会查找/etc/gitconfig，尽管它是相对于Msys 根目录的。这可能是你在Windows中运行安装程序时决定安装Git的任何地方。

2.3 检查你的设置(Checking Your Settings)
```shell
$ git config --list
```
你也可以查看Git认为的一个特定的关键字目前的值，使用如下命令 git config {key}:

```shell
$ git config user.name
```

例如，你可以运行如下命令获取对config命令的手册页帮助:
```shell
$ git help config
```
- nothing added to commit but untracked files present
  这是git没有把提交的文件加载进来，但是把需要提交的文件都列出来了，只需要用git add XXX(文件名) 把需要提交的文件加上 ，然后git commit -m "xx",再git push -u origin master重新提交就可以了
- git commit 失败"Untracked files,Changes not staged for commit" 问题的解决  
也就是说，这个文件在commit之前需要先把文件放入暂存区。只需要在commit之前add一下文件即可。  
```shell
$ git add FFF.txt   //或者 $ git add -A  
```
然后再commit一下就没有问题了。  

## Git常用命令

| 命令 | 说明 |
| -------- | ---------------------- |
| mkdir         XX    | (创建一个空目录 XX指目录名) |
|   pwd               |显示当前目录的路径。|
|   git init          |把当前的目录变成可以管理的git仓库，生成隐藏.git文件。|
|   git add XX        |把xx文件添加到暂存区去。|
|   git commit -m "XX"  |提交文件 –m 后面的是注释。|
|   git status        |查看仓库状态|
|   git diff  XX      |查看XX文件修改了那些内容|
|   git log           |查看历史记录|
|   git reset  --hard HEAD^  |或者git reset  --hard HEAD~ 回退到上一个版本(如果想往回退10个版本，使用git reset --hard HEAD~10)或者回退到指定版本git reset  --hard (commitid)|
|   cat XX            |查看XX文件内容|
|   git reflog        |查看历史记录的版本号id|
|   git checkout -- XX  |把XX文件在工作区的修改全部撤销。|
|   git rm XX          |删除XX文件|
|   git remote add origin https://github.com/ff/testgit.git   |关联一个远程库|
|   git push -u(第一次要用-u 以后不需要) origin master   |把当前master分支推送到远程库|
|   git clone https://github.com/ff/testgit.git    |从远程库中克隆|
|   git checkout -b dev  |创建dev分支 并切换到dev分支上|
|   git branch           |查看当前所有的分支|
|   git checkout master  |切换回master分支|
|   git merge dev        |在当前的分支上合并dev分支|
|   git branch -d dev    |删除dev分支|
|   git branch name      |创建分支|
|   git stash            |把当前的工作隐藏起来 等以后恢复现场后继续工作|
|   git stash list       |查看所有被隐藏的文件列表|
|   git stash apply      |恢复被隐藏的文件，但是内容不删除|
|   git stash drop       |删除文件|
|   git stash pop        |恢复文件的同时 也删除文件|
|   git remote           |查看远程库的信息|
|   git remote -v        |查看远程库的详细信息|
|   git push origin master  |Git会把master分支推送到远程库对应的远程分支上|
