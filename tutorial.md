# git学习

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

   







[廖雪峰教程]: https://www.liaoxuefeng.com/wiki/896043488029600