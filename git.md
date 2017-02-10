# 查看git所有的配置
```code
$ git config --list
```


# 设置姓名和邮箱地址
```code
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
```

# git提高命令输出的可读性
```code
$ git config --global color.ui auto
```

# 创建SSH Key
```code
$ ssh-keygen -t rsa -C "your_email@example.com"
```

# 在github上添加公开密钥
点击右上角的账户设定按钮（Account Settings），选择 SSH Keys 菜单

点击 Add SSH Key 之后,在 Title 中输入适当的密钥名称。
Key 部分请粘贴 id_rsa.pub 文件里的内容

id_rsa.pub的内容可以用如下方法查看

# 私人密钥与GitHub进行认证和通信
```code
$ ssh -T git@github.com
```

# git设置代理
```code
$ git config --global https.proxy http://127.0.0.1:1080
```

# git取消代理
```code
git config --global --unset http.proxy
```

# clone已有仓库
```code
$ git clone git@github.com:hirocastest/Hello-World.git
```

# 查看状态
```code
$ git status
```

# 添加文件
```code
$ git add 计划.txt(添加到暂存区)
```

# 提交
```code
$ git commit -m "描述语句" (记述一行提交信息)
$ git commit(记述详细提交信息)
```
在编辑器中记述提交信息的格式如下。
+ 第一行：用一行文字简述提交的更改内容
+ 第二行：空行
+ 第三行以后：记述更改的原因和详细内容
只要按照上面的格式输入，今后便可以通过确认日志的命令或工具
看到这些记录。
在以 #（井号）标为注释的 Changes to be committed（要提
交的更改）栏中，可以查看本次提交中包含的文件。将提交信息按格式
记述完毕后，请保存并关闭编辑器，以 #（井号）标为注释的行不必删
除。随后，刚才记述的提交信息就会被提交。

# 退出vim
在命令行中输入`$ git commit`时没有加入-m，会自动出来一个让填写提交说明的窗口
+ 步骤一：按键盘<font color='#c7254e'>`i`</font>,此时光标会在最上面
+ 步骤二：输入要提交的说明，按下<font color='#c7254e'>`Esc`</font>,然后输入<font color='#c7254e'>`:`</font>,光标跑到最下面
+ 步骤三：输入<font color='#c7254e'>`wq`</font>之后按回车即可，就回到原始的命令行界面

# 中止提交
如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编
辑器，随后提交就会被中止


# git查看提交日志
```code
$ git log
$ git log README.md(只显示指定目录、文件的日志,只要在 git log命令后加上目录名，便会只显示该目录下的日志。如果加的是文件名，就会只显示与该文件相关的日志。)
$ git log -p（如果想查看提交所带来的改动，可以加上 -p参数，文件的前后差别就会显示在提交信息之后）
```

# push推送到github上
```code
$ git push
之后只要执行 push，GitHub 上的仓库就会被更新
```

# 查看更改前后的差别
```code
$ git diff
```

# 显示分支
```code
$ git branch
```

# git checkout  - b——创建
```code
$ git checkout -b feature-A
```
或者
```code
$ git branch feature-A
$ git checkout feature-A
```

# 切换分支
```code
$ git checkout master
```

# 切换回上一个分支
```code
$ git checkout -
```

# 合并分支
我们假设 feature-A 已经实现完毕，想要将它合并到主干分
支 master 中。首先切换到 master 分支。
```
$ git checkout master
Switched to branch 'master'
```
然后合并 feature-A 分支。为了在历史记录中明确记录下本次分支合
并，我们需要创建合并提交。因此，在合并时加上 --no-ff参数。
```
$ git merge --no-ff feature-A
```


# 添加远程仓库
$ git remote add origin git@github.com:github-book/git-tutorial.git

# 推送至远程仓库
## 推送至master
$ git push -u origin master
像这样执行 git push命令，当前分支的内容就会被推送给远程仓库
origin 的 master分支。-u参数可以在推送的同时，将origin仓库的master分
支设置为本地仓库当前分支的 upstream（上游）。添加了这个参数，将来
运行 git pull命令从远程仓库获取内容时，本地仓库的这个分支就可
以直接从 origin 的 master 分支获取内容，省去了另外添加参数的麻烦。

## 推送至master以外的分支
+ 步骤一：$ git checkout -b feature-D
+ 步骤二：$ git push -u origin feature-D

# 发送pull Request
+ 步骤一：访问github用户的项目页面，点击<font color='#c7254e'>`fork`</font>创建自己的仓库（可以为仓库命名等）
+ 步骤二：`$ git clone https://github.com/YealZoy/first-pr.git
` clone仓库
+ 步骤三：创建特性分支`$ git checkout -b work gh-pages`
+ 步骤四：提交修改
          ```
          $ git add index.html
          $ git commit -m "index.html修改"
          ```
+ 步骤五：创建远程分支
          ```
            $ git push origin work
          ```
+ 步骤六：打开自己的first-pr,确认work分支是否被创建，以及包含修改的代码
+ 步骤七：发送pull Request





         


















