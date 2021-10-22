# git学习教程

使用的是[廖雪峰][廖雪峰教程]的git教程



## 创建版本库

1. 首先新目录下创建git仓库（repository）

   > 注意：windows系统下无法追踪Word文件改动

   使用`git init`初始化命令

   

2. 添加文件到git仓库

   使用`git add `命令添加文件到仓库

   使用`git commit -m "说明文本"`提交文件到仓库

   可以多次`git add`，最终一并提交`git commit`



## 管理历史记录

1. 使用`git status`命令查看仓库状态

   ```powershell
   $ git status
   On branch master
   Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
     (use "git restore <file>..." to discard changes in working directory)
           modified:   tutorial.md
   
   no changes added to commit (use "git add" and/or "git commit -a")
   
   ```

   表示文件`tutorial.md`被修改过了，但是还没有准备提交的修改

2. 使用`git diff`查看更改的内容

3. 继续使用`git add`和`git commit`命令提交修改后的文件



## 版本回退

1. 使用`git log`查看历史版本日志记录

   ```powershell
   $ git log
   commit 20529966e29b0b4ba21ab31f2478601879b1626d (HEAD -> master)
   Author: Cheng Zhijie <jackczj1997@qq.com>
   Date:   Fri Oct 8 23:37:52 2021 +0800
   
       update the Chpanter3
   
   commit a88308d7c01dcd4bd963a30b065bb964f301558d
   Author: Cheng Zhijie <jackczj1997@qq.com>
   Date:   Fri Oct 8 23:34:57 2021 +0800
   
       update the Chpanter2
   
   commit 3a950d8cdaa6eb1918da68478079cf087970b605
   Author: Cheng Zhijie <jackczj1997@qq.com>
   Date:   Fri Oct 8 22:43:01 2021 +0800
   
       update git tutorial
   
   ```

   commit版本号十六进制，在git GUI里面也可以查看提交历史的时间线

   

2. 版本切换

   用`HEAD`表示当前版本，`HEAD^`表示上一个版本，`HEAD^^`表示上上个版本，`HEAD~100`表示往上100个版本

   `git reset`命令回退到指定版本

   `git reset --hard HEAD^`回到上个版本

   `git reset --hard <commit id>`回到指定版本，其中`<commit id>`从`git log`可以查找，只要命令行没关闭就可以找到
   
   ```powershell
   $ git reset --hard 6dfd161f1308
   HEAD is now at 6dfd161 update git reset command
   
   ```
   
   > 版本号`<commit id>`没有必要写全，git可以自动查找前几位
   
   git内部的`HEAD`其实是一个指针，指向当前版本
   
   其实也可以通过`git reflog`命令查看每一次命令，用于查找版本号`<commit id>`
   
   ```powershell
   $ git reflog
   6dfd161 (HEAD -> master) HEAD@{0}: reset: moving to 6dfd161f1308
   2052996 HEAD@{1}: reset: moving to HEAD^
   6dfd161 (HEAD -> master) HEAD@{2}: commit: update git reset command
   2052996 HEAD@{3}: commit: update the Chpanter3
   a88308d HEAD@{4}: commit: update the Chpanter2
   3a950d8 HEAD@{5}: commit (initial): update git tutorial
   
   ```
   
   

3. 理解stage和master的概念

   

   ![alt git add](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)

   

   ![alt git commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)



​		git管理的是修改而不是文件，每次修改后，需要先`git add`到暂存区stage，然后`git commit`提交到版本库



4. `git checkout -- <file>`命令用来撤销文件在工作区的修改

   在`git add`后，`git commit`前，使用`git reset HEAD <file>`撤销暂存区的修改，重新放回工作区

   

   删除也是一种修改操作：

   普通的`rm`删除命令直接删除文件，使用`git rm <file>`命令删除版本库的文件，使用`git checkout -- <file>`即可恢复删除文件



## 远程仓库

1. 添加GitHub的SSH Key

   在GitHub账户设置里添加SSH Key

   

2. 在GitHub创建新的Repository

   在本地仓库目录下运行命令`git remote add origin git@github.com:<GitHub Account Name>/<GitHub Repository Name>.git`

   使用`git push -u origin master`命令推送到远程库

   

3. `git push origin master`把本地`master`分支的最新修改推送至GitHub



4. 从远处库clone到本地

   如果从零开发新项目，应该先创建远程库，再从远程库clone到本地

   `git clone git@github.com:<GitHub Account Name>/<GitHub Repository Name>.git`



## 分支管理 Branches

1. 创建与合并分支

   如下图所示，分支`dev`是`master`外的另一个分支，将`HEAD`指向`dev`分支，对工作区的修改和提交就是针对`dev`分支

   

   ![alt branches](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)

   合并就是把`master`指向`dev`的当前提交

   

   ![alt](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)

   创建`dev`分支并且切换

   ```powershell
   $ git switch -c dev
   Switched to a new branch 'dev'
   
   ```

   这里`-c`参数表示创建并且切换，相当于以下两条命令：

   ```powershell
   $ git branch dev
   $ git switch dev
   ```

   `git branch`查看当前分支

   这里就可以在新分支上直接修改提交

   合并分支`git merge dev`

   删除分支`git branch -d dev`

   

2. 多人协作推送分支的工作模式

   先利用`git push`推送

   如果失败则需要用`git pull`进行合并

   合并有冲突则解决冲突，并且在本地提交

   最后`git push`提交



## 标签管理tags

1. 创建标签（全都储存在本地）

​		先切换到需要打标签的分支上，使用`git tag v1.0`打上v1.0的标签

​		使用`git tag`查看所有标签，使用`git show <tagname>`查看标签信息

​		使用`git tag <tagname> <commit id>`对指定的某次历史提交打标签

​		使用`git tag -a <tagname> -m "message"`指定标签信息



2. 操作标签

   `git tag -d <tagname>`删除标签

   推送标签到远程使用`git push origin <tagname>`

   推送所有未推送的本地标签`git push origin --tags`

   远程删除标签需要先删除本地标签，再远程删除`git push origin :ref/tags/<tagname>`

   



















[廖雪峰教程]: https://www.liaoxuefeng.com/wiki/896043488029600