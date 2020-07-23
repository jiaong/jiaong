---
title: win 10配置Git
tags: 
  - git
  - windows
categories: git
date: 2020-1-1 13:00:00
top: true
comments: true
---

##### 一、Git配置

1. 下载和安装msysGit（git for windows、Git Bash）
2. 检查是否有ssh key 设置 ` cd ~/.ssh` 或 `cd .ssh`
3. 使用Git bash 生成新的ssh key
```git
$ cd ~
# 配置用户
$ git config --global user.name "jiaong"
$ git config --global user.email jiaong.yy@gmail.com
# 生成ssh公私钥
$ ssh-keygen -t rsa -C "jiaong.yy@gmail.com"
# 一路按回车键默认，生成密钥和公钥
# 文件路径 C:\Users\Administrator\.ssh 
# 添加ssh key 到GitHub，步骤：登录GitHub→Settings→SSH kyes→Add SSH key
# 复制公钥C:\Users\Administrator\.ssh\id_rsa.pub 里的内容
# Title自定义，将公钥粘贴到GitHub中Add an SSH key的key输入框，最后“Add Key”。
# 测试ssh keys是否设置成功。
$ ssh -T git@github.com
$ cd H:/workspace/booltest
#   初始化仓库
#   我的以前已经初始化，不需要
$ git init
#   添加远程仓库
$ git remote add origin git@github.com:jiaong/test-ssh-key.git
#   今天使用Git 添加远程github仓库的时候提示错误：fatal: remote origin already exists. 
#   1. 删除远程仓库
$ git remote rm origin
#   2. 再添加远程仓库
$ git remote add origin git@github.com:jiaong/test-ssh-key.git
#   上传远程仓库
#   上传仓库下的所有文件
$ git add .
#   提交上传说明
$ git commit -m "上传说明"
#   提交到GitHub
$ git push -u origin master
#   执行这个命令行后会弹出下面的错误，
#   出现错误的主要原因是github中的README.md文件不在本地代码目录中
To github.com:jiaong/test-ssh-key.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:jiaong/test-ssh-key.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
# 可以通过以下命令解决上面的错误【注：pull=fetch+merge】
$ git pull --rebase origin master
$ git push -u origin master
```

##### 二、 用git命令行添加多个远程仓库

```git
$ git remote add note git@github.com:jiaong/markdownNote.git
# 查看远程仓库
$ git remote -v
# 切换到其他本地仓库目录下
$ cd G:/data/markdown
# 初始化本地仓库
$ git init

# 再关联远程仓库
$ git remote add note git@github.com:jiaong/markdownNote.git
#   上传远程仓库
#   上传仓库下的所有文件
$ git add .
#   提交上传说明
$ git commit -m "上传说明"
#   提交到GitHub
$ git push -u note master
```

##### 三、 一个github账户多台电脑代码提交

在实际工作生活中，我们可能不一定仅仅在一台电脑上编码，比如：我们平时在单位电脑1上写代码，提交代码到github账户，而我们也可能会在在家里的电脑2上继续工作，提交代码，这样就是在不同的电脑上提交代码到同一个github账户，同时在每一台电脑上都保持和github账户的一致，该怎么办呢？
1. 首先在电脑2上完成git的安装和配置：
和在电脑1上的配置一样，按照本系列git学习1中的教程安装配置，其中用户名和邮箱可以依然使用电脑1的用户名和邮箱，也可以设置为其他用户名和邮箱，均无影响。
2. 然后需要在电脑2上创建另一个SSH Key，保证远程github能够识别电脑2打开Shell（Windows下打开Git Bash），输入
`ssh-keygen -t rsa -C "youremail@example.com"`
然后一路回车，无需设置密码。
然后在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，
id_rsa是私钥，不能泄露，id_rsa.pub是公钥，可以放心告诉别人
登陆Github，进入settings,点击SSH Keys,由于电脑1的SSH Key已经上传，所以可以看到已经有一个SSH Key了，这个SSH key是电脑1的，为了创建电脑2的SSH Key，点击Add SSH Key,填写任意Title，在Key文本框粘贴电脑2的id_rsa.pub文件的内容,然后点add Key。这个就设置好了
3. 将远程库克隆到本地电脑2上,进入某个目录，git bash进入命令行模式：
`git clone git@github.com:NIck-Meng/gitest.git`
然后进入该目录，可以看到gitest文件夹，远程的代码已经被克隆到本地电脑2上了。
这样就可在在电脑2上对代码进行修改、提交等操作了，每次git push将本地修改提交到远程后，远程代码就发生了改变。
4. 当在电脑1上工作时，本地代码和远程的代码发生了不一致，为了保持同步，所以需要将远程的代码同步到本地电脑1上
`git fetch origin master`
从远程的origin的master主分支下载最新的版本到origin/master分支上
`git log -p master..origin/master`
然后比较本地的master分支和origin/master分支的差别
`git merge origin/master`
最后进行合并

参考文档 : https://www.cnblogs.com/Nick-M/p/5559042.html