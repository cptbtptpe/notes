## Git

### 知识点

1. 在 `Git` 中，`HEAD` 表示当前版本
2. 当前版本的上一个版本是 `HEAD^`，上上一个版本是 `HEAD^^`，当然往上 `100` 个版本 `^` 太多，所以写成 `HEAD~100`
3. `Hash` 号可以不写全，能让 `Git` 唯一确定就行了，当然一般写全是为了安全起见

### 拉取代码

```
# 拉取指定 origin repo 库的 master 分支
git pull <REPO NAME> <BRANCH NAME>

git pull --rebase <REPO NAME> <BRANCH NAME>

1. 把本地 repo 从上次 pull 之后的变更暂存起來
2. 恢复到上次 pull 时的状态
3. 合并远端的变更到本地
4. 最后再合并刚刚暂存下來的本地变更
```

### 创建本地分支

```
git checkout <BRANCH NAME>

# 并切换到该创建的分支
git checkout -b <BRANCH NAME>
```

### 文件回退版本

```
# 查看文件的修改日志
git log <FILE NAME>

# 回退到指定 Hash 版本
git reset <HASH> <FILE NAME>

# 提交到本地缓冲
git commit -m 'reset file'

# 更新到当前工作目录
git checkout <FILE NAME>

# 提交到远程仓库
git push <REPO NAME> <BRANCH NAME>
```

### 整体回退版本

```
git reset --hard <HASH>

# --hard    重置工作空间，自从 <HASH> 以来在工作空间中的任何改变都被丢弃，并把 HEAD 指向 <HASH>
# --soft     工作空间中的内容不作任何改变，仅仅把 HEAD 指向 <HASH>
```

### 设置用户名和邮箱

```
git config --global user.name <USERNAME>
git config --global user.email <EMAIL>
 
# 使用 git config --list 可查看配置
```

### 修改用户名和邮箱

```
git commit --amend --author='<USERNAME> <EMAIL>'
```

### pull request 流程

1. 首先 `git fork` 我的项目
2. 把 `git fork` 过去的项目，也就是你的项目 `git clone` 到你的本地
3. 运行 `git remote add <REPO NAME> git@github.com:<AUTHOR>/<PROJECT>.git` 把我的库添加为远端库
4. 运行 `git pull <REPO NAME> <BRANCH NAME>` 拉取并合并到本地
5. 修改代码
6. `git commit` 后 `git push` 到自己的库（ git push origin master ）
7. 登录 Github 在你首页可以看到一个 `pull request` 按钮，点击它，填写一些说明信息，然后提交即可

> 1~3 是初始化操作，执行一次即可
> 在修改代码前必须执行第 4 步同步远程(上游)库，然后继续下面的步骤，否则容易发生冲突

### 压缩多个 commit

```
git rebase -i HEAD~<NUMBER OF COMMITS>

# 运行该命令时，你会看到一个交互界面，列出了许多 commit 让你选择哪些需要进行压缩
# 理想情况下，你选择最后一次 commit 并把其它老 commit 都进行压缩
```

### 暂存未提交的更改

```
# 将当前工作空间暂存
git stash

# 恢复指定的文件
git reset HEAD <FILE>

# 查看暂存列表
git stash list

# 解除暂存，恢复到未提交的更改
git stash apply

# 恢复到指定标示的暂存版本，如 stash@{0}
git stash apply <STASH>
```

### 查看日志

```
# 显示 Hash 、作者、日期、提交描述信息
git log

# 显示 Hash 、提交描述信息
git log --pretty=oneline

# 图形显示版本图
git log --graph

# 显示所有分支的历史记录
git log --all

# 查看所有分支的所有操作记录
git reflog

# 查看所有分支的所有操作记录(大型仓库)
git fsck --lost-found

# 将文件中的每一行的作者、最新的变更提交和提交时间展示出来
git blame <FILE NAME>

# 查看更新详情，默认是行级对比
git log -p -1
# ↓↓
git log -U1
# ↓↓
git show -1

# 使用 --word-diff 放在 -p 后可以开启单词级对比
git log -p --word-diff -1

# -p 展开显示提交的内容差异
# -1 显示最近的一次提交，也可以使用 Hash 代替

git log -p <HASH>
# ↓↓
git show <HASH>
```

### 查看分支

```
# 列出本地已经存在的分支，并且在当前分支的前面加 * 号标记
git branch

# 列出本地分支和远程分支
git branch -a

# 创建一个新的本地分支，不进行分支切换
git branch <BRANCH NAME>

# 重命名本地分支，如果新分支名已经存在，则需要使用 -M 代替 -m 来强制重命名
git branch -m <OLD BRANCH NAME> <NEW BRANCH NAME>

# 删除本地分支，-D 强制 (该分支有未合并到当前分支的内容)
git branch -d <BRANCH NAME>

# 删除远程分支 (错误姿势)
git branch -d -r <REPO NAME>/<BRANCH NAME>

# 删除远程分支 (正确姿势，冒号前有空格)
git push <REPO NAME> :<BRANCH NAME>
```

### 初始化本地项目 github 为例

```
git init
git add *
git commit -m "init project."
git remote add <REPO NAME> git@github.com:<AUTHOR>/<PROJECT>.git
git push -u <REPO NAME> <BRANCH NAME>

# <REPO NAME> standard used default `origin`
```

### 修改 commint 信息或漏传文件

```
git commit -m 'initial commit'
git add forgotten_file.md
git commit --amend

# 最终你只会有一个提交
# 第二次提交将代替第一次提交的结果
```

### 删除误传的隐私文件及历史

```
git filter-branch -f --tree-filter 'rm -rf mixed/password' HEAD
# 有必要需把对应的文件写入到 .gitignore 中
git push origin master --force
```

### git command

```
常用操作

git clone <REPO ADDRESS> [<ALIAS>]
                    # 获取/下载/备份远程仓库代码
git clone -b <BRANCH NAME> <REPO ADDRESS>
                    # 仅克隆指定的分支

查看、添加、提交、删除、找回，重置修改文件

git help <COMMAND>  # 显示 command 的 help
git show [<HASH>]   # 显示某次提交的内容详情
git co -- <FILE>    # 抛弃对应文件工作区修改
git co .            # 抛弃当前工作区修改
git add <FILE>      # 将工作文件修改提交到本地暂存区
git add .           # 将所有修改过的工作文件提交暂存区
git rm <FILE>       # 从版本库中删除文件
git rm <FILE> --cached 
                    # 从版本库中删除文件提交记录，但不删除文件
git reset <FILE>    # 从暂存区恢复到工作文件
git reset -- .      # 从暂存区恢复到工作文件
git reset --hard    # 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改
git ci <FILE> 
git ci . 
git ci -a 
                    # 将 git add, git rm 和 git ci 等操作都合并在一起做 git ci -am "some comments"
git ci --amend      # 修改最后一次提交记录
git revert <HASH>   # 恢复某次提交的状态，恢复动作本身也创建次提交对象
git revert HEAD     # 恢复最后一次提交的状态

查看文件 diff

git diff <FILE>     # 比较当前文件和暂存区文件差异 git diff
git diff <HASH-1> <HASH-2> <HASH-3> ... 
                    # 比较多次提交之间的差异
git diff <BRANCH NAME-1> <BRANCH NAME-2> <BRANCH NAME-3> ...
                    # 比较多个分支之间的差异
git diff --staged   # 比较暂存区和版本库差异
git diff --cached   # 比较暂存区和版本库差异
git diff --stat     # 仅仅比较统计信息

查看提交记录

git log <FILE>      # 查看该文件每次提交记录
git log -p <FILE>   # 查看每次详细修改内容的 diff
git log -p -2       # 查看最近两次详细修改内容的 diff
git log --stat      # 查看提交统计信息

本地仓库的查看、切换、创建和删除分支

git br -r           # 查看远程分支
git br <BRANCH NAME> 
                    # 创建新的分支
git br -v           # 查看各个分支最后提交信息
git br --merged     # 查看已经被合并到当前分支的分支
git br --no-merged  # 查看尚未被合并到当前分支的分支
git co <BRANCH NAME>     
                    # 切换到某个分支, co 全称 checkout
git co -b <BRANCH NAME> 
                    # 创建新的分支，并且切换过去
git co -b <NEW BRANCH NAME> <BRANCH NAME> 
                    # 基于 branch 创建新的 new_branch
git co $id          # 把某次历史提交记录 checkout 出来，但无分支信息，切换到其他分支会自动删除
git co $id -b <BRANCH NAME> 
                    # 把某次历史提交记录 checkout 出来，创建成一个分支
git br -d <BRANCH NAME>     
                    # 删除某个分支
git br -D <BRANCH NAME>     
                    # 强制删除某个分支 (未被合并的分支被删除的时候需要强制)

本地仓库的分支合并和 rebase

git merge <BRANCH NAME>     
                    # 将 branch 分支合并到当前分支
git merge origin/master --no-ff 
                    # 不要 Fast-Foward 合并，这样可以生成 merge 提交
git rebase master <BRANCH NAME> 
                    # 将 master rebase 到 branch
                    # 相当于： git co <branch> && git rebase master && git co master && git merge <branch>

Git 补丁管理(方便在多台机器上开发同步时用)

git diff > ../sync.patch 
                    # 生成补丁
git apply ../sync.patch 
                    # 打补丁
git apply --check ../sync.patch 
                    # 测试补丁能否成功

Git 暂存管理

git stash # 暂存
git stash list      # 列所有 stash
git stash apply     # 恢复暂存的内容
git stash drop      # 删除暂存区

Git 远程分支管理

git pull            # 抓取远程仓库所有分支更新并合并到本地, 相当于 git fetch && git merge
git pull --no-ff    # 抓取远程仓库所有分支更新并合并到本地，不要快进合并
git fetch origin    # 抓取远程仓库更新
git merge origin/master 
                    # 将远程主分支合并到本地当前分支
git co --track origin/branch 
                    # 跟踪某个远程分支创建相应的本地分支
git co -b <LOCAL BRANCH NAME> origin/<REMOTE BRANCH NAME> 
                    # 基于远程分支创建本地分支，功能同上
git push            # push 所有分支
git push origin master 
                    # 将本地主分支推到远程主分支
git push -u origin master 
                    # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
git push origin <LOCAL BRANCH NAME> 
                    # 创建远程分支， origin 是远程仓库名
git push origin <LOCAL BRANCH NAME>:<REMOTE BRANCH NAME> 
                    # 创建远程分支
git push origin :<REMOTE BRANCH NAME> 
                    # 先删除本地分支(git br -d <branch>)，然后再 push 删除远程分支

Git 远程仓库管理

git remote -v       # 查看远程服务器地址和仓库名称
git remote show origin 
                    # 查看远程服务器仓库状态
git remote add <REPO NAME> <REPO ADDRESS>
                    # 添加远程仓库地址
git remote set-url origin <REPO ADDRESS>
                    # 设置远程仓库地址(用于修改远程仓库地址)
git remote rm <REPO NAME> 
                    # 删除远程仓库
git remote rename <OLD REPO NAME> <NEW REPO NAME>
                    # 远程仓库的重命名

创建远程仓库

git clone --bare [<ALIAS>] <REPO ADDRESS> 
                    # 用带版本的项目创建纯版本仓库
scp -r <PROJECT> <GIT SSH>:~ 
                    # 将纯仓库上传到服务器上
mkdir <PROJECT> && cd <PROJECT> && git --bare init 
                    # 在服务器创建纯仓库
git remote add origin <REPO ADDRESS> 
                    # 设置远程仓库地址
git push -u origin master 
                    # 客户端首次提交
git push -u origin develop 
                    # 首次将本地 develop 分支提交到远程 develop 分支，并且 track
git remote set-head origin master 
                    # 设置远程仓库的 HEAD 指向 master 分支

命令设置跟踪远程库和本地库

git branch --set-upstream master origin/master
git branch --set-upstream develop origin/develop

打标签

git tag             # 列出已有的标签
git tag -a v1.0.0 -m 'my version 1.0.0'
                    # 创建附注标签
git show v1.0.0     # 查看对应标签的信息
git tag v1.0.0-rc   # 创建轻量标签
```

### .gitignore

```
关于 Git 的忽略文件的语法规则

忽略文件中的空行或以井号（#）开始的行将会被忽略
可以使用 Linux 通配符
    星号（*）代表任意多个字符
    问号（？）代表一个字符
    方括号（[abc]）代表可选字符范围
    大括号（{string1, string2, ...}）代表可选的字符串
如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略
如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略
如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）

示例：

    # 这是注释行，将被忽略
    *.a       # 忽略所有以.a 为扩展名的文件    
    !lib.a    # 但是名为 lib.a 的文件或目录不要忽略，即使前面设置了对*.a 的忽略
    /TODO     # 只忽略此目录下的 TODO 文件，子目录中的 TODO 文件不忽略
    build/    # 忽略所有 build 目录下的文件，但如果是名为 build 的文件则不忽略
    doc/*.txt # 忽略文件如 doc/notes.txt ，但是文件如 doc/server/arch.txt 不忽略
```