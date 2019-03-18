# Git
```
因为之前工作中基本都是使用的sourceTree,而且多人合作的开发项目的时候基本是每个人都有merge权限，直接合并到develop上，来到新公司之后，对应的要求一些比较规范的Git工作流，熟悉git command 迫在眉睫
```


## 一步一步使用git

```
mkdir gitfolder	创建gitfolder文件夹
cd gitfloder	切换到到当前目录下
git init   	初始化仓库
git remote add origin git@XXXX.com 本地仓库关联到远程仓库
```
**注:** 以上都是直接建立空的git仓库然后关联.也可直接使用`git clone git@XXXX.com`的方式直接克隆到本地。克隆之前本地需要设置[SSH](#ssh-配置).

```
1.branch
git branch 查看本地分支
git branch -r 查看远程分支名称 (  git remote -v  查看远程仓库地址)
git branch -a 查看所有分支
git branch -b 创建新分支
git branch -d (-D强制删除)删除分支

2.checkout
git checkout XX 切换到某分支
git checkout -- fileName 回退工作区的文件修改
git checkout -b  newBranch  xxbranch  从后面分支为基础，创建新分支
git checkout -b newBranch  origin/XXbranch 从远程创建新的分支
3.add
git add .  从工作区添加所有的改动到暂存区
git add XXfile 添加某一个改动到暂存区
4.commit
git commit -m “message” 从暂存区添加到版本库
git commit -a -m “message” 等同于 git add .       git commit -m “message”
git commit -am “message” 同上
5.log
git log 查看本地分支提交的commit 记录
git reflog 查看本的操作记录
git log --graph 图形化查看commit记录
git log --graph --pretty=oneline 图形化commit
5.reset
git reset —hard commitID   回退到某一版本
git reset HEAD file  回退暂存区内容到工作区

6.merge
git merge xxbranch //合并某分支到当前分支  fast-forwarding 。快速合并不保留信息
git merge —no-ff -m “merge message” xxbranch  作用同上，但是会保留合并的信息

7.push
git push origin xxbranch 向远程服务器推送当前分支
git push origin -d  xxbranch 删除远程服务器的某分支


8.diff git diff  查看文件改动区别
git diff HEAD file 查看某个文件的改动

9.stash
git stash  把工作区以及暂存的内容藏起来，这样切换分支的时候不会报错
git stash pop 把藏起来的内容 拿出来
git stash list 查看每次藏的记录

git status //查看文件改动

10reabse
git rebase -i master(from不包含)  dev(to 包含)
然后将pick 改为s(squash 挤压合并) 
原理就是：将master和dev之间的分支之间的改动全部全部复制到master之前的数据上。但是分支还是dev.  rebase的用法可以将几个commit合并为一个commit,可以修改commit 
如: git rebase -i commitID1 就可以修改commitID1之后的任意commit
git commit --amend 也可以修改最后一个提交的commit.


git branch --set-upstream-to=origin/<branch> newMaster //将某个分支跟远程分支建立联系

11.推送到远程
git push origin dev 将本地分支推送到远程
git push origin -d dev 删除远程分支

12.tag
git tag v1.1  打tag
git tag	查看全部的tag
git show v1.1 查看tag详情
git tag -d v1.1 删除tag
git push origin --tags 推送所有的未推送的tag
git push origin v1.1 把某个版本的tag推送到服务器
git tag -a v1.2 -m "tag	message" dev 在dev上打分支

git push origin :refs/tags/v1.1 删除服务器的某tag


 vim(vi)  file  打开或创建文件
rm file 删除文件
mkdir folder 创建文件夹
```



### ssh-配置
```
 配置SSH

1. cd ~/.ssh  

如果出现 -bash: cd: /Users/glamor/.ssh: No such file or directory，说明你之前没有用过。直接执行第二步。

如果之前用过需要清理原来的rsa，执行命令：mkdir key_backup $ cp id_rsa* key_backup $ rm id_rsa*

2 ssh-keygen -t rsa -C [shijun.ling@inin88.com](mailto:shijun.ling@inin88.com)   生成公钥秘钥  （在~/.ssh）

3.去gitlab里，把 生成公钥 导入的gitlab的ssh里

4.连接测试  ssh -T [git@github.com](mailto:git@github.com)

5.设置用户信息

git config —global user.name shijun.ling
git config —global user.email shijun.ling@inin88.com

git config —list //查看信息

~/.gitconfig 位置

$ git config user.name 查看
```
[ssh配置原文章](https://www.cnblogs.com/peteremperor/p/6135809.html)

