
## GIT 技巧

### 拉取代码
```
git pull --rebase

1. 把本地 repo 从上次 pull 之后的变更暂存起來
2. 恢复到上次 pull 时的状态
3. 合并远端的变更到本地
4. 最后再合并刚刚暂存下來的本地变更
```

### Pull Request 流程
1. 首先 `git fork` 我的项目
2. 把 `git fork` 过去的项目，也就是你的项目 `git clone` 到你的本地
3. 运行 `git remote add xxx git@github.com:$AUTHOR/$PROJECT.git` 把我的库添加为远端库
4. 运行 `git pull xxx master` 拉取并合并到本地
5. 修改代码
6. `git commit` 后 `git push` 到自己的库（git push origin master）
7. 登录Github在你首页可以看到一个 `pull request` 按钮，点击它，填写一些说明信息，然后提交即可

> 1~3是初始化操作，执行一次即可
> 在修改代码前必须执行第4步同步远程(上游)库，然后继续下面的步骤，否则容易发生冲突