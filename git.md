[TOC]

####

* init 

```shell
git init
git remote add origin XXX
git add 
git commit -m "xxx"
git push origin f_volly_original_20160407:f_volly_original_20160407
```

* alias 为命令设置别名

git config --global alias.ck checkout

* 生成key

ssh-keygen -t rss -C “email"

* 获取分支

git checkout -b [local branch] [remote branch]

git checkout

git merge --no-ff

*--no-ff参数就可以用普通模式合并,合并后的历史有分支,能看出来曾经做过合并,而fast forward合并就看不出来曾经做过合并*

部分提交

git add -p 

* 压缩提交

git rebase -i HEAD~2

* 找回丢失的提交

git fsck --lost-found

* 删除本地分支

git branch -D XXX

* 删除远程分支

git push --delete origin devel

* 也可以推送一个空分支

git push origin :<branchName>

* 清除本地不存在的远程分支

git pull -p

\# 等同于下面的命令

git fetch --prune origin

git fetch -p

* 创建tag

git tag -a V1.2 -m 'XXXXX'

* 查看tag

git tag

推送 git push origin --tags

* 删除 git tag -d V1.2

覆盖远程 git push orign :refs/tags/V1.2

* 创建分支 推送

git branch XXX

git checkout -b XXX

git push origin local_branch:remote_branch

*  git 恢复

git reset --soft HEAD~1 有变化的文件会出现暂存区等待commit

git reset --hard HEAD ~1 清除上一次commit

git revert 撤消一次操作，操作之前的commit都会保留

git reset --soft 什么也不做，也重新标记下head

git reset --mixed 默认 会将add状态去除

git reset —hard 不保留

git pull

* 修改作者信息

git commit --amend --author='name<mail>'

清除untrack文件

git add .

git stash 

git stash drop

或 

git clean -xdf

* 保留当前修改git pull

git statsh 

git pull

git stash pop

* 解决冲突

git stash list

git stash clear

* push之前修改内容

git commit — amend

修改代码→commit→git pull —rebase→git push。也就是将get merge origin/master替换成了git rebase origin/master，它的过程是先将HEAD指向origin/master

$ git checkout feature-branch

$ git rebase master

$ git checkout master

$ git merge --no-ff feature-branch

$ git push origin master

git tag TAG_NAME commit-id

git branch -m old_local_branch_name new_local_branch_name

清除不想跟踪的文件

git update-index --assume-unchanged PATH

清除untracking文件

git clean -fd

合并多条记录

git merge --squash XXX

push远程分支 提交分支数据到远程服务器：

 git push origin f_volly_original_20160407:f_volly_original_20160407

git blame

查看文件的每行改动记录

git gui blame HomePageFragLocationPresenter.java

git biset查找有问题的commit

git gc 清理 .git/pack

删除远程库地址

git remote rm origin

git branch -f branch 强制移动HEAD指针到某一记录

* git submodule

git clone <repository> --recursive 递归的方式克隆整个项目

git submodule add <repository> <path> 添加子模块

git submodule init 初始化子模块

git submodule update 更新子模块

git submodule foreach git pull 拉取所有子模块

git clone project.git --recursive

