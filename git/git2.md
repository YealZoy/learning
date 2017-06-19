# 创建版本库
```
$ mkdir learngit
$ cd learngit
$ pwd
```

`pwd`命令用于显示当前目录  

```
$ git init
```
会初始化一个空的仓库，当前目录多了一个.git目录,不要修改.git目录里的文件  

在learngit目录下新建一个readme.txt
```
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```

`git status`命令可以查看仓库当前的状态

```
$ git diff readme.txt
diff --git a/readme.txt b/readme.txt
index e69de29..013b5bc 100644
--- a/readme.txt
+++ b/readme.txt
@@ -0,0 +1,2 @@
+Git is a distributed version control system.
+Git is free software.
\ No newline at end of file
```

`git diff`查看具体修改了什么内容

```
$ git log
commit dc7729cd52ca25d2f7d367f88f6a0ee08132c97b
Author: Yeal Zoy <314186096@qq.com>
Date:   Mon Jun 19 15:08:33 2017 +0800

    文件修改

commit 9975249efff9e7c9ee586073ea5e998b19bd889d
Author: Yeal Zoy <314186096@qq.com>
Date:   Mon Jun 19 15:05:57 2017 +0800

    添加文件

commit 0ea7ddc74afee4f56ee61c863dd275ab357da7a4
Author: Yeal Zoy <314186096@qq.com>
Date:   Mon Jun 19 15:00:46 2017 +0800

    添加文件

```

`git log`显示从最近到最远的提交日志

# 版本回溯
在git中`head`表示当前版本，上一个版本就是`head^`,上上一个版本就是`head^^`,往上100个版本`head~100`
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git reset --hard HEAD^
HEAD is now at 9975249 添加文件

郑玉燕@zyy MINGW64 /f/learngit (master)
$ git log
commit 9975249efff9e7c9ee586073ea5e998b19bd889d
Author: Yeal Zoy <314186096@qq.com>
Date:   Mon Jun 19 15:05:57 2017 +0800

    添加文件

commit 0ea7ddc74afee4f56ee61c863dd275ab357da7a4
Author: Yeal Zoy <314186096@qq.com>
Date:   Mon Jun 19 15:00:46 2017 +0800

    添加文件

```

如果想回去,只要上面的命令窗口还没有被关掉，找到指定的版本
```
$ git reset --hard dc7729cd52c
HEAD is now at dc7729c 文件修改
```

版本号没必要写全，前几位就行，git会自动查找  

如果commit id不知道
```
$ git reflog
dc7729c HEAD@{0}: reset: moving to dc7729cd52c
9975249 HEAD@{1}: reset: moving to HEAD^
dc7729c HEAD@{2}: commit: 文件修改
9975249 HEAD@{3}: commit: 添加文件
0ea7ddc HEAD@{4}: commit (initial): 添加文件
```

# 工作区和暂存区


