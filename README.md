# Git_Study

        
------        
        
### 作者：冰红茶  
### 参考书籍：《Git 版本控制管理》 Jon Loeliger   
            
------    
            
        

  版本控制是一个非常重要而且非常常用的技术，我之前用的比较多的都是在Windows平台上的eclipse和GitHub。不过后面由于需要把平台都迁移到Linux上，所以在Linux平台上的版本控制显得非常的重要^_ ^
  
## 目录

## [一、简介](#1)
### [1.1 背景](#1.1)
## [二、起步](#2)
### [2.1 Git命令行](#2.1)
### [2.2 Git使用快速入门](#2.2)   
### [2.3 配置文件](#2.3)  
## [三、基本的git概念和操作](#3)
### [3.1 基本概念](#3.1)
### [3.2 基本操作](#3.2)  
## [四、分支](#4)
### [4.1 基本概念](#4.1)
### [4.2 基本操作](#4.2) 
## [五、合并](#5)
### [5.1 基本概念](#5.1)
### [5.2 基本操作](#5.2) 
## [六、远程版本库](#6)
### [6.1 基本概念](#6.1)
### [6.2 基本操作](#6.2)
### [6.3 最佳实践](#6.3)   
------      
        
        
<h2 id='1'> 一、简介</h2>
<h3 id='1.1'>1.1 背景</h3>  
        
#### 1) VCS
> - 一个可以管理和追踪软件代码或者其他类似内容的不同版本的工具，通常称为版本控制系统VCS，version control system
> - Git是由Linux之父Linus Torvalds发明，起初是为了方便管理Linux内核的开发工作
> - 在Git之前用得最多的是Bitkeeper，然而在2005年春天Bitkeeper对免费版功能做出了限制，是大家觉得使用Bitkeeper并不是长久之计
        
------      
        
               
<h2 id='2'> 二、起步</h2>
<h3 id='2.1'>2.1 Git命令行</h3>  
        
#### 1) 基本命令与规则
> - git和git --version
                
                [lvhongbin@localhost ~]$ git --version
                git version 1.8.3.1

                [lvhongbin@localhost ~]$ git
                usage: git [--version] [--help] [-c name=value]
                           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
                           [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
                           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
                           <command> [<args>]

                The most commonly used git commands are:
                   add        Add file contents to the index
                   bisect     Find by binary search the change that introduced a bug
                   branch     List, create, or delete branches
                   checkout   Checkout a branch or paths to the working tree
                   clone      Clone a repository into a new directory
                   commit     Record changes to the repository
                   diff       Show changes between commits, commit and working tree, etc
                   fetch      Download objects and refs from another repository
                   grep       Print lines matching a pattern
                   init       Create an empty Git repository or reinitialize an existing one
                   log        Show commit logs
                   merge      Join two or more development histories together
                   mv         Move or rename a file, a directory, or a symlink
                   pull       Fetch from and merge with another repository or a local branch
                   push       Update remote refs along with associated objects
                   rebase     Forward-port local commits to the updated upstream head
                   reset      Reset current HEAD to the specified state
                   rm         Remove files from the working tree and from the index
                   show       Show various types of objects
                   status     Show the working tree status
                   tag        Create, list, delete or verify a tag object signed with GPG

                'git help -a' and 'git help -g' lists available subcommands and some
                concept guides. See 'git help <command>' or 'git help <concept>'
                to read about a specific subcommand or concept.
                
> - Git的命令有长短的选项
> - 短的 -character 操作数
> - 长的是 --word=操作数
        git commit -m "Fixed a type."
        git commit --message="Fixed a type."
> - 只有 极少数的命令用于git，大多数是用于子命令
> - "裸双破折号" 用来分离一系列参数，比如用来分离命令行的控制部分和操作数部分。这是为什么呢？这是 因为有的标签跟你的文件的名字重复了，所以为了区分，使用了"裸双破折号" 
        
                # Checkout the tag named "main.c"
                $ git checkout main.c

                # Checkout the file named "main.c"
                $ git checkout -- main.c

        
<h3 id='2.2'>2.2 Git使用快速入门</h3>  
        
#### 1) 创建初始版本库
> - 在目标目录下使用git init创建初始VCS目录./.git 
        
                [lvhongbin@localhost ~]$ mkdir ./git/website && cd ./git/website
                [lvhongbin@localhost website]$ touch ./index.html
                [lvhongbin@localhost website]$ echo 'My website is alive!'> index.html

                # Git并不关心你是否从一个完全空白的目录还是一个装满文件的目录开始
                # 此时Git创建了一个隐藏的目录./.git
                [lvhongbin@localhost website]$ git init
                Initialized empty Git repository in /home/lvhongbin/git/website/.git/
                [lvhongbin@localhost website]$ 
#### 2) 将文件添加到版本库中
> - 使用命令git add index.html
> - 使用git add . 命令可以让Git把当前目录及子目录中的文件都添加到版本库中
> - git把add和commit这两步分开，以避免频繁的变化
> - git status 命令显示add和commit之间的状态
> - git commit -m "日志消息" --author="LvHongbin <hblvsjtu@163.com\>" 一条完全限定的git commit必须提供日志消息和作者
> - export GIT_EDITOR=vim 在commit期间git自动打开指定的编辑器进行消息的交互
        
                [lvhongbin@localhost website]$ git add ./index.html
                [lvhongbin@localhost website]$ git status
                # On branch master
                #
                # Initial commit
                #
                # Changes to be committed:
                #   (use "git rm --cached <file>..." to unstage)
                #
                #   new file:   index.html
                #
                [lvhongbin@localhost website]$ git commit -m "Initial contents of public_html" --author="LvHongbin <hblvsjtu@163.com>"
                [master (root-commit) 2d6c3be] Initial contents of public_html
                 Author: LvHongbin <hblvsjtu@163.com>
                 Committer: LvHongbin <lvhongbin@localhost.localdomain>
                Your name and email address were configured automatically based
                on your username and hostname. Please check that they are accurate.
                You can suppress this message by setting them explicitly:

                    git config --global user.name "Your Name"
                    git config --global user.email you@example.com

                After doing this, you may fix the identity used for this commit with:

                    git commit --amend --reset-author

                 1 file changed, 1 insertion(+)
                 create mode 100644 index.html

                # 在commit期间git自动打开指定的编辑器进行消息的交互 
                [lvhongbin@localhost website]$ export GIT_EDITOR=vim

                # 再次查看添加文件的变动状态，发现没有改变
                [lvhongbin@localhost website]$ git status
                # On branch master
                nothing to commit, working directory clean              
#### 3) 配置提交作者
> - 如果每次提交都要设置作者就是在太麻烦了，所以有一个指定默认作者的操作。另外也可以使用GIT_AUTHOR_NAME和GIT_AUTHOR_EMAIL
                
                git config user.name "LvHongbin"
                git config user.email "hblvsjtu@163.com"

                # 查看默认配置
                [lvhongbin@localhost website]$ git config -l
                core.repositoryformatversion=0
                core.filemode=true
                core.bare=false
                core.logallrefupdates=true
                user.name=LvHongbin
                user.email=hblvsjtu@163.com

#### 4) 再次提交
> - index.html修改的内容  
                
                [lvhongbin@localhost website]$ vim ./index.html
                [lvhongbin@localhost website]$ cat ./index.html
                <!DOCTYPE html>
                <html>
                    <head>
                        <title>Welcome to my place</title>
                    </head>
                    <body>
                        My website is alive!
                    </body>
                </html> 
> - 查看提交结果
               
                [lvhongbin@localhost website]$ git commit ./index.html
                ############################################################
                # 这是git调用vim作为消息交互的窗口
                    Convert to HTML #这是添加的提交信息
                    # Please enter the commit message for your changes. Lines starting
                    # with '#' will be ignored, and an empty message aborts the commit.
                    # Explicit paths specified without -i nor -o; assuming --only paths...
                    # On branch master
                    # Changes to be committed:
                    #   (use "git reset HEAD <file>..." to unstage)
                    #
                    #       modified:   index.html
                    #
                ############################################################
                [master 79cede2] Convert to HTML
                1 file changed, 9 insertions(+), 1 deletion(-)
#### 5) 查看提交历史和比较提交内容
> - 
                
                # 查看单独提交的历史
                [lvhongbin@localhost website]$ git log
                commit 79cede26fa341dd55432da1d1e2ae7966eb11767
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 22:01:19 2018 +0800

                    Convert to HTML

                commit 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 21:36:25 2018 +0800

                    Initial contents of public_html

                # 查看特定提交码的信息
                [lvhongbin@localhost website]$ git show 79cede26fa341dd55432da1d1e2ae7966eb11767
                commit 79cede26fa341dd55432da1d1e2ae7966eb11767
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 22:01:19 2018 +0800

                    Convert to HTML

                diff --git a/index.html b/index.html
                index 34217e9..daf1ba4 100644
                --- a/index.html
                +++ b/index.html
                @@ -1 +1,9 @@
                -My website is alive!
                +<!DOCTYPE html>
                +<html>
                +    <head>
                +        <title>Welcome to my place</title>
                +    </head>
                +    <body>
                +       My website is alive!
                +    </body>
                +</html>

                # 查看当前开发分支的简介单行摘要
                [lvhongbin@localhost website]$ git show-branch --more=10
                [master] Convert to HTML
                [master^] Initial contents of public_html

                # 比较不同提交码下的提交差别
                # 按照惯例旧的在前，新的在后，这样比较出来的结果，旧的前面是(-)号，新的是(+)号
                [lvhongbin@localhost website]$ git diff 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1 79cede26fa341dd55432da1d1e2ae7966eb11767
                diff --git a/index.html b/index.html
                index 34217e9..daf1ba4 100644
                --- a/index.html
                +++ b/index.html
                @@ -1 +1,9 @@
                -My website is alive!
                +<!DOCTYPE html>
                +<html>
                +    <head>
                +        <title>Welcome to my place</title>
                +    </head>
                +    <body>
                +       My website is alive!
                +    </body>
                +</html>
#### 6) 版本库的文件删除和重命名
> - 删除命令
        
                git rm remove.html
                git commit -m "Remove remove.html"
> - 范例
                
                # 范例
                [lvhongbin@localhost website]$ touch remove.html
                [lvhongbin@localhost website]$ git add ./remove.html
                [lvhongbin@localhost website]$ git commit -m "add remove.html"
                [master d187d87] add remove.html
                 1 file changed, 0 insertions(+), 0 deletions(-)
                 create mode 100644 remove.html
                [lvhongbin@localhost website]$ git rm ./remove.html
                rm 'remove.html'
                [lvhongbin@localhost website]$ git commit -m "remove remove.html"
                [master 11d9eab] remove remove.html
                 1 file changed, 0 insertions(+), 0 deletions(-)
                 delete mode 100644 remove.html
                [lvhongbin@localhost website]$ git status
                # On branch master
                nothing to commit, working directory clean
> - 重命名命令
        
                git mv mv1.html mv2.html
                git commit -m "Rename mv1.html to mv2.html"
#### 7) 版本库的克隆
> - 使用命令：git clone 旧的文件目录 新的文件目录   
        
                [lvhongbin@localhost git]$ git clone website website_clone
                Cloning into 'website_clone'...
                done.

                # 比较两个文件的不同
                Only in website/.git: COMMIT_EDITMSG
                diff -r website/.git/config website_clone/.git/config
                6,8c6,11
                < [user]
                <   name = LvHongbin
                <   email = hblvsjtu@163.com
                ---
                > [remote "origin"]
                >   url = /home/lvhongbin/git/website
                >   fetch = +refs/heads/*:refs/remotes/origin/*
                > [branch "master"]
                >   remote = origin
                >   merge = refs/heads/master
                Binary files website/.git/index and website_clone/.git/index differ
                diff -r website/.git/logs/HEAD website_clone/.git/logs/HEAD
                1,4c1
                < 0000000000000000000000000000000000000000 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1 LvHongbin <lvhongbin@localhost.localdomain> 1527687385 +0800    commit (initial): Initial contents of public_html
                < 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1 79cede26fa341dd55432da1d1e2ae7966eb11767 LvHongbin <hblvsjtu@163.com> 1527688879 +0800   commit: Convert to HTML
                < 79cede26fa341dd55432da1d1e2ae7966eb11767 d187d87321d0f05b7589e5519950d7d54f9ada67 LvHongbin <hblvsjtu@163.com> 1527690906 +0800   commit: add remove.html
                < d187d87321d0f05b7589e5519950d7d54f9ada67 11d9eab789a7cc1f25d30a3a779b5e5bd0653940 LvHongbin <hblvsjtu@163.com> 1527690949 +0800   commit: remove remove.html
                ---
                > 0000000000000000000000000000000000000000 11d9eab789a7cc1f25d30a3a779b5e5bd0653940 LvHongbin <lvhongbin@localhost.localdomain> 1527692009 +0800    clone: from /home/lvhongbin/git/website
                diff -r website/.git/logs/refs/heads/master website_clone/.git/logs/refs/heads/master
                1,4c1
                < 0000000000000000000000000000000000000000 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1 LvHongbin <lvhongbin@localhost.localdomain> 1527687385 +0800    commit (initial): Initial contents of public_html
                < 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1 79cede26fa341dd55432da1d1e2ae7966eb11767 LvHongbin <hblvsjtu@163.com> 1527688879 +0800   commit: Convert to HTML
                < 79cede26fa341dd55432da1d1e2ae7966eb11767 d187d87321d0f05b7589e5519950d7d54f9ada67 LvHongbin <hblvsjtu@163.com> 1527690906 +0800   commit: add remove.html
                < d187d87321d0f05b7589e5519950d7d54f9ada67 11d9eab789a7cc1f25d30a3a779b5e5bd0653940 LvHongbin <hblvsjtu@163.com> 1527690949 +0800   commit: remove remove.html
                ---
                > 0000000000000000000000000000000000000000 11d9eab789a7cc1f25d30a3a779b5e5bd0653940 LvHongbin <lvhongbin@localhost.localdomain> 1527692009 +0800    clone: from /home/lvhongbin/git/website
                Only in website_clone/.git/logs/refs: remotes
                Only in website_clone/.git: packed-refs
                Only in website_clone/.git/refs: remotes

        
<h3 id='2.3'>2.3 配置文件</h3>  
        
#### 1) .git/config
> - 主要用来配置一些默认选项，优先级最高，可以使用--file选项来修改
        
                [lvhongbin@localhost website]$ cat ./.git/config
                [core]
                    repositoryformatversion = 0
                    filemode = true
                    bare = false
                    logallrefupdates = true
                [user]
                    name = LvHongbin
                    email = hblvsjtu@163.com
#### 2) ~/.gitconfig
> - 用户特定的配置设置，优先级次之，可以使用--global选项来修改
        
                git config --global user.name "LvHongbin"
                git config --global user.email "hblvsjtu@163.com"
#### 3) /etc/gitconfig
> -  这是系统范围的配置设置，优先级最低，可以使用--system选项来修改
#### 4) 移除设置的命令
> - --unset
                
                # 类似javascript的user对象
                git config --unset --global user.email     
#### 5) 配置别名
> - alias 如：
             
                git config --global alias.rmovefile "git rm '文件名'"

        
------      
        
        
<h2 id='3'>三、基本的git概念</h2>
<h3 id='3.1'>3.1 基本概念</h3>  
        
#### 1) 版本库
> - repository
> - 两个数据结构：对象库object store和索引index
> - 对象库包含原始数据和所有日志消息，作者信息，日期以及其他用来重建项目任意版本或者分支的信息，包括四种原子对象：
>> - 块对象blob 二进制大对象binary large object，保存一个文件的数据，但是并不包含任何关于该文件的元数据
>> - 目录树对象tree 包含所有文件的元数据 
>> - 提交对象commit 保存版本库中每一次变化的元数据，包括作者，提交者，提交日期和日志消息。每一个提交对象都指向一个目录树对象
>> - 标签对象tag 是一个可以任意被指定的且人类可读的名字，比如虽然79cede26fa341dd55432da1d1e2ae7966eb11767是一个确切的且定义好的提交，但是可以给他指定另外一个标签，如：Version-1.0
                git tag -m "Tag version 1.0" V1.0 提交码前面7位
                
                # 根据提交吗的前7位创建标签对象
                [lvhongbin@localhost website]$ git tag -m "The first tag" V1.0 2d6c3be

                # 根据标签对象的SHA1值查看提交信息
                [lvhongbin@localhost website]$ git rev-parse V1.0
                8b636d23d24b2306e56747dd2dff459ebbb296e9
                [lvhongbin@localhost website]$ git cat-file -p 8b636d2
                object 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                type commit
                tag V1.0
                tagger LvHongbin <hblvsjtu@163.com> 1527734156 +0800

                The first tag

                # 运用标签对象查看提交信息
                [lvhongbin@localhost website]$ git show V1.0
                tag V1.0
                Tagger: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 10:35:56 2018 +0800

                The first tag

                commit 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 21:36:25 2018 +0800

                    Initial contents of public_html

                diff --git a/index.html b/index.html
                new file mode 100644
                index 0000000..34217e9
                --- /dev/null
                +++ b/index.html
                @@ -0,0 +1 @@
                +My website is alive!

                # 运用标签对象查看提交信息
                [lvhongbin@localhost website]$ git log V1.0
                commit 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 21:36:25 2018 +0800

                    Initial contents of public_html

                # 运用标SHA1值查看提交信息
                [lvhongbin@localhost website]$ git show 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                commit 2d6c3bee2137fabb3d7cde090ddc7a38e33a79c1
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Wed May 30 21:36:25 2018 +0800

                    Initial contents of public_html

                diff --git a/index.html b/index.html
                new file mode 100644
                index 0000000..34217e9
                --- /dev/null
                +++ b/index.html
                @@ -0,0 +1 @@
                +My website is alive!

> - 索引index在合并merge，允许管理，检查和同时操作同一个文件的多个版本祈祷非常重要的作用 
> - 对象库中的每一个对象都有一个唯一的名号曾，这个名称事项对象的内容应用SHA1得到的[SHA1散列值](https://baike.baidu.com/item/SHA1/8812671?fr=aladdin)
> - 其实git commit 包含着两个步骤: 
        
                echo -n "commit a file that says hello\n" | git commit-tree $(git write-tree)
> - 查看提交信息
        
                git cat-file -p 提交码前面7位
>>>>>> ![图3-1 二次提交的Git对象.jpg](https://github.com/hblvsjtu/Git_Study/blob/master/picture/%E5%9B%BE3-1%20%E4%BA%8C%E6%AC%A1%E6%8F%90%E4%BA%A4%E7%9A%84Git%E5%AF%B9%E8%B1%A1.jpg?raw=true)
        
<h3 id='3.2'>3.2 基本操作</h3>  
        
#### 1) 添加文件
> - git add 文件或者目录
> - 每个添加的文件的全部内容都将被复制到对象库中，并按文件的SHA1名来索引。暂存一个文件也称为缓存caching一个文件，或者叫“把文件放进索引”
#### 2) 简单查看文件列表和SHA1值
> - git ls-files --stage
        
                [lvhongbin@localhost website]$ git ls-files --stage
                100644 daf1ba4fdc1246ef1624f8a3f46d9e08f319b920 0   index.html
#### 3) 提交
> - 三种状态：文件未添加，文件未提交，文件未更新 
                
                # 三种状态：文件未添加（或者说是未追踪），文件未提交，文件未更新
                [lvhongbin@localhost website]$ vim index.html
                [lvhongbin@localhost website]$ touch newfilenotsummit.txt
                [lvhongbin@localhost website]$ touch newfilenotadd.txt
                [lvhongbin@localhost website]$ git add newfilenotsummit.txt
                
                [lvhongbin@localhost website]$ git status
                # On branch master
                # Changes to be committed:
                #   (use "git reset HEAD <file>..." to unstage)
                #
                #   new file:   newfilenotsummit.txt
                #
                # Changes not staged for commit:
                #   (use "git add <file>..." to update what will be committed)
                #   (use "git checkout -- <file>..." to discard changes in working directory)
                #
                #   modified:   index.html
                #
                # Untracked files:
                #   (use "git add <file>..." to include in what will be committed)
                #
                #   newfilenotadd.txt
                [lvhongbin@localhost website]$
> - git commit --all 提交 文件未提交，文件未更新这两种状态下的所有文件，但不包括文件未添加（或者说是未追踪）
                
                # 提交 文件未提交，文件未更新这两种状态下的所有文件
                [lvhongbin@localhost website]$ git commit --all
                [master 0a4d3f1] execute commit --all command
                 2 files changed, 1 insertion(+)
                 create mode 100644 newfilenotsummit.txt
                [lvhongbin@localhost website]$ git status
                # On branch master
                # Untracked files:
                #   (use "git add <file>..." to include in what will be committed)
                #
                #   newfilenotadd.txt
                nothing added to commit but untracked files present (use "git add" to track)
#### 4) 删除
> - git rm 
> - 从索引和工作目录中删除一个文件，与普通的rm不同，普通的rm只会直接从目录中删除文件，但是不会删除该文件的索引 
> - git rm --cached 文件名 删除索引中的文件并把它保留在工作目录中 并把文件标记为为追踪，即未添加的状态
#### 5) 重命名
> - git mv 更改索引，并显示改名字的记录
> - 其实以下两个步骤是等价的
        
                mv stuff newstuff
                git rm stuff
                git add newstuff

                # 等价于
                git mv stuff newstuff

                [lvhongbin@localhost website]$ touch stuff.txt 

                # 使用第一种的方法
                [lvhongbin@localhost website]$ git add stuff.txt && git commit -m "before change name" stuff.txt
                [master 469e38a] before change name
                 1 file changed, 0 insertions(+), 0 deletions(-)
                 create mode 100644 stuff.txt

                [lvhongbin@localhost website]$ mv stuff.txt newstuff.txt
                [lvhongbin@localhost website]$ git rm stuff.txt
                rm 'stuff.txt'
                [lvhongbin@localhost website]$ git add newstuff.txt
                [lvhongbin@localhost website]$ git status
                # On branch master
                # Changes to be committed:
                #   (use "git reset HEAD <file>..." to unstage)
                #
                #   renamed:    stuff.txt -> newstuff.txt
                #
                # Untracked files:
                #   (use "git add <file>..." to include in what will be committed)
                #
                #   newfilenotadd.txt

                # 使用第二种的方法
                [lvhongbin@localhost website]$ git mv newstuff.txt newnewstuff.txt
                [lvhongbin@localhost website]$ git status
                # On branch master
                # Changes to be committed:
                #   (use "git reset HEAD <file>..." to unstage)
                #
                #   renamed:    stuff.txt -> newnewstuff.txt
                #
                # Untracked files:
                #   (use "git add <file>..." to include in what will be committed)
                #
                #   newfilenotadd.txt
> - 查看回溯历史 
>> - git log --follow 文件名
>> - git cat-file方式
>> - git show方式
        
                [lvhongbin@localhost website]$ git log newnewstuff.txt
                commit e0766fc70fdc25c7b74322b872b3d1ed32bca7d9
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 11:41:45 2018 +0800

                    has changed filename

                # 查看回溯历史   
                [lvhongbin@localhost website]$ git log --follow newnewstuff.txt
                commit e0766fc70fdc25c7b74322b872b3d1ed32bca7d9
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 11:41:45 2018 +0800

                    has changed filename

                commit 469e38ae5cba93289a35d174e601416be7fa185d
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 11:36:39 2018 +0800

                    before change name

                commit 0a4d3f1a2f913e725ed8c4e2bf9afa1cb849fc26
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 11:14:06 2018 +0800

                    execute commit --all command

                # git cat-file方式
                [lvhongbin@localhost website]$ git cat-file -p  469e38a
                tree a5801629c277304ef202fd904337b4f3a11d1102
                parent 0a4d3f1a2f913e725ed8c4e2bf9afa1cb849fc26
                author LvHongbin <hblvsjtu@163.com> 1527737799 +0800
                committer LvHongbin <hblvsjtu@163.com> 1527737799 +0800

                before change name

                # git show方式
                [lvhongbin@localhost website]$ git show 469e38a
                commit 469e38ae5cba93289a35d174e601416be7fa185d
                Author: LvHongbin <hblvsjtu@163.com>
                Date:   Thu May 31 11:36:39 2018 +0800

                    before change name

                diff --git a/stuff.txt b/stuff.txt
                new file mode 100644
                index 0000000..e69de29

        
------      
        
        
<h2 id='4'>四、分支</h2>
<h3 id='4.1'>4.1 基本命令</h3>  
        
#### 1) 创建分支 
> - git branch {branch} {starting-commit}  
> - 命名方式最好以目录的形式 如test/test1
> - 默认是从最近一次提交作为分支的开始
> - 如果是想修复某一个bug，可以从指定的提交开始
        
                [lvhongbin@localhost website]$ git show-branch
                [master] has changed filename

                # commit 0a4d3f1a2f913e725ed8c4e2bf9afa1cb849fc26
                # Author: LvHongbin <hblvsjtu@163.com>
                # Date:   Thu May 31 11:14:06 2018 +0800
                # execute commit --all command
                [lvhongbin@localhost website]$ git branch test/test1 0a4d3f1
                
#### 2) 列出分支名 
> - git branch       
        
                [lvhongbin@localhost website]$ git branch
                * master
                  test/test1
#### 3) 查看分支
> - git show-branch {branchName}
        
                [lvhongbin@localhost website]$ git show-branch
                * [master] has changed filename
                 ! [test/test1] execute commit --all command
                --
                *  [master] has changed filename
                *  [master^] before change name
                *+ [test/test1] execute commit --all command
>>>>>> ![图4-1 分支查看.jpg]()
        
#### 4) 工作分支的检出（或者说是转移）
> - git checkout {branchName}
> - 可以明显看出来星号*已经转移到指定的分支了 
        
                [lvhongbin@localhost website]$ git branch
                * master
                  test/test1
                [lvhongbin@localhost website]$ git checkout test/test1
                Switched to branch 'test/test1'
                [lvhongbin@localhost website]$ git branch
                  master
                * test/test1
> - 创建并快速检出 git checkout -b test/test3
        
                [lvhongbin@localhost website]$ git checkout -b test/test3
                M   mergeCheckoutFile.txt
                Switched to a new branch 'test/test3'
            
                [lvhongbin@localhost website]$ git branch
                  master
                  test/test1
                  test/test2
                * test/test3
> - 当有未提交的更改时发生检出，此时git会提示错误。但是第一次创建文件时候的未提交不算，从第二次修改未提交后发生检出，则报错，以此最大限度保证修改被保存下来
> - 当然，如果你真的不介意数据的丢失，可以采取强制的手段让他检出 -f
> - 对于文件未添加状态的文件，检出的时候不加理会
        
                [lvhongbin@localhost website]$ touch newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ git add newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ git checkout master
                A   newBranchNotCommitFile.txt
                Switched to branch 'master'
                [lvhongbin@localhost website]$ git checkout test/test1
                A   newBranchNotCommitFile.txt
                Switched to branch 'test/test1'
                [lvhongbin@localhost website]$ git commit
                [test/test1 d61f018] test/test1 CommitFile.txt
                 1 file changed, 0 insertions(+), 0 deletions(-)
                 create mode 100644 newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ vim newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ git checkout master
                error: Your local changes to the following files would be overwritten by checkout:
                    newBranchNotCommitFile.txt
                Please, commit your changes or stash them before you can switch branches.
                Aborting

                # 必须commit后才能检出
                [lvhongbin@localhost website]$ git add newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ git checkout master
                error: Your local changes to the following files would be overwritten by checkout:
                    newBranchNotCommitFile.txt
                Please, commit your changes or stash them before you can switch branches.
                Aborting

                # 必须commit后才能检出
                [lvhongbin@localhost website]$ git commit -m "New branch has commited file"
                [test/test1 62837ae] New branch has commited file
                 1 file changed, 1 insertion(+)
                [lvhongbin@localhost website]$ git checkout master
                Switched to branch 'master'
#### 5) 合并变更到不同的分支
> - gei checkout -m {branch}
> - 把修改的内容加入到目标分支中
        
                [lvhongbin@localhost website]$ git branch
                  master
                * test/test1
                [lvhongbin@localhost website]$ git branch test/test2
                [lvhongbin@localhost website]$ git checkout test/test2
                D   mergeCheckoutFile.txt
                Switched to branch 'test/test2'
                [lvhongbin@localhost website]$ touch mergeCheckoutFile.txt
                [lvhongbin@localhost website]$ git add mergeCheckoutFile.txt
                [lvhongbin@localhost website]$ git commit mergeCheckoutFile.txt
                # On branch test/test2
                # Untracked files:
                #   (use "git add <file>..." to include in what will be committed)
                #
                #   newfilenotadd.txt
                nothing added to commit but untracked files present (use "git add" to track)

                [lvhongbin@localhost website]$ vim mergeCheckoutFile.txt
                [lvhongbin@localhost website]$ vim mergeCheckoutFile.txt
                [lvhongbin@localhost website]$ cat mergeCheckoutFile.txt
                mergeCheckoutFile.txt
                [lvhongbin@localhost website]$ git branch
                  master
                  test/test1
                * test/test2
                [lvhongbin@localhost website]$ git checkout -m test/test1
                M   mergeCheckoutFile.txt
                Switched to branch 'test/test1'
                [lvhongbin@localhost website]$ git branch
                  master
                * test/test1
                  test/test2

                [lvhongbin@localhost website]$ git show-branch test/test1
                [test/test1] mergeCheckoutFile
                [lvhongbin@localhost website]$ git show-branch test/test2
                [test/test2] mergeCheckoutFile
                [lvhongbin@localhost website]$ cat mergeCheckoutFile.txt
                mergeCheckoutFile.txt

                # 合并后如果在修改，则不会进行同步修改，只能合并 合并之前的改动
                [lvhongbin@localhost website]$ git checkout test/test2
                M   mergeCheckoutFile.txt
                Switched to branch 'test/test2'
                [lvhongbin@localhost website]$ touch mergeCheckoutFile2.txt
                [lvhongbin@localhost website]$ git add mergeCheckoutFile2.txt
                [lvhongbin@localhost website]$ git commit mergeCheckoutFile2.txt
                [test/test2 dcd7ee8] commit mergeCheckoutFile2.txt
                 1 file changed, 0 insertions(+), 0 deletions(-)
                 create mode 100644 mergeCheckoutFile2.txt
                [lvhongbin@localhost website]$ git show-branch test/test2
                [test/test2] commit mergeCheckoutFile2.txt
                [lvhongbin@localhost website]$ git show-branch test/test1
                [test/test1] mergeCheckoutFile

                [lvhongbin@localhost website]$ git show-branch
                ! [master] has changed filename
                 ! [test/test1] mergeCheckoutFile
                  * [test/test2] commit mergeCheckoutFile2.txt
                ---
                  * [test/test2] commit mergeCheckoutFile2.txt
                 +* [test/test1] mergeCheckoutFile
                 +* [test/test1^] New branch has commited file
                 +* [test/test1~2] test/test1 CommitFile.txt
                +   [master] has changed filename
                +   [master^] before change name
                ++* [test/test1~3] execute commit --all command
#### 6) 删除分支
> - git branch -d {branch} 
> - 删除的分支蹦年是当前的工作分支，如果是则先要切换
> - 删除分支前需要先合并，这是为了保护数据，如果需要强制删除，则可以使用-D
> - 误删分支可以使用git reflog命令来恢复
                
                # 删除的分支蹦年是当前的工作分支，否则报错
                [lvhongbin@localhost website]$ git branch -d master
                error: Cannot delete the branch 'master' which you are currently on.

                #删除分支前需要先合并，这是为了保护数据，如果需要强制删除，则可以使用-D
                [lvhongbin@localhost website]$ git branch -d test/test3
                error: The branch 'test/test3' is not fully merged.
                If you are sure you want to delete it, run 'git branch -D test/test3'.
                [lvhongbin@localhost website]$ git show-branch
                * [master] has changed filename
                 ! [test/test1] mergeCheckoutFile
                  ! [test/test2] git commit --all
                   ! [test/test3] commit mergeCheckoutFile2.txt
                ----
                  +  [test/test2] git commit --all
                  ++ [test/test3] commit mergeCheckoutFile2.txt
                 +++ [test/test1] mergeCheckoutFile
                 +++ [test/test1^] New branch has commited file
                 +++ [test/test1~2] test/test1 CommitFile.txt
                *    [master] has changed filename
                *    [master^] before change name
                *+++ [test/test1~3] execute commit --all command
                [lvhongbin@localhost website]$ git merge test/test3
                Merge made by the 'recursive' strategy.
                 mergeCheckoutFile.txt      | 0
                 mergeCheckoutFile2.txt     | 0
                 newBranchNotCommitFile.txt | 1 +
                 3 files changed, 1 insertion(+)
                 create mode 100644 mergeCheckoutFile.txt
                 create mode 100644 mergeCheckoutFile2.txt
                 create mode 100644 newBranchNotCommitFile.txt
                [lvhongbin@localhost website]$ git branch -d test/test3
                Deleted branch test/test3 (was dcd7ee8).
                [lvhongbin@localhost website]$ git show-branch
                * [master] Merge branch 'test/test3'
                 ! [test/test1] mergeCheckoutFile
                  ! [test/test2] git commit --all
                ---
                -   [master] Merge branch 'test/test3'
                *   [master^] has changed filename
                *   [master~2] before change name
                  + [test/test2] git commit --all
                * + [test/test2^] commit mergeCheckoutFile2.txt
                *++ [test/test1] mergeCheckoutFile


        
------      
        
        
<h2 id='5'>五、合并</h2>
<h3 id='5.1'>5.1 基本概念</h3>  
        
#### 1) 创建分支 
> - 
        
------      
        
        
<h2 id='6'>六、远程版本库 </h2>
<h3 id='6.1'>6.1 基本概念</h3>  
        
#### 1) 裸版本库和开发版本库 
> - 开发版本库用于常规的日常开发，他保持当前分支的概念，并在工作目录中提供检出当前分支的副本 git clone URL
> - 裸版本库没有工作目录，不适合用于正常的开发，也没有检出分支的概念 git clone --bare URL 
> - 发布的版本库应该是裸版本库
        
<h3 id='6.2'>6.2 基本命令</h3>  
        
#### 1) 创建SSH密钥 
> - ssh-keygen -t rsa -C "hblvsjtu@163.com" 创建SSH密钥
> - cat /home/lvhongbin/.ssh/id_rsa.pub 查看秘钥

        
                [lvhongbin@localhost Git_Study]$ ssh-keygen -t rsa -C "hblvsjtu@163.com"
                Generating public/private rsa key pair.
                Enter file in which to save the key (/home/lvhongbin/.ssh/id_rsa): 
                Created directory '/home/lvhongbin/.ssh'.
                Enter passphrase (empty for no passphrase): 
                Enter same passphrase again: 
                Your identification has been saved in /home/lvhongbin/.ssh/id_rsa.
                Your public key has been saved in /home/lvhongbin/.ssh/id_rsa.pub.
                The key fingerprint is:
                SHA256:EUwriLzl+Ynh5hF94WEjnhM7AtWcemRvEvgoZsls1uI hblvsjtu@163.com
                The key's randomart image is:
                +---[RSA 2048]----+
                |    .+ +o        |
                | . o..B .o       |
                | o+oo*+oB        |
                |  @=+++Oo=       |
                | *.o*.BoS        |
                |  E. * =         |
                |    = o          |
                |   o .           |
                |    .            |
                +----[SHA256]-----+

                [root@localhost Git_Study]# cat /home/lvhongbin/.ssh/id_rsa.pub
                ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDIzFf+s+YxALfaXtW7nw2Uxr1h7FzqEgTOEx2k/fGGcMGrCmvbWUX7Cmb3s00sZ4nu6l9etytCRU7xu93m21d/tjnZ0iyCP1rv09+2pS9Rb6ysIOD7Y6Fnoc+Torf3n1rZp4tEufyOO+nMxRmX6rrcizebp9OcLl1ffNRvrD8VCPB1LWcYUPtFphjKDsISRCkXJkJ1HHeIh3SMQfRRKOJa/Wxwvy6TqTe+p4F39AIf0UCEAHqFeUWOMPb6RZ8N5E3xJzEphzQAIyzGSibxxoOq3SbJx5J3f4jM61yfvP/seZHShDwxcu/9m89szMXybor5Swc7RzRAzFClBUhS1DXB hblvsjtu@163.com

                [root@localhost Git_Study]# ssh -T git@github.com
                The authenticity of host 'github.com (13.229.188.59)' can't be established.
                RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
                RSA key fingerprint is MD5:16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
                Are you sure you want to continue connecting (yes/no)? yes
                Warning: Permanently added 'github.com,13.229.188.59' (RSA) to the list of known hosts.
                Hi hblvsjtu! You've successfully authenticated, but GitHub does not provide shell access.

                [root@localhost Git_Study]# git config --global user.email "hblvsjtu@163.com"
                [root@localhost Git_Study]# git config --global user.name "LvHongbin"

#### 2) 远程克隆 
> - git clone URL 
> - 克隆文件夹后最好先同步一下文件 git commit -a
        
                [lvhongbin@localhost git]$ git clone https://github.com/hblvsjtu/Git_Study.git
                Cloning into 'Git_Study'...
                remote: Counting objects: 22, done.
                remote: Compressing objects: 100% (19/19), done.
                remote: Total 22 (delta 6), reused 15 (delta 2), pack-reused 0
                Unpacking objects: 100% (22/22), done.
                [lvhongbin@localhost git]$ ls
                Git_Study  website  website_clone 
                [lvhongbin@localhost git]$ cd Git_Study
                [lvhongbin@localhost Git_Study]$ ll -a
                total 88
                drwxrwxr-x. 4 lvhongbin lvhongbin    87 May 31 18:22 .
                drwxrwxr-x. 5 lvhongbin lvhongbin    59 May 31 18:22 ..
                drwxrwxr-x. 8 lvhongbin lvhongbin   163 May 31 18:22 .git
                -rw-rw-r--. 1 lvhongbin lvhongbin 14774 May 31 18:22 git.tar.gz
                drwxrwxr-x. 2 lvhongbin lvhongbin    80 May 31 18:22 picture
                -rw-rw-r--. 1 lvhongbin lvhongbin 31474 May 31 18:22 README.html
                -rw-rw-r--. 1 lvhongbin lvhongbin 40549 May 31 18:22 README.md

                LvHongbins-Mac:Git_Study lvhongbin$ git commit -a -m "更新了第6章远程版本库" --author="LvHongbin <hblvsjtu@163.com\>"
                [master 00d7b4c] 更新了第6章远程版本库
                 1 file changed, 121 insertions(+), 1 deletion(-)

#### 3) 远程提交 
> - git push
                
                [lvhongbin@localhost Git_Study]$ git push
                warning: push.default is unset; its implicit value is changing in
                Git 2.0 from 'matching' to 'simple'. To squelch this message
                and maintain the current behavior after the default changes, use:

                  git config --global push.default matching

                To squelch this message and adopt the new behavior now, use:

                  git config --global push.default simple

                See 'git help config' and search for 'push.default' for further information.
                (the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
                'current' instead of 'simple' if you sometimes use older versions of Git)

                Username for 'https://github.com': hblvsjtu
                Password for 'https://hblvsjtu@github.com': 
                Everything up-to-date
#### 4) 远程pull 
> - git pull
#### 5) 远程获取元数据 
> - git fetch
#### 6) 本地版本库与远程版本库之间建立联系
> - git remote add origin https://github.com/hblvsjtu/Git_Study.git 添加远程版本库的地址
> - git remote update 更新元数据
> - git branch -a 查看所有分支
                
                [lvhongbin@localhost Git_Study]$ git remote add origin https://github.com/hblvsjtu/Git_Study.git
                fatal: remote origin already exists.
                [lvhongbin@localhost Git_Study]$ git remote update
                Fetching origin
                remote: Counting objects: 6, done.
                remote: Compressing objects: 100% (2/2), done.
                remote: Total 6 (delta 3), reused 6 (delta 3), pack-reused 0
                Unpacking objects: 100% (6/6), done.
                From https://github.com/hblvsjtu/Git_Study
                   9013bbf..00d7b4c  master     -> origin/master
                [lvhongbin@localhost Git_Study]$ git branch
                * master
                [lvhongbin@localhost Git_Study]$ git branch -a
                * master
                  remotes/origin/HEAD -> origin/master
                  remotes/origin/master
> - 创建新的分支后push新的分支 git push --set-upstream origin 本地分支
                
                LvHongbins-Mac:Git_Study lvhongbin$ git branch test/test1
                LvHongbins-Mac:Git_Study lvhongbin$ touch testNewBranch.txt
                LvHongbins-Mac:Git_Study lvhongbin$ vim testNewBranch.txt
                LvHongbins-Mac:Git_Study lvhongbin$ cat testNewBranch.txt

                testNewBranch.txt
                LvHongbins-Mac:Git_Study lvhongbin$ 
                LvHongbins-Mac:Git_Study lvhongbin$ git show-branch
                * [master] 更新了第6章远程版本库
                 ! [test/test1] 更新了第6章远程版本库
                --
                *+ [master] 更新了第6章远程版本库
                LvHongbins-Mac:Git_Study lvhongbin$ git checkout test/test1
                Switched to branch 'test/test1'
                LvHongbins-Mac:Git_Study lvhongbin$ git add testNewBranch.txt
                LvHongbins-Mac:Git_Study lvhongbin$ git commit -m "add testNewBranch.txt for testing creating a new branch" testNewBranch.txt
                [test/test1 0f7f536] add testNewBranch.txt for testing creating a new branch
                 1 file changed, 1 insertion(+)
                 create mode 100644 testNewBranch.txt
                LvHongbins-Mac:Git_Study lvhongbin$ git show-branch
                ! [master] 更新了第6章远程版本库
                 * [test/test1] add testNewBranch.txt for testing creating a new branch
                --
                 * [test/test1] add testNewBranch.txt for testing creating a new branch
                +* [master] 更新了第6章远程版本库

                LvHongbins-Mac:Git_Study lvhongbin$ git push --set-upstream origin test/test1
                Counting objects: 3, done.
                Delta compression using up to 4 threads.
                Compressing objects: 100% (2/2), done.
                Writing objects: 100% (3/3), 327 bytes | 327.00 KiB/s, done.
                Total 3 (delta 1), reused 0 (delta 0)
                remote: Resolving deltas: 100% (1/1), completed with 1 local object.
                To https://github.com/hblvsjtu/Git_Study.git
                 * [new branch]      test/test1 -> test/test1
                Branch 'test/test1' set up to track remote branch 'test/test1' from 'origin'.
> - 创建新的分支后push到另外的远程分支上，本地分支与远程分支中间有一个冒号 git push --set-upstream origin 本地分支:远程分支
        
                LvHongbins-Mac:Git_Study lvhongbin$ touch newBranchfile.txt
                LvHongbins-Mac:Git_Study lvhongbin$ vim newBranchfile.txt
                LvHongbins-Mac:Git_Study lvhongbin$ cat newBranchfile.txt
                newBranchfile.txt for MacOS!

                LvHongbins-Mac:Git_Study lvhongbin$ git add newBranchfile.txt
                LvHongbins-Mac:Git_Study lvhongbin$ git commit -m "add newBranchfile.txt in the newBranch" --author="LvHongbin <hblvsjtu@163.com>"  newBranchfile.txt
                [newBranch 0c70c53] add newBranchfile.txt in the newBranch
                 1 file changed, 1 insertion(+)
                 create mode 100644 newBranchfile.txt

                LvHongbins-Mac:Git_Study lvhongbin$ git push --set-upstream origin newBranch:newBranchRemote
                Counting objects: 3, done.
                Delta compression using up to 4 threads.
                Compressing objects: 100% (2/2), done.
                Writing objects: 100% (3/3), 325 bytes | 325.00 KiB/s, done.
                Total 3 (delta 1), reused 0 (delta 0)
                remote: Resolving deltas: 100% (1/1), completed with 1 local object.
                To https://github.com/hblvsjtu/Git_Study.git
                   0f7f536..0c70c53  newBranch -> newBranchRemote
                Branch 'newBranch' set up to track remote branch 'newBranchRemote' from 'origin'.
> - 删除远程分支 git push --set-upstream origin :远程分支
        
                LvHongbins-Mac:Git_Study lvhongbin$ git branch addBranch
                LvHongbins-Mac:Git_Study lvhongbin$ git push origin addBranch
                Total 0 (delta 0), reused 0 (delta 0)
                To https://github.com/hblvsjtu/Git_Study.git
                 * [new branch]      addBranch -> addBranch
                LvHongbins-Mac:Git_Study lvhongbin$ git push origin :addBranch
                To https://github.com/hblvsjtu/Git_Study.git
                 - [deleted]         addBranch       

        
<h3 id='6.3'>6.3 最佳实践</h3>  
        
#### 1) 以Linux_Study.git为例
> -  每次clone或者在更改之前都应该先更新一下远程的data，避免冲突
        
                LvHongbins-Mac:Desktop lvhongbin$ git clone https://github.com/hblvsjtu/Linux_Study.git
                Cloning into 'Linux_Study'...
                remote: Counting objects: 172, done.
                remote: Compressing objects: 100% (135/135), done.
                remote: Total 172 (delta 33), reused 159 (delta 23), pack-reused 0
                Receiving objects: 100% (172/172), 3.32 MiB | 285.00 KiB/s, done.
                Resolving deltas: 100% (33/33), done.

                LvHongbins-Mac:Desktop lvhongbin$ cd ./Linux_Study
                LvHongbins-Mac:Linux_Study lvhongbin$ ls
                README.html     README.md       picture         practise        practise.tar.gz     recoverTheNet.sh

                # 每次clone或者在更改之前都应该先更新一下远程的data，避免冲突
                LvHongbins-Mac:Linux_Study lvhongbin$ git remote update
                Fetching origin
                LvHongbins-Mac:Linux_Study lvhongbin$ git branch -a
                * master
                  remotes/origin/HEAD -> origin/master
                  remotes/origin/master
                LvHongbins-Mac:Linux_Study lvhongbin$ git pull origin master
                From https://github.com/hblvsjtu/Linux_Study
                 * branch            master     -> FETCH_HEAD
                Already up to date.
                LvHongbins-Mac:Linux_Study lvhongbin$ git status
                On branch master
                Your branch is up to date with 'origin/master'.

                nothing to commit, working tree clean

                # 确认跟远程数据同步之后再进行更改
                LvHongbins-Mac:Linux_Study lvhongbin$ cp ../findTheMaxMTU_MasOS.sh  ./practise/findTheMaxMTU_MasOS.sh
                LvHongbins-Mac:Linux_Study lvhongbin$ vim ./practise/findTheMaxMTU.sh

                # 观察更改的内容
                LvHongbins-Mac:Linux_Study lvhongbin$ git status
                On branch master
                Your branch is up to date with 'origin/master'.

                Changes not staged for commit:
                  (use "git add <file>..." to update what will be committed)
                  (use "git checkout -- <file>..." to discard changes in working directory)

                    modified:   practise/findTheMaxMTU.sh

                Untracked files:
                  (use "git add <file>..." to include in what will be committed)

                    .DS_Store
                    practise/findTheMaxMTU_MasOS.sh

                no changes added to commit (use "git add" and/or "git commit -a")

                # 添加和提交文件
                LvHongbins-Mac:Linux_Study lvhongbin$ git add practise/findTheMaxMTU_MasOS.sh
                LvHongbins-Mac:Linux_Study lvhongbin$ git commit -m "add findTheMaxMTU_MasOS.sh and modify the original practise/findTheMaxMTU.sh  discription" --author="LvHongbin<hblvsjtu@163.com>" practise/findTheMaxMTU_MasOS.sh practise/findTheMaxMTU.sh
                [master 4284f33] add findTheMaxMTU_MasOS.sh and modify the original practise/findTheMaxMTU.sh  discription
                 2 files changed, 71 insertions(+), 1 deletion(-)
                 create mode 100644 practise/findTheMaxMTU_MasOS.sh
                LvHongbins-Mac:Linux_Study lvhongbin$ git push origin master
                Counting objects: 5, done.
                Delta compression using up to 4 threads.
                Compressing objects: 100% (5/5), done.
                Writing objects: 100% (5/5), 573 bytes | 573.00 KiB/s, done.
                Total 5 (delta 4), reused 0 (delta 0)
                remote: Resolving deltas: 100% (4/4), completed with 3 local objects.
                To https://github.com/hblvsjtu/Linux_Study.git
                   65966fe..4284f33  master -> master



