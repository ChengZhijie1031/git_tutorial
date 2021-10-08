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









[廖雪峰教程]: https://www.liaoxuefeng.com/wiki/896043488029600