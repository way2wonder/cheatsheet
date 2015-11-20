###安装
Linux:`sudo apt-get install git`

###创建版本库
在文件夹中  `git init`

工作区  暂存区   版本库
1. `git  add  file`  命令将工作区的内容提交到工作区，
然后通过 `git  commit -m "备注信息" ` 提交到版本库 
2. 修改文本内容之后通过 `git diff  file`  可以展示变化的内容
3. `git log`
4. 版本回退  `git reset --hard HEAD^`    HEAD 为当前版本，那么HEAD^就是上个版本
5. `git reset --hard commit_id`     `git reflog`  获取commit ID 然后就能重返未来啦


###修改

1. 只会将提交到工作区的文件提交到版本库中：如果第二次修改没有通过`git add` 命令加入到暂存区，那么`git commit`的时候就不会提交第二次修改
2. 撤销修改：

    - 仅仅在工作区修改：`git checkout -- file`  , `--`  很重要，如果没有`--` 那么就变成另外一个命令（切换到另外一个分支）。
    - 已经提交到暂存区：用命令`git reset HEAD file` 可以把暂存区的修改撤销掉（unstage），重新放回工作区：
    - 已经提交到版本库： 参照上衣章的版本回退命令


###删除
1. `rm readme.txt`  delete file
2. `git status`   view difference
3.  you have 2 different choice . 
    - `git rm file` 删除版本库文件，并提交`git commit`
    - `git checkout -- file` 从版本库恢复文件（`git checkout`其实是用版本库里的版本替换工作区的版本）



###远程库

添加远程库，这里我们用 [GitHub](www.github.com) 作为远程仓库

1. 创建sshkey  `ssh-keygen -t rsa -C "youremail@example.com"`(比如我的github的帐号是772755185@qq.com)
2. 将id_rsa.pub 中的内容粘贴到github的 add sshkey 中
3. `git clone git@github.com:way2wonder/gitskills.git`   克隆命令
4. `git remote add origin git@server-name:path/repo-name.git`  关联远程库
5. `git push -u origin master`  将本地仓库推送到远程库  origin这个名字可以自己更改，但是一般都按这个名字

** GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。
使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https **





### 分支

1. `git checkout - b  branchName`创建分支
2. `git merge  master branch1`   合并分支
3. ` git checkout master`   切换到master分支

**当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
用git log --graph命令可以看到分支合并图。**