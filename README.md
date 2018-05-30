
    


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
------      
        
        
<h2 id='1'> 一、简介</h2>
<h3 id='1.1'>1.1 背景</h3>  
        
#### 1) VCS
> - 一个可以管理和追踪软件代码或者其他类似内容的不同版本的工具，通常称为版本控制系统VCS，version control system
> - Git是由Linux之父Linus Torvalds发明，起初是为了方便管理Linux内核的开发工作
> - 在Git之前用得最多的是Bitkeeper，然而在2005年春天Bitkeeper对免费版功能做出了限制，是大家觉得使用Bitkeeper并不是长久之计
        
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