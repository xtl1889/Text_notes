# 记录一下git工作的使用和遇到的问题

git clone "----------" 克隆代码

/××××××××git的使用×××××××××××××××××××××××/

修改之前 git pull 更新一下代码

修改之后 git stash clear 清理缓存

再将本地的修改存起来  git stash

然后同步服务器最新的代码  git pull

把缓存的修改  恢复回来  git stash apply

如果有冲突 解决冲突 。。。

git add app/src (或者  .)
git commit -m "xxxxx"

git checkout .  清掉本地无用的修改

//git pull
git pull --rebase

git push origin master 提交

/×××××××××××××分支创建××××××××××××××××××/

1 查看远程分支
    git branch -a  

2 查看本地分支
    git branch  
  
3 创建分支
    git branch newBranch(分支名)
  
4 切换分支
    git checkout newBranch

5 线面是把分支推到远程分支 
    git push origin newBranch  
 
6 创建并切换到该分支（相当于3 4）
    git checkout -b newBranch
  
7 删除远程分支  
    git branch -r -d origin/branch-name  
    git push origin :branch-name  

/×××××××××××××分支合并××××××××××××××××××/

去自己的工作分支
  $ git checkout work

提交工作分支的修改
  $ git commit -a

回到主分支
  $ git checkout master

获取远程最新的修改，此时不会产生冲突
  $ git pull

回到工作分支
  $ git checkout work

用rebase合并主干的修改，如果有冲突在此时解决
  $ git rebase master

回到主分支
  $ git checkout master

合并工作分支的修改，此时不会产生冲突。
  $ git merge work

提交到远程主干
$ git push

这样做的好处是，远程主干上的历史永远是线性的。每个人在本地分支解决冲突，不会在主干上产生冲突。

/×××××××××××××××××××××××××××××××/

git reset --hard  清理

git reset HEAD^ 回退 commit

gitk .查看冲突

git status

git checkout commit的id  回退到改提交之前的代码
git checkout master      恢复到回退时候的代码

/***问题1*************************************************************/

有时遇到clone下来代码，在Android Studio中没有显示 Update project 和 Commit Changes 图标，而且更改代码 所在文件名没有变为蓝色(提示该文件已经修改),新建的文件名也不是红色(提示改文件为新增文件)，但是用命令提交代码是正常的。此时：VCS-->Enable Version Control Integration,选中git即可(将Android Studio项目进行初始化git)。
