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





















