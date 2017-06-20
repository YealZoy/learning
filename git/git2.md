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

# 撤销修改
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git checkout -- readme.txt
```
可以丢弃工作区的修改

命令`git checkout -- readme.txt`意思就是,把`readme.txt`文件在工作区的修改全部撤销，有两种情况
+ 一种是`readme.txt`自修改后还没有被放到暂存区，现在撤销修改就回到和版本库一摸一样的状态
+ 一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

# 删除文件
新建test.txt
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git add test.txt

郑玉燕@zyy MINGW64 /f/learngit (master)
$ git commit -m"test.txt文件添加"
[master 041e604] test.txtt文件添加
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt

郑玉燕@zyy MINGW64 /f/learngit (master)
$ rm test.txt

郑玉燕@zyy MINGW64 /f/learngit (master)
$ git checkout -- test.txt

郑玉燕@zyy MINGW64 /f/learngit (master)
$ git rm test.txt
rm 'test.txt'
```

`rm test.txt`只删除工作区中的`test.txt`文件  

在版本库文件没删除之前可以通过`git checkout -- test.txt`还原

`git rm test.txt`版本库删除`test.txt`文件

# 远程仓库
github仓库
+ 创建SSH Key
```
$ ssh-keygen -t rsa -C "314186096@qq.com"
```

+ 登陆github,打开“Account settings”，“SSH Keys”页面,然后点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容,点“Add Key”，你就应该看到已经添加的Key：

## 添加远程仓库
+ 首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。
```
$ git remote add origin https://github.com/YealZoy/learngit.git
```

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

+ 把所有内容推送到远程库上
```
$ git push -u origin master
Counting objects: 12, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (12/12), 1010 bytes | 0 bytes/s, done.
Total 12 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/YealZoy/learngit.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

## 从远程库克隆
+ 首先，登陆GitHub，创建一个新的仓库，名字叫gitskills：
+ 下一步是用命令git clone克隆一个本地库
```
$ git clone git@github.com:YealZoy/gitskills.git
```

# 分支管理
在版本回退里，每次提交，Git把他们串成一条时间线，这条时间线就是一个分支。在Git里这个分支叫主分支，即`master`分支。`head`严格来说不是指向提交，而是指向`master`，而是`master`指向提交，。所以`head`指向的就是当前分支。  
![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git0.png)

当创建新的分支，例如dev时，git创建了一个指针叫dev,指向`master`相同的提交，再把`head`指向`dev`，表示当前分支在`dev`上  

![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git1.png)  

不过现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变
![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git3.png)   

假如在`dev`上的工作完成了，就可以把`dev`合并到`master`上，就是直接把`master`指向`dev`的当前的提交，就完成了合并。
![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git4.png)  
合并完成分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针删掉，删掉后就剩下了一条`master`分支：
 ![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git5.png) 

+ 创建`dev`分支，然后切换到`dev`分支
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git checkout -b dev
D       test.txt
Switched to a new branch 'dev'
```
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后，用git branch命令查看当前分支：
```
郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git branch
* dev
  master
```

+ 在`dev`分支上正常修改提交
```
郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git add readme.txt

郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git commit -m"file changed”
>"
[dev 8a399eb] file changed”
 1 file changed, 1 insertion(+), 1 deletion(-)
```

+ dev分支的工作完成，就可以切换回master分支
```
郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
```
切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：

+ 把`dev`分支的工作成果合并到`master`分支上
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git merge dev
Updating 756a220..8a399eb
Fast-forward
 readme.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

+ 合并完成后，就可以删除dev分支了：
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git branch -d dev
Deleted branch dev (was 8a399eb).
```

## 解决冲突
+ 准备新的feature1分支，继续新分支开发
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git checkout -b feature1
Switched to a new branch 'feature1'
```

+ 修改readme.txt
+ 在feature1分支上提交
```
郑玉燕@zyy MINGW64 /f/learngit (feature1)
$ git add readme.txt

郑玉燕@zyy MINGW64 /f/learngit (feature1)
$ git commit -m"and simpl"
[feature1 0a33704] and simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

+ 切换到master分支：
```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
```

+ 在master分支上把readme.txt文件
+ 提交
```
$ git add readme.txt 
$ git commit -m "& simple"
[master 400b400] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)
```

现在，master分支和feature1分支各自都分别有新的提交，变成了这样：
![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git6.png) 

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突
```
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

修改readme.txt,再提交
```
$ git add readme.txt 
$ git commit -m "conflict fixed"
[master 59bc1cb] conflict fixed
```
现在，master分支和feature1分支变成了下图所示：
![图片来自阮一峰教程](https://github.com/YealZoy/learning/tree/master/images/git7.png) 

## 分支管理
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

+ 首先，仍然创建并切换dev分支：
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git checkout -b dev
Switched to a new branch 'dev'
```

+ 修改readme.txt文件，并提交一个新的commit：
```
郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git add readme.txt

郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git commit -m"dev分支提交"
[dev 3fa9c15] dev分支提交
 1 file changed, 1 insertion(+)
```

+ 切换回master：
```
郑玉燕@zyy MINGW64 /f/learngit (dev)
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 8 commits.
  (use "git push" to publish your local commits)

```

+ 准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：
```
郑玉燕@zyy MINGW64 /f/learngit (master)
$ git merge --no-ff -m"merge with no-f" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)

```
因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。