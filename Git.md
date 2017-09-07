# 记录一下git工作的使用和遇到的问题

git clone "----------" 克隆代码

/××××××××git的使用×××××××××××××××××××××××/

修改之前 git pull 更新一下代码

修改之后 git stash clear 清理缓存

再将本地的修改存起来  git stash

然后同步服务器最新的代码 git pull

把缓存的修改  恢复回来  git stash apply

如果有冲突 解决冲突 。。。

git add app/src (或者  .)
git commit -m "xxxxx"

git checkout .  清掉本地无用的修改

//git pull
git pull --rebase

git push origin master 提交

/×××××××××××××××××××××××××××××××/

git reset --hard  清理

git reset HEAD^ 回退 commit

gitk .查看冲突

git status

git checkout commit的id  回退到改提交之前的代码
git checkout master      恢复到回退时候的代码

/***问题1*************************************************************/

有时遇到clone下来代码，在Android Studio中没有显示 Update project 和 Commit Changes 图标，而且更改代码 所在文件名没有变为蓝色(提示该文件已经修改),新建的文件名也不是红色(提示改文件为新增文件)，但是用命令提交代码是正常的。此时：VCS-->Enable Version Control Integration,选中git即可(将Android Studio项目进行初始化git)。
