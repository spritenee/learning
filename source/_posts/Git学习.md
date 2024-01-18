---
title: Git学习笔记
abbrlink: 8520
date: 2024-01-02 00:00:00
tags:
lang: zh-CN
cover: https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240118152138155.png
---

# Git学习笔记

### 安装

在 Windows 环境中，最简单快捷的方法是使用 msysGit。

http://msysgit.github.io/

安装过程中，可以设置调用 Git 的环境变量。一般只会用到 msysGit 中附属的 Git Bash 命令提示符，所以请选择最上面的Use Git Bash only，然后进行下一步。

![image-20240101072709809](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202312/image-20240101072709809.png)

![image-20240101072738346](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202312/image-20240101072738346.png)

#### 换行符的处理
在所示的页面中，选择换行符的相关设置。
GitHub 中公开的代码大部分都是以 Mac 或 Linux 中的 LF（Line Feed）换行。然而，由于 Windows 中是以 CRLF（Carriage Return ＋Line Feed）换行的，所以在非对应的编辑器中将不能正常显示。
Git 可以通过设置自动转换这些换行符。使用 Windows 环境的各位，请选择推荐的“Checkout Windows-style, commit Unix-style line endings”选项。换行符在签出时会自动转换为 CRLF，在提交时则会自动转换为LF。

![image-20240101072858375](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202312/image-20240101072858375.png)

#### Git Bash
顺利安装好 msysGit 之后，Git Bash 会作为一个应用程序添加进系统，接下来请启动它。双击之后，会弹出一个名为 Git Bash 的命令提示符，它附属于 msysGit。如果是按照上述介绍的流程进行安装，那么 git 命令就只能在 Git Bash 中使用，在 Windows 附属的命令提示符中则无法运行。

![image-20240101073119720](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202312/image-20240101073119720.png)

从名字中带有 Bash 就不难猜到，Git Bash 中照搬了许多 Bash 命令，习惯 Linux 的人用起来会感觉比 Windows 命令提示符更得心应手。借这个机会，不妨也熟悉一下 Windows 的 CLI（Command Line Interface，命令行界面）操作。

### 初始设置

#### 设置姓名和邮箱地址

首先来设置使用 Git 时的姓名和邮箱地址。名字请用英文输入。

```
$ git config --global user.name "Firstname Lastname"
```

```bash
$ git config --global user.email "your_email@example.com"
```

这个命令，会在“~/.gitconfig”中以如下形式输出设置文件。

```txt
[user]
 name = Firstname Lastname
 email = your_email@example.com
```

想更改这些信息时，可以直接编辑这个设置文件。这里设置的**姓名和邮箱地址**会用在 Git 的**提交日志**中。由于在 GitHub 上公开仓库时，这里的姓名和邮箱地址也会随着提交日志一同被公开，所以请**不要使用不便公开的隐私信息**。
在 GitHub 上公开代码后，前来参考的程序员可能来自世界任何地方，所以请不要使用汉字，尽量用英文进行描述。当然，如果您不想使用真名，完全可以使用网络上的昵称。

#### 提高命令输出的可读性

顺便一提，将 color.ui 设置为 auto 可以让命令的输出拥有更高的可读性。

```
$ git config --global color.ui auto
```

“~/.gitconfig”中会增加下面一行。

```
[color]
 ui = auto
```

这样一来，各种命令的输出就会变得更容易分辨。



## Github

#### 设置头像

只要使用创建 GitHub 账户时注册的邮箱在 [Gravatar](http://cn.gravatar.com/) 上设置头像，GitHub 的头像就会变成您设置好的样子。

#### 设置 SSH Key

运行下面的命令创建 SSH Key。

```bash
$ ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key
(/Users/your_user_directory/.ssh/id_rsa): `按回车键`
Enter passphrase (empty for no passphrase): `输入密码`
Enter same passphrase again: `再次输入密码`
```

密码根据情况输入，不输入一般也可以。一路回车即可。

id_rsa 文件是私有密钥，id_rsa.pub 是公开密钥。

将公钥添加到github设置中，私钥继续默认保存在个人PC上。需要时它们会自动两相验证，完成身份确认。

#### 添加公开密钥

![image-20240101075107597](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202312/image-20240101075107597.png)

添加成功之后，创建账户时所用的邮箱会接到一封提示“公共密钥添加完成”的邮件。
完成以上设置后，就可以用手中的私人密钥与 GitHub 进行认证和通信了。让我们来实际试一试。

```bash
$ ssh -T git@github.com
The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is  `fingerprint值` .
Are you sure you want to continue connecting (yes/no)? `输入yes` 
```

出现如下结果即为成功。

```
Hi hirocastest! You've successfully authenticated, but GitHub does not 
provide shell access.
```

可以`Follow`感兴趣的用户，对于仓库，也可以使用 Watch 功能获取最新的开发信息。如果您经常使用的某个软件正在 GitHub 上进行开发，不妨去 `Watch` 一下。

#### 创建仓库

##### Initialize this repository with a README

在 Initialize this repository with a README 选项上打钩，随后GitHub 会自动初始化仓库并设置 README 文件，让用户可以立刻clone 这个仓库。如果想向 GitHub 添加手中已有的 Git 仓库，建议不要勾选，直接手动 push。

#####  Add .gitignore

下方左侧的下拉菜单非常方便，通过它可以在初始化时自动生成 .gitignore 文件 A。这个设定会帮我们把**不需要**在 Git 仓库中进行版本管理的文件记录在 .gitignore 文件中，省去了每次根据框架进行设置的麻烦。下拉菜单中包含了主要的语言及框架，选择今后将要使用的即可。

##### Add a license

右侧的下拉菜单可以选择要添加的许可协议文件。如果这个仓库中包含的代码已经确定了许可协议，那么请在这里进行选择。随后将自动生成包含许可协议内容的 LICENSE 文件，用来表明该仓库内容的许可协议。

#### 连接仓库

##### GitHub Flavored Markdown

在 GitHub 上进行交流时用到的 Issue、评论、Wiki，都可以用Markdown 语法表述，从而进行标记。准确地说应该是 GitHub Flavored Markdown（GFM）语法。该语法虽然是 GitHub 在 Markdown 语法基础上扩充而来的，但一般情况下只要按照原本的 Markdown 语法进行描述就可以。
关于 Markdown 语法的解说，[网上也有相关资料可查](http://www.ituring.com.cn/article/775)。

##### 编写代码

```bash
 `hello_word.php的内容`
<?php
 echo "Hello World!";
?>
```

由于 hello_word.php 还没有添加至 Git 仓库，所以显示为 `Untracked files`。

```bash
$ git status
# On branch master
# Untracked files:
# (use "git add <file>..." to include in what will be committed)
#
# hello_world.php
nothing added to commit but untracked files present (use "git add" to track)
```

##### 提交

将 hello_word.php 提交至仓库。这样一来，这个文件就进入了版本管理系统的管理之下。**今后的更改管理**都交由 Git 进行。

```bash
$ git add hello_world.php
$ git commit -m "Add hello world script by php"
[master d23b909] Add hello world script by php
 1 file changed, 3 insertions(+)
 create mode 100644 hello_world.php
```

通过 `git add` 命令将文件加入<span style="background-color: yellow; color: black; cursor: help;" title="在 Index 数据结构中记录文件提交之前的状态。">暂存区</span>，再通过 `git commit` 命令提交。
添加成功后，可以通过 `git log` 命令查看提交日志。

```bash
$ git log
commit d23b909caad5d49a281480e6683ce3855087a5da
Author: hirocastest <hohtsuka@gmail.com>
Date: Tue May 1 14:36:58 2012 +0900
 Add hello world script by php
`略`
```

##### 进行 push

之后只要执行 push，GitHub 上的仓库就会被更新。

```bash
$ git push
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 328 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:hirocastest/Hello-World.git
 46ff713..d23b909 master -> master
```

这样一来代码就在 GitHub 上公开了。

---

#### git init——初始化仓库

要使用 Git 进行版本管理，必须先初始化仓库。Git 是使用 `git init` 命令进行初始化的。请实际建立一个目录并初始化仓库。

```bash
$ mkdir git-tutorial
$ cd git-tutorial
$ git init
Initialized empty Git repository in /Users/hirocaster/github/github-book
/git-tutorial/.git/
```

如果初始化成功，执行了 `git init` 命令的目录下就会生成 .git 目录。这个 **.git 目录**里存储着管理当前目录内容所需的仓库数据。
在 Git 中，我们将这个目录的内容称为“**附属于该仓库的工作树**”。文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。如果想将文件恢复到原先的状态，可以从仓库中调取之前的快照，在工作树中打开。开发者可以通过这种方式获取以往的文件。

#### git status——查看仓库的状态

git status命令用于显示 Git 仓库的状态。工作树和仓库在被操作的过程中，状态会不断发生变化。在 Git 操作过程中时常用 `git status` 命令查看当前状态，可谓基本中的基本。

```bash
$ git status
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
```

结果显示了我们当前正处于 master 分支下。接着还显示了没有可提交的内容。所谓**提交**（Commit），是指“**记录工作树中所有文件的当前状态**”。
尚没有可提交的内容，就是说当前我们建立的这个仓库中还没有记录任何文件的任何状态。这里，我们建立 README.md 文件作为管理对象，为第一次提交做前期准备。

```bash
$ touch README.md
$ git status
# On branch master
#
# Initial commit
## Untracked files:# (use "git add <file>..." to include in what will 
be committed)#
# README.md
nothing added to commit but untracked files present (use "git add" to 
track)
```

可以看到在 Untracked files 中显示了 README.md 文件。类似地，只要对 Git 的工作树或仓库进行操作，git status命令的显示结果就会发生变化。

#### git add——向暂存区中添加文件

如果只是用 Git 仓库的工作树创建了文件，那么该文件并不会被记入 Git 仓库的版本管理对象当中。因此我们用 git status命令查看README.md 文件时，它会显示在 Untracked files 里。
要想让文件成为 Git 仓库的管理对象，就需要用 git add命令将其加入暂存区（Stage 或者 Index）中。暂存区是提交之前的一个临时区域。

```bash
$ git add README.md
$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
# (use "git rm --cached <file>..." to unstage)
#
# new file: README.md
#
```

将 README.md 文件加入暂存区后，git status命令的显示结果发生了变化。可以看到，README.md 文件显示在 `Changes to be committed` 中了。

#### git commit——保存仓库的历史记录

git commit命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。

实际运行一下 git commit命令。

```bash
$ git commit -m "First commit"
[master (root-commit) 9f129ba] First commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
```

-m 参数后的 "First commit"称作**提交信息**，是对这个提交的概述。

##### 记述详细提交信息

刚才我们只简洁地记述了一行提交信息，如果想要记述得更加详细，请**不加 - m**，直接执行 git commit命令。执行后编辑器就会启动，并显示如下结果。

```bash
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
#
# Initial commit
#
# Changes to be committed:
# (use "git rm --cached <file>..." to unstage)
#
# new file: README.md
#
```

**在编辑器中记述**提交信息的格式如下。
● 第一行：用一行文字简述提交的更改内容
● 第二行：空行
● 第三行以后：记述更改的原因和详细内容

只要按照上面的格式输入，今后便可以通过确认日志的命令或工具看到这些记录。
在以 #（井号）标为注释的 Changes to be committed（要提交的更改）栏中，可以查看本次提交中包含的文件。将提交信息按格式记述完毕后，请保存并关闭编辑器，以 #（井号）标为注释的行不必删除。随后，刚才记述的提交信息就会被提交。

##### 中止提交

如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编辑器，随后提交就会被中止。

##### 查看提交后的状态

执行完 git commit命令后再来查看当前状态。

```bash
$ git status
# On branch master
nothing to commit, working directory clean
```

当前工作树处于刚刚完成提交的最新状态，所以结果显示没有更改。

##### git log——查看提交日志

git log命令可以查看以往仓库中提交的日志。包括可以查看什么人在什么时候进行了提交或合并，以及操作前后有怎样的差别。

先来看看刚才的 git commit命令是否被记录了。

```bash
$ git log
commit 9f129bae19b2c82fb4e98cde5890e52a6c546922
Author: hirocaster <hohtsuka@gmail.com>
Date: Sun May 5 16:06:49 2013 +0900
 First commit
```

如上所示，屏幕显示了刚刚的提交操作。commit 栏旁边显示的“9f129b……”是指向这个提交的哈希值。Git 的其他命令中，在指向提
交时会用到这个哈希值。
Author 栏中显示我们给 Git 设置的用户名和邮箱地址。Date 栏中显示提交执行的日期和时间。再往下就是该提交的提交信息。

##### 只显示提交信息的第一行

如果只想让程序**显示第一行简述信息**，可以在 git log命令后加上 `--pretty=short`。这样一来开发人员就能够更轻松地把握多个提交。

##### 只显示指定目录、文件的日志

只要在 `git log` 命令后加上目录名，便会只显示该目录下的日志。如果加的是文件名，就会只显示与该文件相关的日志。

```bash
$ git log README.md
```

##### 显示文件的改动

如果想查看提交所带来的改动，可以加上 `-p` 参数，文件的前后差别就会显示在提交信息之后。

```bash
$ git log -p
```

比如，执行下面的命令，就可以只查看 README.md 文件的提交日志以及提交前后的差别。

```bash
$ git log -p README.md
```

#### git diff——查看更改前后的差别

`git diff` 命令可以查看工作树、暂存区、最新提交之间的差别。

我们在刚刚提交的 README.md 中写点东西。

```txt
# Git教程
```

这里用 Markdown 语法写下了一行题目。

##### 查看工作树和暂存区的差别

执行 `git diff` 命令，查看当前工作树与暂存区的差别。（a和b是两个不同分支）

```bash
$ git diff

diff --git a/README.md b/README.md
index e69de29..cb5dc9f 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# Git教程
```

由于我们尚未用 `git add` 命令向暂存区添加任何东西，所以程序只会显示工作树与最新提交状态之间的差别。

这里解释一下显示的内容。“+”号标出的是新添加的行，被删除的行则用“-”号标出。我们可以看到，这次只添加了一行。
用 `git add` 命令将 README.md 文件加入暂存区。

```bash
$ git add README.md
```

##### 查看工作树和最新提交的差别

如果现在执行 `git diff` 命令，由于工作树和暂存区的状态并无差别，结果什么都不会显示。要查看与最新提交的差别，请执行以下命令。

```
$ git diff HEAD
diff --git a/README.md b/README.md
index e69de29..cb5dc9f 100644
--- a/README.md
+++ b/README.md
@@ -0,0 +1 @@
+# Git教程
```

不妨养成这样一个好习惯：在执行 `git commit` 命令之前先执行`git diff HEAD`命令，查看本次提交与上次提交之间有什么差别，等确认完毕后再进行提交。这里的 **HEAD 是指向当前分支中最新一次提交的指针**。
由于我们刚刚确认过两个提交之间的差别，所以直接运行 `git commit` 命令。

```
$ git commit -m "Add index"
[master fd0cbf0] Add index
 1 file changed, 1 insertion(+)
```

保险起见，我们查看一下提交日志，确认提交是否成功。

```
$ git log
commit fd0cbf0d4a25f747230694d95cac1be72d33441d
Author: hirocaster <hohtsuka@gmail.com>
Date: Sun May 5 16:10:15 2013 +0900

 Add index
 
commit 9f129bae19b2c82fb4e98cde5890e52a6c546922
Author: hirocaster <hohtsuka@gmail.com>
Date: Sun May 5 16:06:49 2013 +0900

 First commit
```

成功查到了第二个提交。

### 分支的操作

#### git branch——显示分支一览表

`git branch`命令可以将分支名列表显示，同时可以确认当前所在分支（标星号*的）。

#### git checkout -b——创建、切换分支

如果想以当前的 main （默认）分支为基础创建新的分支，我们需要用到`git checkout -b`命令。

##### 切换到 feature-A 分支并进行提交

执行下面的命令，创建并切换到名为 feature-A 的分支。

```
$ git checkout -b feature-A
Switched to a new branch 'feature-A'
```

等效于

```
$ git branch feature-A
$ git checkout feature-A
```

不断对一个分支（例如feature-A）进行提交的操作，我们称为“**培育分支**”。

##### 切换回 main 分支

```
$ git checkout main
Switched to branch 'main'
```

##### 切换回上一个分支

```
$ git checkout -
Switched to branch 'feature-A'
```

像上面这样用“-”（连字符）代替分支名，就可以切换至上一个分支。当然，将“-”替换成 feature-A 同样可以切换到 feature-A 分支。

#### 特性 (Feature) 分支

Git 与 Subversion（SVN）等集中型版本管理系统不同，创建分支时不需要连接中央仓库，所以能够相对轻松地创建分支。因此，当今大部分工作流程中都用到了**特性（Topic）分支**。
特性分支顾名思义，是集中实现单一特性（主题），除此之外不进行任何作业的分支。在日常开发中，往往会创建数个特性分支，同时在此之外再保留一个随时可以发布软件的稳定分支。稳定分支的角色通常由 main 分支担当。

基于特定主题的作业在特性分支中进行，主题完成后再与 main 分支合并。

#### 主干 (main) 分支

主干分支是刚才我们讲解的特性分支的原点，同时也是合并的终点。通常人们会用 main 分支作为主干分支。

有时我们需要让这个主干分支总是配置在正式环境中，有时又需要用标签 Tag 等创建版本信息，同时管理多个版本发布。拥有多个版本发布时，**主干分支也有多个**。

#### git merge——合并分支

假设 feature-A 已经实现完毕，想要将它合并到主干分支 main 中。首先切换到 main 分支，然后把 feature A分支“拽”着合并进来。

```bash
$ git checkout main
```

然后合并 feature-A 分支。为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交。因此，在合并时加上 `--no-ff` 参数。

{% hideToggle --no-ff参数介绍 %}

在Git版本控制系统中，`--no-ff`是一个合并（merge）操作的选项。`ff`在这里的含义是“Fast-forward”，也就是快进模式。

为了更清楚地解释`--no-ff`参数的含义，我们需要先了解一下Git的Fast-forward模式。

在Git中，如果一个分支（例如，feature分支）是从另一个分支（例如，master分支）创建的，然后在feature分支上进行了提交，而在此期间master分支没有任何变动，那么当feature分支合并回master分支时，Git默认会采取Fast-forward模式。在Fast-forward模式中，Git只需简单地将master分支的指针向前“快进”到feature分支的最新提交，就完成了合并。结果就是，合并后的提交历史线性无分叉，你无法看到分支曾经存在过。

而当使用`--no-ff`选项进行合并时，Git会禁用Fast-forward模式，即使当前的合并可以进行Fast-forward。Git会创建一个新的merge commit，即使这个commit并不总是必要的。这样，你可以从commit历史中显式地看到一个合并发生过，以及哪些提交属于哪个分支。这对于保持明确、易于理解的历史记录非常有用。

简单说，`--no-ff`选项让合并后的Git历史记录保留分支信息，给出更丰富的项目历史信息。

{% endhideToggle %}

```git bash
$ git merge --no-ff feature-A
```

随后编辑器会启动，用于录入合并提交的信息。

```
Merge branch 'feature-A'

# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
```



---

command `git branch -M main` changes your main branch's name to "main". （应该是本地）

To create a new branch, run this command: `git checkout -b test`. I will break it down. `checkout` tells Git it is supposed to switch to a new branch. `-b` tells Git to create a new branch. `test` is the name of the branch to be created and switched to.

You can check all the branches that exist in your repo by running the `git branch` command.

To **pull** in Git means to clone a remote repository's **current state** into your computer/repository. This comes in handy when you want to work on your repo from a different computer or when you are contributing to an open source project online.

## How to check your Git configuration:

The command below returns a list of information about your git configuration including user name and email:

```
git config -l
```

## How to setup your Git username:

With the command below you can configure your user name:

```
git config --global user.name "Fabio"
```

## How to setup your Git user email:

This command lets you setup the user email address you'll use in your commits.

```
git config --global user.email "signups@fabiopacifici.com"
```

## How to cache your login credentials in Git:

You can store login credentials in the cache so you don't have to type them in each time. Just use this command:

```
git config --global credential.helper cache
```

## How to initialize a Git repo:

Everything starts from here. The first step is to initialize a new Git repo locally in your project root. You can do so with the command below:

```
git init
```

## How to add a file to the staging area in Git:

The command below will add a file to the staging area. Just replace `filename_here` with the name of the file you want to add to the staging area.

```
git add filename_here
```

## How to add all files in the staging area in Git

If you want to add all files in your project to the staging area, you can use a wildcard `.` and every file will be added for you.

```
git add .
```

## How to add only certain files to the staging area in Git

With the asterisk in the command below, you can add all files starting with 'fil' in the staging area.

```
git add fil*
```

## How to check a repository's status in Git:

This command will show the status of the current repository including staged, unstaged, and untracked files.

```
git status
```

## How to commit changes in the editor in Git:

This command will open a text editor in the terminal where you can write a full commit message.

A commit message is made up of a short summary of changes, an empty line, and a full description of the changes after it.

```
git commit
```

## How to commit changes with a message in Git:

You can add a commit message **without opening the editor**. This command lets you only specify a short summary for your commit message.

```
git commit -m "your commit message here"
```

## How to commit changes (and skip the staging area) in Git:

You can add and commit tracked files with a single command by using the -a and -m options. 这个 `-a` 标记的全称是 `--all`，这表示 Git 将提交所有在工作区被修改（但不包括新文件或者被删除的文件）的文件。如果你在 `-a` 后没有指定文件名，那么 Git 将自动确认（即，把文件的更改添加到暂存区）所有已跟踪的文件中的更改，并随后会提交这些更改。

```
git commit -a -m "your commit message here"
```

## How to see your commit history in Git:

This command shows the commit history for the current repository:

```
git log
```

## How to see your commit history including changes in Git:

This command shows the commit's history including all files and their changes: 

`-p` 是一个选项，也可以写作 `--patch`。当你添加这个选项时，Git 不只会显示每个提交的信息，还会显示每个提交具体修改了哪些内容。换句话说，`-p` 选项会让 Git 显示每个提交的 "patch"，也就是每个提交所做的更改。

具体来说，`git log -p` 命令会显示每个文件的更改的内容、更改行的位置、以及具体的添加和删除了哪些行。添加的行会用绿色加号标注，删除的行会用红色减号标注。

总的来说，`git log -p` 提供了一种检查项目历史的详细方式，让你可以更好地理解每次提交做了什么改动。

```
git log -p
```

## How to see a specific commit in Git:

This command shows a specific commit.

Replace commit-id with the id of the commit that you find in the commit log after the word commit.

```
git show commit-id
```

## How to see log stats in Git:

This command will cause the Git log to show some statistics about the changes in each commit, including line(s) changed and file names.

用来查看提交历史以及每次提交影响的文件和行数的命令。`--stat` 是一个选项，它会在每个提交信息后面额外显示修改的文件，每个文件修改的行数，以及每个文件更改的具体概要。

```
git log --stat
```

## How to see changes made before committing them using "diff" in Git:

You can pass a file as a parameter to only see changes on a specific file.
`git diff` shows only unstaged changes by default.

We can call diff with the `--staged` flag to see any staged changes.

`git diff` 是一个在 Git 版本控制系统中用来显示文件差异的命令。命令的具体解释：

1. `git diff`：这是最基础的用法，不带任何参数。它会比较工作区和暂存区间的差异，显示那些被修改但还未被加入到暂存区的变更。
2. `git diff all_checks.py`：在 `git diff` 后面加上一个文件名（在这里是 `all_checks.py`），Git 会显示在工作区中相对于暂存区，该文件的具体改变。只有在这个文件有变化，并且这个变化尚未添加到暂存区时，这个命令才会显示输出。
3. `git diff --staged`：使用 `--staged` 选项（也可使用 `--cached` 选项，两者等同），`git diff` 会显示在暂存区和最后一次提交之间的差异。这个命令展示了你下一次提交时，哪些改动将被包含。

`git diff` 命令对于了解在下一次提交前你的暂存区到底发生了什么改变非常有用，从而帮助你管理和组织你的提交。

```
git diff
git diff all_checks.py
git diff --staged
```

## How to see changes using "git add -p":

This command opens a prompt and asks if you want to stage changes or not, and includes other options.

当你执行 `git add -p` 命令时，Git 会显示你做过的每一个修改，并让你可以选择是否要暂存这个修改。对于每一个修改，你可以选择 'y'（表示 'yes'，暂存这个修改），'n'（表示 'no'，不暂存这个修改），或者其他的选项。

`git add -p` 非常有用，因为它让你可以精确地控制你想要提交的更改。例如，如果你在一个文件中做了多个更改，但你只想提交其中的一部分，那么你可以用 `git add -p` 来选择你想要提交的部分。

最后，要注意的是，执行完 `git add -p` 命令后，你需要执行 `git commit` 命令来提交这些暂存的更改，这样才能把这些更改保存到你的版本历史中。

```
git add -p
```

## How to remove tracked files from the current working tree in Git:

This command expects a commit message to explain why the file was deleted.

```
git rm filename
```

## How to rename or move files in Git:

This command stages the changes, then it expects a commit message.

```
git mv oldfile newfile  # 这条命令将会把工作区中的 `oldfile` 文件重命名为 `newfile`。
```

```
git mv filename directory  #这条命令将会把工作区中的 `filename` 文件移动到 `directory` 目录下。
```

`git mv` 命令会立即在工作区中对文件进行重命名或移动，而且这个变更会被自动暂存，也就是说会立即进入 Git 的暂存区，等待被提交。

## How to ignore files in Git:

Create a `.gitignore` file and commit it.

## How to revert unstaged changes in Git:

此命令可以用来撤销对工作区中文件的修改。它会将指定的文件或目录恢复到最近一次 `git commit` 或 `git add` 的状态。如果你在这之后对文件进行了修改或者删除，使用这个命令可以撤销这些更改。

```
git checkout filename
```

需要注意的是，`git checkout filename` 命令会立即在工作区中对文件进行更新，而且这个更新是无法撤销的。因此，在使用这个命令前，需要确认对当前文件的修改是否不再需要。

## How to revert staged changes in Git:

You can use the -p option flag to specify the changes you want to reset.

```
git reset HEAD filename
```

这条命令将在暂存区中的 `filename` 文件恢复到未暂存的状态，但是它不会撤销你在工作区中对文件的修改。

也就是说，`git reset HEAD filename` 命令可以用来撤销 `git add filename` 命令，但不能用来撤销 `git commit -m 'your message'` 命令。如果你想撤销最近的提交，你需要使用`git reset --soft HEAD~1` 或者 `git reset --hard HEAD~1` 命令。

```
git reset HEAD -p
```

`git reset -p` （或者也可以写作 `git reset --patch`）的效果和 `git add -p` 类似，但方向相反 —— `git add -p` 命令允许你选择性地将文件变更添加到暂存区，而 `git reset -p` 则允许你选择性地将文件变更从暂存区撤销。

当你运行 `git reset HEAD -p` 命令后，它会为暂存区中的每一个文件变更显示一个提示，你可以选择 `y`（意味着 "是的，取消暂存这个变更"），`n`（意味着 "不，保持这个变更在暂存区"），或者其它一些选项来决定如何处理每一个变更。

需要注意的是，`git reset HEAD -p` 命令只会从暂存区移出文件变更，但不会撤销在工作区中对文件的修改。

## How to amend the most recent commit in Git:

`git commit --amend` allows you to modify and add changes to the most recent commit.

```
git commit --amend
```

!!Note!!: fixing up a local commit with amend is great and you can push it to a shared repository after you've fixed it. But you should avoid amending commits that have already been made public.

## How to rollback the last commit in Git:

`git revert` will create a new commit that is the opposite of everything in the given commit.
We can revert the latest commit by using the head alias like this:

```
git revert HEAD
```

## How to rollback an old commit in Git:

You can revert an old commit using its commit id. This opens the editor so you can add a commit message.

```
git revert commit_id
```

## How to create a new branch in Git:

By default, you have one branch, the main branch. With this command, you can create a new branch. Git won't switch to it automatically – you will need to do it manually with the next command.

```
git branch branch_name
```

## How to switch to a newly created branch in Git:

When you want to use a different or a newly created branch you can use this command:

```
git checkout branch_name
```

## How to list branches in Git:

You can view all created branches using the `git branch` command. It will show a list of all branches and mark the current branch with an asterisk and highlight it in green.

```
git branch
```

## How to create a branch in Git and switch to it immediately:

In a single command, you can create and switch to a new branch right away.

```
git checkout -b branch_name
```

## How to delete a branch in Git:

When you are done working with a branch and have merged it, you can delete it using the command below:

```
git branch -d branch_name
```

## How to merge two branches in Git:

To merge the history of the branch you are currently in with the `branch_name`, you will need to use the command below:

```
git merge branch_name
```

## How to show the commit log as a graph in Git:

We can use `--graph` to get the commit log to show as a graph. Also,
`--oneline` will limit commit messages to a single line.

```
git log --graph --oneline
```

## How to show the commit log as a graph of all branches in Git:

Does the same as the command above, but for all branches.

```
git log --graph --oneline --all
```

## How to abort a conflicting merge in Git:

If you want to throw a merge away and start over, you can run the following command:

```
git merge --abort
```

## How to add a remote repository in Git

This command adds a remote repository to your local repository (just replace `https://repo_here` with your remote repo URL).

```
git add remote https://repo_here
```

## How to see remote URLs in Git:

You can see all remote repositories for your local repository with this command:

```
git remote -v
```

## How to get more info about a remote repo in Git:

Just replace `origin` with the name of the remote obtained by
running the git remote -v command.

```
git remote show origin
```

## How to push changes to a remote repo in Git:

When all your work is ready to be saved on a remote repository, you can push all changes using the command below:

```
git push
```

## How to pull changes from a remote repo in Git:

If other team members are working on your repository, you can retrieve the latest changes made to the remote repository with the command below:

```
git pull
```

## How to check remote branches that Git is tracking:

This command shows the name of all remote branches that Git is tracking for the current repository:

```
git branch -r
```

## How to fetch remote repo changes in Git:

This command will download the changes from a remote repo but will not perform a merge on your local branch (as git pull does that instead).

```
git fetch
```

## How to check the current commits log of a remote repo in Git

Commit after commit, Git builds up a log. You can find out the remote repository log by using this command:

```
git log origin/main
```

## How to merge a remote repo with your local repo in Git:

If the remote repository has changes you want to merge with your local, then this command will do that for you:

```
git merge origin/main
```

## How to get the contents of remote branches in Git without automatically merging:

This lets you update the remote without merging any content into the
local branches. You can call git merge or git checkout to do the merge.

```
git remote update
```

## How to push a new branch to a remote repo in Git:

If you want to push a branch to a remote repository you can use the command below. Just remember to add -u to create the branch upstream:

```
git push -u origin branch_name
```

## How to remove a remote branch in Git:

If you no longer need a remote branch you can remove it using the command below:

```
git push --delete origin branch_name_here
```

## How to use Git rebase:

You can transfer completed work from one branch to another using `git rebase`.

```
git rebase branch_name_here
```

这个命令用于将更改从一个分支复制到另一个分支。假设你正在当前分支上工作，并已经创建了一些提交，但同时，其他人也在同一个项目上完成了一些工作并提交到主干分支。此时，你可以使用 `git rebase` 命令来获取他们的更改，而不会产生一个合并提交。

`git rebase` 会首先取消你当前分支上的提交，然后在你指定的另一个分支上重新应用这些提交，因此，你的提交历史会更清晰、线性，这对于项目的历史理解是有帮助的。

这是一种非常常用的方法，尤其是当你在一个长期分支上工作，并且需要经常将主干分支的更改合并到你的分支时。

这里是一个简单的 `git rebase` 命令的例子：

```bash
git rebase master
```

在这个例子中，`master` 是我们想要将当前分支的更改应用到的基准点。

然而，需要注意的是，`git rebase` 会通过改变提交历史来达到清晰、线性的目的。如果你在公开的分支上进行 `rebase`，这可能会给其他开发者带来困扰，因为它会改变提交历史。因此，`rebase` 最好用于本地的私有分支。

## How to run rebase interactively in Git:

You can run git rebase interactively using the -i flag.
It will open the editor and present a set of commands you can use.

```
git rebase -i master
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```

## How to force a push request in Git:

This command will force a push request. This is usually fine for pull request branches because nobody else should have cloned them.
But this isn't something that you want to do with public repos.

```
git push -f
```





---

在**Git Bash中的"ls"命令**（无需在前面加 `git`，且只能在 Git bash 中运行，输出结果默认多列显示）其实就是从Linux环境中取的，"ls"命令在这两个环境中的功能完全相同，它是用来列出当前目录下的所有文件与子目录。

"ls"命令可以选用一些参数来改变它的输出结果，例如：

- "ls -l"：列出文件和目录的详细信息，包括大小，修改日期和权限等。
- "ls -a"：列出所有文件和目录，包括以"."开头的隐藏文件。
- "ls -h"：以易读的方式列出文件大小（例如KB，MB）。

---

`git`命令在`cmd`和在`Git bash`中运行有何区别？

在大多数情况下，Git 命令在 CMD（Windows命令提示符）和 Git Bash中运行的效果是相同的。主要的区别在于这两个环境提供的附加功能和对 Linux 命令的 support。

1. **环境和工具支持**：Git Bash 是一个模仿 Bash（一个流行的 Linux shell）的环境，它还包括了一些常见的 Unix 工具，比如 ls、ssh 和 grep 等命令。这些命令是在Windows的CMD中无法直接使用的。如果你有在Linux或者macOS下工作的经验，你可能会发现 Git Bash 更加亲切和易用。
2. **路径处理**：在 Git Bash 中，你可以使用 Unix 惯用的前斜杠（/）来写路径名。例如，在 Git Bash 中，你可以使用 "/c/Users" 来访问 "C:\Users"。而在 CMD 中，你需要使用反斜杠（\）来写路径名。
3. **脚本**：Git Bash 提供了对 Bash 脚本的支持，因此在 Git Bash 中可以执行复杂的脚本命令。而CMD则只支持Windows批处理命令。

基于以上区别，你可以根据你的具体需求和使用习惯来选择合适的环境。如果你需要运行更复杂的脚本，或者习惯于使用 Unix 工具，那么推荐你使用 Git Bash。如果你需要与Windows的其他命令或程序进行交互，或者只需运行简单的 Git 命令，那么 CMD 也是一个不错的选择。

---

> git add .和git add -all有区别吗？

实际上，你可能是在询问 `git add .` 和 `git add --all` (`git add -A`)之间的区别。这两个命令都是用于将工作区的更改添加到 Git 的暂存区，但是它们工作的方式略有不同：

- `git add .` : 这个命令将会添加当前目录和其子目录中所有新的或被修改的文件到暂存区。然而，如果你从工作区删除了一个文件（并且这个删除操作还没有被暂存），`git add .` 不会将这个删除操作添加到暂存区。
- `git add --all` : 这个命令将会添加所有新的、被修改的、以及被删除的文件到暂存区。如果你从工作区删除了一个文件，`git add --all` 会将这个删除操作添加到暂存区。

因此，这两个命令的主要区别在于是否处理被删除的文件。如果你希望将你删除的文件也加入到暂存区，那么应该使用 `git add --all`。如果你只关心新的和被修改的文件，那么 `git add .` 就足够了。

---

`git status --short`

**Note:** Short status flags are:

- ?? - Untracked files
- A - Files added to stage
- M - Modified files
- D - Deleted files

---

## Git Help

If you are having trouble remembering commands or options for commands, you can use Git `help`.

There are a couple of different ways you can use the `help` command in command line:

- `git *command* -help` - See all the available options for the specific command
- `git help --all` - See all possible commands

> `git help` 和 `git help --all` 有何区别？

`git help` 和 `git help --all` 这两个命令的主要区别在于它们展示的信息的详细程度。

- `git help`：此命令会输出 Git 的基本帮助信息，包括一些常见的 Git 命令和介绍。你也可以使用 `git help <命令名>` 来查看特定 Git 命令的详细用法和说明。
- `git help --all`：此命令会输出所有 Git 命令/功能的列表。如果你想查看 Git 提供了哪些功能或要找特定的 Git 命令，`git help --all` 是一个很有用的工具。

所以，`git help --all` 提供了一个比 `git help` 更详细的命令列表。此外，`git help --all` 这个命令非常有用，当你不确定一个特定功能的命令是什么，或者你想知道 Git 还有什么其它命令或功能时可以参考。

例如：

```
git commit -help
usage: git commit [] [--] ...

    -q, --quiet           suppress summary after successful commit
    -v, --verbose         show diff in commit message template
```

**Note:** You can also use `--help` instead of `-help` to open the relevant Git manual page

`git help --all`会输出 一个长长的列表，可以按 `Shift+G` 跳到末尾或 `q` 退出。

---

Git 是设计为保护你的本地改动的，一般不会无故丢失你的文件。如果你的文件无意中被删除了，一个可能的原因是这个文件在远程仓库中被删除了。默认情况下，`git pull` 会尝试把你的本地仓库和远程仓库同步，如果远程仓库删除了一个文件，那么在你本地运行 `git pull` 之后，这个文件也会在你的本地仓库被删除。不过在删除之前，Git 通常会检查这个文件是否有未提交的改动，如果有的话，Git 会阻止删除操作，并提示你先提交或储藏（stash）你的改动。

Git 在设计上不会删除未跟踪的文件/文件夹。未跟踪的文件在 git 眼中是看不见的，无论你执行哪个命令都不会对它们产生影响。只有当文件被跟踪后（通过 `git add` 添加），才能被 git 命令所管理。也就是说，如果一个文件从未被添加到 git 仓库（一直是未跟踪的状态）那么它就不会被任何 git 命令删除。从你的描述来看，我猜测你的文件/文件夹是被跟踪的，然后在远程被其他人删除，所以在你执行 `git pull` 命令后本地的文件被删除了。

在 Git 中，`-p` 或者 `--prune` 选项通常用于清理（剪枝）那些在远程仓库中已被删除但在本地仓库中仍然存在引用的分支。

在多人协作的项目中，常常有新的分支被创建和删除。有时，你的本地仓库可能还保留着远程仓库中已经被删除的分支的引用。在这种情况下，`-p` 或 `--prune` 选项就变得有用了，它可以帮助你清理那些已经被删除但你的本地仓库中仍然存在的远程分支。

举个例子，如果你使用 `git fetch -p origin` 或者 `git fetch --prune origin`，Git 会从名为 "origin" 的远程仓库获取新的数据，并且删除任何在远程仓库已被删除但在本地仓库中仍存在的分支的引用。

这个选项并不会影响你的本地分支，也不会删除本地存在但远程仓库中不存在的文件或文件夹。它的主要作用是同步你的本地仓库和远程仓库，清理已经无效的远程分支引用。在其他命令（如 `git pull`）中，这个选项可能会执行不同的操作，具体取决于命令的具体实现。

所以，`-p` 或 `--prune` 选项主要用于清理无效的远程分支引用，帮助你让本地仓库和远程仓库保持同步。

---

`git checkout <file>`命令可以用于恢复在工作区中指定文件的更改。其功能是将特定文件恢复到最后一次提交的状态。

需要注意的是，这个命令只能恢复已经提交的文件版本。也就是说，如果你对文件做了修改，但还没有提交，然后运行`git checkout <file>`，那么所有未提交的修改都会丢失。

所以在使用这个命令时要特别小心。在对文件进行重要修改时，建议定期提交，以免出现意外。

`git add .` 只会添加**当前目录及其子目录下的修改**。所以如果你在项目根目录下执行 `git add .`，你会把整个项目的修改都添加到暂存区。但如果你在一个子目录下执行 `git add .`，那么只有这个子目录及其子目录下的修改被添加到了暂存区。

`git add --all` 则会添加**工作树中所有的修改**到暂存区，包括这个项目所有目录中的修改，以及新增的文件和已经删除的文件。

所以，如果你删除了一个文件，然后在项目根目录下执行了 `git add .`，这个删除操作就被添加到了暂存区，并且在下一次的 `git commit` 中会被提交。而如果你执行了 `git add --all`，无论你在哪一个目录下，删除的文件都会被添加到暂存区，并在下一次的 `git commit` 中被提交。

在任何一种情况下，你还是可以使用 `git checkout -- <file>` 来恢复已经删除的文件。只要这个文件在最近一次的 commit 中存在，它就能被恢复。

`git checkout -- <directory>`可以用来恢复整个目录及其内容。它会恢复这个目录中所有文件到最近一次commit的状态。如果在最近一次的commit中，该目录及其内容存在，则它们会被恢复。

比如，如果你 accidently 删除了一个名为 "myfolder" 的目录，你可以用以下命令恢复它：

plaintext

```plaintext
git checkout -- myfolder
```

这条命令将会恢复 "myfolder"目录及其所有内容。

但请注意，跟恢复单个文件一样， `git checkout -- <directory>`只能恢复到最近一次commit的状态。如果在你删除目录之后，目录或其内的文件有所更改并且没有提交，这些更改将会丢失。

---

在Git中，"Fast-forward"是指当你试图将一个分支合并到另一个分支时，如果这两个分支存在线性关系，也就是说，没有发生任何新的commit在你当前的分支上，Git会直接将你的指针向前移动。

举个例子，假设你有两个分支，`master` 和 `feature`。开始时，两者指向同一commit。然后在 `feature` 分支上做了一些修改并commit了这些更改。在此过程中，`master` 分支没有发生变化。这样，当你试图将 `feature` 合并到 `master` 时，由于 `master` 分支上没有新的commit，所以 Git 可以做的只是将 `master` 分支的指针移动到 `feature` 分支最新的commit。这就叫做 "Fast-forward"。

但是，如果在 `master` 分支上也有了新的commit，那么Git将不能进行 "Fast-forward"，而必须合并这两个分支的更改，经常会创建一个新的 "合并commit"。

要创建一个 "合并commit"，你需要合并两个分支，这两个分支都有新的独立的更改。这样，git无法使用"Fast-forward"方式进行合并，需要创建一个新的commit以包含这两个分支的所有更改。这个新的commit就被称为 "合并commit"。

例如，你在 `master` 分支，想要合并 `feature` 分支，你可以沿用以下步骤：

1. 确保你正在 `master` 分支：`git checkout master`
2. 合并 `feature` 分支：`git merge feature`

如果 `master` 和 `feature` 分支都有新的独立更改，git将启动一个合并过程，可能需要你解决冲突。解决冲突后，你可以使用 `git add .` 把解决冲突后的文件添加到暂存区，然后执行 `git commit` 完成合并过程，创建一个新的 "合并commit"。在你执行 `git commit` 的时候，git会自动打开一个文本编辑器，让你为这个新的 "合并commit" 输入一个commit信息。

如果你想强制git进行一次真正的合并，即使能够进行 "Fast-forward" 合并，你可以使用 `git merge --no-ff feature` 命令，这将始终创建一个 "合并commit"。

---

`git push --set-upstream origin master`

Now we are going to push our master branch to the origin url, and set it as the default remote branch:

**Note:** Since this is the first time you are connecting to GitHub, you will get some kind of notification you to authenticate this connection.

---

## Git Fetch

`fetch` gets all the change history of a tracked branch/repo.

we can also verify by showing the differences between our local `master` and `origin/master`：`git diff origin/master`。

## Git Merge

`merge` combines the current branch, with a specified branch.

We have confirmed that the updates are as expected, and we can merge our current branch (`master`) with `origin/master`:

`git merge origin/master`

---

`git branch` 查看本地分支

`git branch`查看全部（本地+远程）分支

---

# GitHub Pages

With GitHub pages, GitHub allows you to host a webpage from your repository.

We start by creating a new repository. This repository needs a special name to function as a GitHub page. It needs to be your GitHub `username`, followed by `.github.io`.

![image-20240113185936314](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240113185936314.png)

---

"Fork"这个词在GitHub上的用法，其实是来自更早的开源社区。在软件开发中，"Fork"通常指的是从原始项目中创建一个新的独立分支，该分支随后可以独立发展和变化，而与原始项目并行运行，彼此独立。

"Fork"这个词在物理上的意思是"分叉"，而在项目发展的过程中，"Fork"一个项目，就好像你在一条路上遇到一个分岔路口，然后选择了另外一条路。你沿着新路线走下去，这条路线是依靠原来的道路而开启的，但是随着时间的推移，可能与原来的路线发生显著的不同。

所以，当你在GitHub上"Fork"一个项目时，就意味着你创建了一个原始仓库的副本，并在此基础上进行修改和开发，完全独立于原始仓库。这是开源社区中共享和更改代码的一种常见方式。

A `clone` is a full copy of a repository, including all logging and versions of files.

**Note:** To specify a specific folder to clone to, add the name of the folder after the repository `URL`, like this: `git clone https://github.com/w3schools-test/w3schools-test.github.io.git *myfolder*`

一般来讲，我们 fork 下来的 repo，其 origin 都是不允许改动的：

```
git remote -v
origin  https://github.com/w3schools-test/w3schools-test.github.io.git (fetch)
origin  https://github.com/w3schools-test/w3schools-test.github.io.git (push)
```

可以看出，上面的 origin 是指向被 fork 的源 repo，不允许改动。所以我们要添加自己的 fork：

First, we `rename` the original `origin` `remote`:

```
git remote rename origin upstream
git remote -v
upstream        https://github.com/w3schools-test/w3schools-test.github.io.git (fetch)
upstream        https://github.com/w3schools-test/w3schools-test.github.io.git (push)
```

1. `remote`: `remote` 是 Git 中用以管理远程仓库的命令。你可以通过它添加，删除，修改或列出 Git 仓库中的远程仓库。
2. `rename`: `rename` 是 `remote` 子命令的一部分，用于修改远程仓库的别名。
3. `origin`: `origin` 是一种常见的远程仓库别名，通常是你克隆仓库时默认的别名，指向你克隆的原始仓库。
4. `upstream`: `upstream` 是这个命令中你想要新的别名。

所以，`git remote rename origin upstream` 这条命令的作用就是把远程仓库的别名从 `origin` 改为 `upstream`。这在你想要关联原始的远程仓库并从中获取最新的更新，同时还有一个或多个你自己的远程仓库（通常用别名 `origin`）来推送你的更改时，是很有用的。

Then fetch the `URL` of our own `fork`:

And add that as `origin`:

```
git remote add origin https://github.com/kaijim/w3schools-test.github.io.git
git remote -v
origin  https://github.com/kaijim/w3schools-test.github.io.git (fetch)
origin  https://github.com/kaijim/w3schools-test.github.io.git (push)
upstream        https://github.com/w3schools-test/w3schools-test.github.io.git (fetch)
upstream        https://github.com/w3schools-test/w3schools-test.github.io.git (push)
```

**Note:** According to Git naming conventions, it is recommended to name your own repository `origin`, and the one you forked for `upstream`

Now we have 2 remotes:

- `origin` - our own `fork`, where we have read and write access
- `upstream `- the original, where we have read-only access

在Git中，"origin"和"upstream"并无固定含义，它们只是远程仓库的别名，你可以随便命名。但是在开源社区中，经常使用这两个名字，因此它们有着某种约定俗成的含义。

1. "origin"：通常情况下，当你从远程仓库克隆一个项目到本地时，Git会自动为你创建一个名为"origin"的远程仓库别名，它指向你克隆的远程仓库。"origin"在这里代表你的原始或主要的远程仓库。
2. "upstream"：如果你是从一个Fork的仓库中克隆下来的项目，一般你会把原仓库作为"upstream"。"upstream"在这种情况下通常代表原始的或源头的远程仓库，你可以随时从这个远程仓库拉取最新的代码，保持Fork的项目更新。

让我们以一个例子来说明：假设你"Fork"了一个开源项目，然后你在本地克隆了你的"Fork"版本。在这种情况下，"origin"将会指向你的"Fork"版本，在GitHub中就是"you/repo"，而你可以把原始项目设置为"upstream"，在GitHub中就是"original_author/repo"。这样，你可以方便地从原始项目拉取更新，并推送你的更改到你的"Fork"版本。

然而，这只是一种约定，你完全可以为你的远程仓库设置其他的别名。关键是清楚知道这些别名各自指向哪个远程仓库，并了解如何在它们之间同步代码。

---

## Git Ignore

When sharing your code with others, there are often files or parts of your project, you do not want to share.

Examples

- log files
- temporary files
- hidden files
- personal files
- etc.

Git can specify which files or parts of your project should be ignored by Git using a `.gitignore` file.

Git will not track files and folders specified in `.gitignore`. However, the `.gitignore` file itself **IS** tracked by Git.

## Create .gitignore

To create a `.gitignore` file, go to the root of your local Git, and create it:

```
touch .gitignore
```

Example:

```
# ignore ALL .log files
*.log

# ignore ALL files in ANY directory named temp
temp/
```

**Note:** In this case, we use a single `.gitignore` which applies to the entire repository.

It is also possible to have additional `.gitignore` files in subdirectories. These only apply to files or folders within that directory.

## Rules for .gitignore

Here are the general rules for matching patterns in `.gitignore` files: 

| Pattern                          | Explanation/Matches                                          | Examples                                                     |
| :------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
|                                  | Blank lines are ignored                                      |                                                              |
| # *text comment*                 | Lines starting with # are ignored                            |                                                              |
| *name*                           | All *name* files, *name* folders, and files and folders in any *name* folder | /name.log /name/file.txt /lib/name.log                       |
| *name*/                          | Ending with / specifies the pattern is for a folder. Matches all files and folders in any *name* folder | /name/file.txt /name/log/name.log  **no match:** /name.log   |
| *name*.*file*                    | All files with the *name.file*                               | /name.file /lib/name.file                                    |
| */name*.*file*                   | Starting with / specifies the pattern matches only files in the root folder | /name.file  **no match:** /lib/name.file                     |
| *lib/name*.*file*                | Patterns specifiing files in specific folders are always realative to root (even if you do not start with / ) | /lib/name.file  **no match:** name.file /test/lib/name.file  |
| ***/lib/name.file*               | Starting with ** before / specifies that it matches any folder in the repository. Not just on root. | /lib/name.file /test/lib/name.file                           |
| ***/name*                        | All *name* folders, and files and folders in any *name* folder | /name/log.file /lib/name/log.file /name/lib/log.file         |
| /lib/***/name*                   | All *name* folders, and files and folders in any *name* folder within the lib folder. | /lib/name/log.file /lib/test/name/log.file /lib/test/ver1/name/log.file  **no match:** /name/log.file |
| *.*file*                         | All files withe *.file* extention                            | /name.file /lib/name.file                                    |
| **name*/                         | All folders ending with *name*                               | /lastname/log.file /firstname/log.file                       |
| *name*?.*file*                   | ? matches a **single** non-specific character                | /names.file /name1.file  **no match:** /names1.file          |
| *name*[a-z].*file*               | [*range*] matches a **single** character in the specified range (in this case a character in the range of a-z, and also be numberic.) | /names.file /nameb.file  **no match:** /name1.file           |
| *name*[abc].*file*               | [*set*] matches a **single** character in the specified set of characters (in this case either a, b, or c) | /namea.file /nameb.file  **no match:** /names.file           |
| *name*[!abc].*file*              | [!*set*] matches a **single** character, **except** the ones spesified in the set of characters (in this case a, b, or c) | /names.file /namex.file  **no match:** /namesb.file          |
| *.*file*                         | All files withe *.file* extention                            | /name.file /lib/name.file                                    |
| *name*/ !*name*/secret.log       | ! specifies a negation or exception. Matches all files and folders in any *name* folder, except name/secret.log | /name/file.txt /name/log/name.log  **no match:** /name/secret.log |
| *.*file *!*name*.file            | ! specifies a negation or exception. All files withe *.file* extention, except name.file | /log.file /lastname.file  **no match:** /name.file           |
| *.*file *!*name*/**.file* junk.* | Adding new patterns after a negation will re-ignore a previous negated file All files withe *.file* extention, except the ones in *name* folder. Unless the file name is junk | /log.file /name/log.file  **no match:** /name/junk.file      |

## Local and Personal Git Ignore Rules

It is also possible to ignore files or folders but not show it in the distributed `.gitignore` file.

These kinds of ignores are specified in the `.git/info/exclude` file. It works the same way as `.gitignore` but are not shown to anyone else.

---

## What is SSH

SSH is a secure shell network protocol that is used for network management, remote file transfer, and remote system access.

SSH uses a pair of SSH keys to establish an authenticated and encrypted secure network protocol. It allows for secure remote communication on unsecured open networks.

SSH keys are used to initiate a secure "handshake". When generating a set of keys, you will generate a "public" and "private" key.

The "**public**" key is the one you share with the remote party. Think of this more as the **lock**.

The "**private**" key is the one you keep for yourself in a secure place. Think of this as the **key** to the lock.

SSH keys are generated through a security algorithm. It is all very complicated, but it uses prime numbers, and large random numbers to make the public and private key.

It is created so that the public key can be derived from the private key, but not the other way around.

## Generating an SSH Key Pair

In the command line for Linux, Apple, and in the Git Bash for Windows, you can generate an SSH key.

Let's go through it, step by step.

Start by creating a new key, using your email as a label:

```
ssh-keygen -t rsa -b 4096 -C "test@w3schools.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/user/.ssh/id_rsa):
Created directory '/Users/user/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/user/.ssh/id_rsa
Your public key has been saved in /Users/user/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:******************************************* test@w3schools.com
The key's randomart image is:
+---[RSA 4096]----+
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
+----[SHA256]-----+
```

You will be prompted with the following through this creation:

```
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa):
```

Select a file location, or press "Enter" to use the default file location.

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

Entering a secure passphrase will create an additional layer of security. Preventing anyone who gains access to the computer to use that key without the passphrase. However, it will require you to supply the passphrase anytime the SSH key is used.

Now we add this SSH key pair to the SSH-Agent (using the file location from above):

```
ssh-add /Users/user/.ssh/id_rsa
Enter passphrase for /Users/user/.ssh/id_rsa:
Identity added: /Users/user/.ssh/id_rsa (test@w3schools.com)
```

You will be prompted to supply the passphrase, if you added one.

Now the SSH key pair is ready to use.

是否需要将SSH密钥对添加到SSH-Agent取决于你的具体需求和应用场景。

在一些场景下，确实有必要将SSH密钥对添加到SSH-Agent。例如，如果你在本地有多个SSH密钥，并且你需要经常切换使用它们来访问不同的远程服务器，那么将它们添加到SSH-Agent会非常方便。SSH-Agent可以保存你的SSH私钥，并在需要的时候自动提供相应的私钥。这样，你就不需要每次手动指定私钥，也不需要每次都输入私钥的密码。

一旦你启动了SSH-Agent并向其中添加了私钥，只要你的SSH-Agent还在运行，你就可以任意访问你已经添加过的私钥，无须每次都输入密码。这对于自动化脚本和后台任务来说尤其有用。

然而，如果你只有一个密钥，而且你不介意每次都输入密码的话，那么你可能并不需要添加密钥到SSH-Agent。而且出于安全考虑，在不使用的时候存储在SSH-Agent的密钥应该被清空，以防止在你的电脑被盗或者遗失的情况下，别人能够利用这个密钥访问你的服务器。



## Copy the SSH Public Key

In the previous chapter, we created an SSH key pair.

Now we will use the `clip <` command to copy the public key to our clipboard:

```
clip < /Users/user/.ssh/id_rsa.pub
```

Go to GitHub, navigate to the top left corner, click your profile, and select: Settings:

![GitHub Profile Settings](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/img_github_profile_settings.png)

Then select "SSH and GPG keys". and click the "New SSH key" button:

![GitHub Profile Settings SSH](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/img_github_profile_settings_ssh.png)



---

Select a title, and paste the public SSH key into the "Key" field, and click "Add SSH Key":

![GitHub Profile Settings SSH Add Key](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/img_github_profile_settings_ssh_add.png)

You will be prompted to supply your GitHub password.

## Test SSH Connection to GitHub

Now we can test our connection via SSH to GitHub:

```
ssh -T git@github.com
The authenticity of host 'github.com (140.82.121.3)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com,140.82.121.3' (RSA) to the list of known hosts.
Hi w3schools-test! You've successfully authenticated, but GitHub does not provide shell access.
```

If the last line contains your username on GitHub, you are successfully authenticated!

## Add New GitHub SSH Remote

Now we can add a new remote via SSH to our Git.

First, get the SSH address from our repository on GitHub:

![GitHub Get SSH Code](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/img_github_repository_code_ssh.png)

Then use that address to add a new origin:

```
git remote add ssh-origin git@github.com:w3schools-test/hello-world.git
```

**Note:** You can **change a remote origin from HTTPS to SSH** with the command: `git remote set-url *remote-name* git@github.com:*username*/*repository*.git`

---

## Git Revert

`revert` is the command we use when we want to take a previous `commit` and add it as a new `commit`, keeping the `log` intact.

## Git Revert - Find Commit in Log

First thing, we need to find the point we want to return to. To do that, we need to go through the `log`.

To avoid the very long log list, we are going to use the `--oneline` option, which gives just one line per commit showing:

- The first seven characters of the `commit hash`
- the `commit message`

So let's find the point we want to `revert`:

```
git log --oneline
52418f7 (HEAD -> master) Just a regular update, definitely no accidents here...
9a9add8 (origin/master) Added .gitignore
81912ba Corrected spelling error
3fdaa5b Merge pull request #1 from w3schools-test/update-readme
836e5bf (origin/update-readme, update-readme) Updated readme for GitHub Branches
daf4f7c (origin/html-skeleton, html-skeleton) Updated index.html with basic meta
facaeae (gh-page/master) Merge branch 'master' of https://github.com/w3schools-test/hello-world
e7de78f Updated index.html. Resized image
5a04b6f Updated README.md with a line about focus
d29d69f Updated README.md with a line about GitHub
e0b6038 merged with hello-world-images after fixing conflicts
1f1584e added new image
dfa79db updated index.html with emergency fix
0312c55 Added image to Hello World
09f4acd Updated index.html with a new line
221ec6e First release of Hello World!
```

We want to revert to the previous `commit`: `52418f7 (HEAD -> master) Just a regular update, definitely no accidents here...`, and we see that it is the latest `commit`.

## Git Revert HEAD

We revert the latest `commit` using git `revert HEAD` (`revert` the latest change, and then `commit`), adding the option `--no-edit` to skip the commit message editor (getting the default `revert` message):

```
git revert HEAD --no-edit
[master e56ba1f] Revert "Just a regular update, definitely no accidents here..."
 Date: Thu Apr 22 10:50:13 2021 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 img_hello_git.jpg
```

Now let's check the `log` again:

```
git log --oneline
e56ba1f (HEAD -> master) Revert "Just a regular update, definitely no accidents here..."
52418f7 Just a regular update, definitely no accidents here...
9a9add8 (origin/master) Added .gitignore
81912ba Corrected spelling error
3fdaa5b Merge pull request #1 from w3schools-test/update-readme
836e5bf (origin/update-readme, update-readme) Updated readme for GitHub Branches
daf4f7c (origin/html-skeleton, html-skeleton) Updated index.html with basic meta
facaeae (gh-page/master) Merge branch 'master' of https://github.com/w3schools-test/hello-world
e7de78f Updated index.html. Resized image
5a04b6f Updated README.md with a line about focus
d29d69f Updated README.md with a line about GitHub
e0b6038 merged with hello-world-images after fixing conflicts
1f1584e added new image
dfa79db updated index.html with emergency fix
0312c55 Added image to Hello World
09f4acd Updated index.html with a new line
221ec6e First release of Hello World!
```

**Note:** To revert to earlier commits, use `git revert HEAD~*x*` (*`x`* being a number. 1 going back one more, 2 going back two more, etc.)

---

## Git Reset

`reset` is the command we use when we want to move the repository back to a previous `commit`, discarding any changes made after that `commit`.

**Warning:** Messing with the `commit` history of a repository can be dangerous. It is usually ok to make these kinds of changes to your own local repository. However, you should avoid making changes that rewrite history to `remote` repositories, especially if others are working with them.

Even though the commits are no longer showing up in the `log`, it is not removed from Git.

If you know the commit hash you can `reset` to it:

```
git reset e56ba1f
```

---

## Git commit --amend

`commit --amend` is used to modify the most recent `commit`.

It combines changes in the `staging environment` with the latest `commit`, and creates a new `commit`.

This new `commit` replaces the latest `commit` entirely.

## Git Amend Commit Message

One of the simplest things you can do with `--amend` is to change a `commit` message.

Let's update the `README.md` and `commit`:

```
git commit -m "Adding plines to reddme"
[master 07c5bc5] Adding plines to reddme
 1 file changed, 3 insertions(+), 1 deletion(-)
```

Now let's check the `log`:

```
git log --oneline
07c5bc5 (HEAD -> master) Adding plines to reddme
9a9add8 (origin/master) Added .gitignore
81912ba Corrected spelling error
3fdaa5b Merge pull request #1 from w3schools-test/update-readme
836e5bf (origin/update-readme, update-readme) Updated readme for GitHub Branches
daf4f7c (origin/html-skeleton, html-skeleton) Updated index.html with basic meta
facaeae (gh-page/master) Merge branch 'master' of https://github.com/w3schools-test/hello-world
e7de78f Updated index.html. Resized image
5a04b6f Updated README.md with a line about focus
d29d69f Updated README.md with a line about GitHub
e0b6038 merged with hello-world-images after fixing conflicts
1f1584e added new image
dfa79db updated index.html with emergency fix
0312c55 Added image to Hello World
09f4acd Updated index.html with a new line
221ec6e First release of Hello World!
```

Oh no! the `commit` message is full of spelling errors. Embarrassing. Let's `amend` that:

```
git commit --amend -m "Added lines to README.md"
[master eaa69ce] Added lines to README.md
 Date: Thu Apr 22 12:18:52 2021 +0200
 1 file changed, 3 insertions(+), 1 deletion(-))
```

And re-check the `log`:

```
git log --oneline
eaa69ce (HEAD -> master) Added lines to README.md
9a9add8 (origin/master) Added .gitignore
81912ba Corrected spelling error
3fdaa5b Merge pull request #1 from w3schools-test/update-readme
836e5bf (origin/update-readme, update-readme) Updated readme for GitHub Branches
daf4f7c (origin/html-skeleton, html-skeleton) Updated index.html with basic meta
facaeae (gh-page/master) Merge branch 'master' of https://github.com/w3schools-test/hello-world
e7de78f Updated index.html. Resized image
5a04b6f Updated README.md with a line about focus
d29d69f Updated README.md with a line about GitHub
e0b6038 merged with hello-world-images after fixing conflicts
1f1584e added new image
dfa79db updated index.html with emergency fix
0312c55 Added image to Hello World
09f4acd Updated index.html with a new line
221ec6e First release of Hello World!
```

## Git Amend Files

Adding files with `--amend` works the same way as above. Just add them to the `staging environment` before committing.











![image-20240118152138155](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240118152138155.png)
