
# Git learning


Tags：git，markdown


---


使用 *markdown* 记录 **git** 的学习过程, 原始学习资料见[Pro git](http://git-scm.com/book/zh/v1)


[toc]


## 1. 起步


Git实现目标
* 速度
* 简单的设计
* 对非线性开发模式的强力支持（允许上千个并行开发的分支）
* 完全分布式
* 有能力高效管理类似 Linux  内核一样的超大规模项目（速度和数据量）

Git优秀之处：
- 直接记录快照，而非差异比较
- 近乎所有操作都是本地执行
- 时刻保持数据完整性
- 多数操作仅添加数据

Mac上安装git和配置

```
$ brew install git
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
$ git config --global core.editor emacs
$ git config --global merge.tool vimdiff
```

查看所有配置，或某一项

```
$ git config --list
$ git config user.name
```

引用总结：

> 至此，你该对 Git 有了点基本认识，包括它和以前你使用的 CVCS 之间的差别。现在，在你的系统上应该已经装好了 Git，设置了自己的名字和电邮。接下来让我们继续学习 Git 的基础知识。


## 2. Git基础

第一个git命令：`git init`, 初始化git仓库。使用`git add`对文件进行跟踪：

```
$ git add *.c
$ git add README
$ git commit -m 'initial project version'
```

从现有仓库克隆

```
$ git clone git://github.com/schacon/grit.git
```

检查当前文件状态

```
$ git status
On branch master
nothing to commit, working directory clean
```

修改`.gitignore`，设置忽略的文件模式，例如

```
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a
# 但 lib.a 除外
!lib.a
# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO
# 忽略 build/ 目录下的所有文件
build/
# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

查看已暂存和未暂存的更新

```
$ git status
$ git diff
$ git diff --staged
```

删除，仅删除仓库和移动

```
$ git rm grit.gemspec
$ git rm --cached readme.txt
$ git mv README.txt README
```

查看提交历史

```
$ git log
$ git log -p -2
```

其他格式（单词层面，行数统计，自定义1,2,3）

```
$ git log -U1 --word-diff
$ git log --stat
$ git log --pretty=oneline
$ git log --pretty=format:"%h - %an, %ar : %s"
$ git log --pretty=format:"%h %s" --graph
```

使用图形化工具查阅提交历史: `gitk`

修改上一次提交

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

取消对文件的修改

```
git checkout -- benchmarks.rb
```

取消已经暂存的文件

```
$ git add -A
$ git reset HEAD
```

记住，任何已经提交到 Git 的都可以被恢复。即便在已经删除的分支中的提交，或者用 --amend 重新改写的提交，都可以被恢复（关于数据恢复的内容见第九章）。所以，你可能失去的数据，仅限于没有提交过的，对 Git 来说它们就像从未存在过一样。

### 远程仓库
远程仓库是指托管在网络上的项目仓库，可能会有好多个，其中有些你只能读，另外有些可以写。同他人协作开发某个项目时，需要管理这些远程仓库，以便推送或拉取数据，分享各自的工作进展。 管理远程仓库的工作，包括添加远程库，移除废弃的远程库，管理各式远程库分支，定义是否跟踪这些分支，等等。

查看当前的远程库 (显示对应的克隆地址)

```
$ git remote
$ git remote -v
```

添加远程仓库 `git remote add [shortname] [url]`

```
$ git remote add pb git://github.com/paulboone/ticgit.git
$ git remote -v
$ git fetch pb
```

推送数据到远程仓库`git push [remote-name] [branch-name]`
查看远程仓库信息 `git remote show [remote-name]`

```
$ git remote show pb
$ git remote show origin
```

远程仓库的删除和重命名

```
$ git remote rename pb paul
$ git remote rm paul
```

### 标签
同大多数 VCS 一样，Git 也可以对某一时间点上的版本打上标签。Git 使用的标签有两种类型：轻量级的（lightweight）和含附注的（annotated）。轻量级标签就像是个不会变化的分支，实际上它就是个指向特定提交对象的引用。而含附注标签，实际上是存储在仓库中的一个独立对象，它有自身的校验和信息，包含着标签的名字，电子邮件地址和日期，以及标签说明，

列显已有的标签 (字母排序)
```
git tag
```

特定的搜索模式 
```
$ git tag -l
```

含附注的标签
```
$ git tag -a v1.4 -m 'my version 1.4'
```

签署标签
如果你有自己的私钥，还可以用 GPG 来签署标签

```
$ git tag -s v1.5 -m 'my signed 1.5 tag'
You need a passphrase to unlock the secret key for
user: "Scott Chacon <schacon@gee-mail.com>"
1024-bit DSA key, ID F721C45A, created 2009-02-09
```

验证标签
可以使用 `git tag -v [tag-name]` （译注：取 verify 的首字母）的方式验证已经签署的标签。此命令会调用 GPG 来验证签名，所以你需要有签署者的公钥，存放在 keyring 中，才能验证：

```
$ git tag -v v1.4.2.1
object 883653babd8ee7ea23e6a5c392bb739348b1eb61
type commit
tag v1.4.2.1
tagger Junio C Hamano <junkio@cox.net> 1158138501 -0700

GIT 1.4.2.1

Minor fixes since 1.4.2, including git-mv and git-http with alternates.
gpg: Signature made Wed Sep 13 02:08:25 2006 PDT using DSA key ID F3119B9A
gpg: Good signature from "Junio C Hamano <junkio@cox.net>"
gpg:                 aka "[jpeg image of size 1513]"
Primary key fingerprint: 3565 2A26 2040 E066 C9A7  4A7D C0C6 D9A4 F311 9B9A
```

轻量级标签
轻量级标签实际上就是一个保存着对应提交对象的校验和信息的文件。要创建这样的标签，一个 `-a`，`-s` 或 `-m` 选项都不用，直接给出标签名字即可：

```
$ git tag v1.4-lw
$ git tag
$ git tag show v1.4-lw
```

后期加注标签
我们忘了在提交 “updated rakefile” 后为此项目打上版本号 v1.2，没关系，现在也能做。只要在打标签的时候跟上对应提交对象的校验和（或前几位字符）即可：

```
$ git log --pretty=oneline
$ git tag -a v1.2 9fceb02
```

分享标签
只有通过显式命令才能分享标签到远端仓库:

```
$ git push origin v1.5
```

如果要一次推送所有本地新增的标签上去

```
$ git push origin --tags
```

### 技巧和窍门
Git 命令别名

```
$ git config --global alias.co checkout
$ git co
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.unstage 'reset HEAD --'
$ git config --global alias.last 'log -1 HEAD'
$ git config --global alias.visual '!gitk'
```

## 3. 分支
Git 的分支可谓是难以置信的轻量级，它的新建操作几乎可以在瞬间完成，并且在不同分支间切换起来也差不多一样快。和许多其他版本控制系统不同，Git 鼓励在工作流程中频繁使用分支与合并，哪怕一天之内进行许多次都没有关系。

### 3.1 Git 分支 - 何谓分支

Git 中的分支，就是从某个提交对象往回看的历史。Git 会使用 master 作为分支的默认名字。HEAD 的特别指针，指向你正在工作中的本地分支的指针（译注：将 HEAD 想象为当前分支的别名。）。

创建分支，并切换：

```
$ git branch testing
$ git checkout testing
```

> 由于 Git 中的分支实际上仅是一个包含所指对象校验和（40 个字符长度 SHA-1 字串）的文件，所以创建和销毁一个分支就变得非常廉价。说白了，新建一个分支就是向一个文件写入 41 个字节（外加一个换行符）那么简单，当然也就很快了。

### 3.2 分支的新建与合并

新建并切换到该分支：

```
$ git checkout -b iss53
Switched to a new branch 'iss53'
```

### 3.3 分支的衍合

把一个分支中的修改整合到另一个分支的办法有两种：`merge` 和 `rebase`。衍合（`rebase`）：先在自己的一个分支里进行开发，当准备向主项目提交补丁的时候，根据最新的 origin/master 进行一次衍合操作然后再提交，这样维护者就不需要做任何整合工作。


衍合的风险
> 一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行衍合操作。



## 4. 服务器上的Git
## 5. 分布式Git
## 6. Git工具
## 7. 自定义Git
## 8. Git与其他系统
## 9. Git内部原理
