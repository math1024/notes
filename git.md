[TOC]



* init 

```shell
git init
git remote add origin XXX
git add 
git commit -m "xxx"
git push origin branch_name:branch_name
```

* alias 为命令设置别名

```shell
git config --global alias.ck checkout
```

* 生成key

```shell
ssh-keygen -t rss -C “email"
```

* 获取分支

```shell
git checkout -b [local branch] [remote branch]
git checkout
git merge --no-ff
# *--no-ff参数就可以用普通模式合并,合并后的历史有分支,能看出来曾经做过合并,而fast forward合并就看不出来曾经做过合并*
```

* git log

```shell
// log显示一行
git log --pretty=oneline
```



* 压缩提交

```shell
git rebase -i HEAD~2
```

* 找回丢失的提交

```shell
git fsck --lost-found
```

* 创建分支

```shell
git branch XXX
git checkout -b XXX
git push origin local_branch:remote_branch
```

* 删除分支

```shell
# 删除本地分支
git branch -D XXX
# 删除远程分支
git push --delete origin devel
# 清除本地不存在的远程分支
git pull -p
```

* tag

```shell
# 创建tag
git tag -a V1.2 -m 'XXXXX'
# 查看tag
git tag
# 推送 
git push origin --tags
# 删除 git tag -d V1.2
覆盖远程 git push orign :refs/tags/V1.2
```

*  git 恢复

```shell
git reset --soft HEAD~1 有变化的文件会出现暂存区等待commit
git reset --hard HEAD ~1 清除上一次commit
git revert 撤消一次操作，操作之前的commit都会保留
git reset --soft 什么也不做，也重新标记下head
git reset --mixed 默认 会将add状态去除
git reset —hard 不保留
```

* 修改作者信息

```shell
git commit --amend --author='name<mail>'
```

* 清除untrack文件

```shell
git add .
git stash 
git stash drop
或 
git clean -xdf
# 清除不想跟踪的文件
git update-index --assume-unchanged PATH
```

* 保留当前修改git pull

```shell
git statsh 
git pull
git stash pop
```

```shell
修改代码→commit→git pull —rebase→git push。也就是将get merge origin/master替换成了git rebase origin/master，它的过程是先将HEAD指向origin/master
$ git checkout feature-branch
$ git rebase master
$ git checkout master
$ git merge --no-ff feature-branch
$ git push origin master
git tag TAG_NAME commit-id
git branch -m old_local_branch_name new_local_branch_name
```

查看文件的每行改动记录

```shell
git blame
git gui blame HomePageFragLocationPresenter.java
git biset查找有问题的commit
git gc 清理 .git/pack
```

* 删除远程库地址

```shell
git remote rm origin
```

* git submodule

```shell
git clone <repository> --recursive 递归的方式克隆整个项目
git submodule add <repository> <path> 添加子模块
git submodule init 初始化子模块
git submodule update 更新子模块
git submodule foreach git pull 拉取所有子模块
git clone project.git --recursive
```

* 查看commit在哪个分支 git branch --contains

```
语法：git branch --contains <commit-id>
命令：git branch --contains 700920
```

* git filter-branch --env-filter

```shell

```

* git format-patch 生成patch

```shell
# 生成最近的1次commit的patch
git format-patch HEAD^ 　　　　　　　　　　　　　  
# 生成最近的2次commit的patch
git format-patch HEAD^^　　　　　　　　　　　　　  
# 生成两个commit间的修改的patch（包含两个commit <r1>和<r2>都是具体的commit号)
git format-patch <r1>..<r2> 
# 生成单个commit的patch
git format-patch -1 <r1>  
# 生成某commit以来的修改patch（不包含该commit）
git format-patch <r1>  
# 生成从根到r1提交的所有patch
git format-patch --root <r1>　　　　　　　　　　　　   
```

* git am \ git apply应用patch

```shell
# 直接应用patch作者信息
git am 
# 需要重新add和commit
git apply
```

* git count-objects -v -H

```

```

* git bisect 

```shell
// 二分法排错
git bisect start HEAD XXXX
git bisect good
git bisect bad
```

