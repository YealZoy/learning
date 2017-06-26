# 关于版本控制
版本控制是一种记录一个或若干文件内容变化，以便将来查阅特定版本修订情况的系统

# 用户信息
安装完git应该做的第一件事就是设置用户名与邮件地址,每一个Git提交都会使用这些信息,并且会写入到每一次提交中，不可更改：
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
如果使用了`--global`选项，该命令只需运行一次，因为之后再系统做任何事情，Git都会使用那些信息。当向针对特定项目使用不同的用户名与邮件地址时，可以在那个项目目录下运行没有`--global`选项的命令来配置

# 检查配置信息
`git config --list`命令会列出所有Git当时能找到的配置

可以通过`git config <key>`检查Git的某一项配置
```
git config user.name
```

# 获取帮助
有三种方法可以找到Git命令使用手册
```
git help <verb>
git <verb> --help
man git-<verb>
```

# 获取Git仓库
有两种获取git项目仓库的方法。第一种事在现有项目或目录下导入所有文件到Git中;第二种是从服务器克隆一个现有的Git仓库

## 在现有目录中初始化仓库
只需进入该项目目录并输入
```
git init
```

该命令会创建一个名为`.git`的子目录，这个子目录含有你初始化的Git仓库中所有的必须文件，这些文件是Git仓库的骨干。但在这个时候，仅仅是做了一个初始化的操作。项目的文件还没有被跟踪

如果是一个已经存在的文件的文件夹中初始化Git仓库进行版本控制的话，应该开始跟踪这些文件并提交。可以通过`git add`命令来实现对指定文件的跟踪，然后执行`git commit`提交
```
git add *.c
git add LICENSE
git commit -m "init project version"
```

## 克隆现有的仓库
克隆仓库的命令格式是`git clone [url]`  

`git clone https://github.com/libgit2/libgit2`  

这会在当前目录下创建名为`libgit2`的目录，并在这个目录下初始化一个`.git`文件夹，从远程仓库拉取下所有放入`.git`文件夹，然后从中读取最新版本的文件的拷贝。如果想在克隆仓库的时候自定义本地仓库名字，可以使用如下命令:
`$ git clone https://github.com/libgit2/libgit2 mylibgit`
这将执行与上一个命令相同的操作，不过在本地创建的仓库名字变为 mylibgit。

# 记录每次更新到仓库
工作目录下的每一个文件都不外乎两种状态:已跟踪或未跟踪。已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，他们的状态可能出于未修改，已修改或已放入暂存区。工作目录中除已跟踪文件意外的所有其它文件都属于未跟踪文件，他们既不存在于上次快照的记录中，也没有放入暂存区。初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并出于未修改状态。  
编辑某些文件之后，由于自上次提交后对它们作了修改，Git将它们标记为以修改文件，逐步将这些修改过的文件放入暂存区，然后提交所有暂存了的修改，如此反复，git是文件的生命周期如下:
![图片来自git-scm](https://github.com/YealZoy/learning/blob/master/images/lifecycle.png) 

# 检查当前文件状态
要查看哪些文件处于什么状态，可以用`git status`命令。如果在克隆仓库后立即使用此命令，会看到类似这样的输出
```
$ git status
On branch master
nothing to commit, working directory clean
```

这说明现在的工作目录相当干净。所有已跟踪文件在上次提交后都未被更改过。此外，上见的信息还表明，当前目录下没有出现任何处于未跟踪状态的新文件，否则Git会在这里列出来。最后还显示了当前所在的分支，并说明这个分支同远程服务器上对应的分支没有偏离

# 跟踪文件
使用`git add`开始跟踪一个文件

`git add README`

在运行`git status`命令
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
```

只要在 Changes to be committed 这行下面的，就说明是已暂存状态。`git add`命令使用文件

# 暂存已修改文件
如果修改了一个名为`CONTRIBUTING.md`的已被跟踪的文件，然后运行`git status`命令
```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

文件 CONTRIBUTING.md 出现在 Changes not staged for commit 这行下面,说明已跟踪文件的内容发生了变化，但还没有放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。

```
$ git add CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```

再次修改`CONTRIBUTING.md`,保存后运行`git status`

```
$ vim CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md
```

`CONTRIBUTING.md`文件同时出现在暂存区和非暂存区。Git只不过暂存你运行`git add`命令时的那个版本，而不是你运行`git commit`时，在工作目录中的当前版本

# 状态简览
`git status`命令输出十分详细。可以用`git status -s`命令或`git status --short`命令，将得到一种更为紧凑的格式输出
```
$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt
```

新添加的未跟踪的文件前面有`??`标记，新添加到暂存区的文件前面有`A`标记，修改过的文件前面有`M`标记，有两个`M`标记出现的位置，右边的`M`表示该文件被修改了但是还没放入暂存区，出现在左边的`M`表示文件被修改了并放入暂存区。 `README`文件在工作区被修改了但是还没有将修改后的文件放入暂存区,`lib/simplegit.rb` 文件被修改了并将修改后的文件放入了暂存区。而`Rakefile` 在工作区被修改并提交到暂存区后又在工作区中被修改了

# 忽略文件
可以创建一个名为.gitignore的文件，列出要忽略的文件模式
```
$ cat .gitignore
*.[oa]
*~
```
第一行告诉 Git 忽略所有以 .o 或 .a 结尾的文件
第二行告诉 Git 忽略所有以波浪符（~）结尾的文件

文件`.gitignore`的格式规范如下
+ 所有空行或者以`#`开头的行都会被Git忽略
+ 可以使用标准的glob模式匹配
+ 匹配模式可以以(`/`)开头防止递归
+ 匹配模式可以以('/')结尾指定目录
+ 要忽略指定模式以外的文件或目录，可以在模式前加上(!)取反

```
# no .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in the build/ directory
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```




