# 记录一下git工作的使用和遇到的问题

git clone "----------" 克隆代码

/××××××××git的使用×××××××××××××××××××××××/

修改之前 git pull 更新一下代码

修改之后 git stash clear 清理缓存

再将本地的修改存起来  git stash

然后同步服务器最新的代码  git pull

把缓存的修改  恢复回来  git stash apply

如果有冲突 解决冲突 。。。

处理完冲突后 git add (有冲突的文件路径) 将处理完的文件加入到 缓存   
然后在 git stash  apply

git add app/src (或者  .)
git commit -m "xxxxx"

git checkout .  清掉本地无用的修改

//git pull
git pull --rebase

git push origin master 提交

/×××××××××××××分支创建××××××××××××××××××/

1 查看远程分支    
    $ git branch -a  

2 查看本地分支   
    $ git branch  
  
3 创建分支    
    $ git branch newBranch(分支名)    
   
4 切换分支    
    $ git checkout newBranch

5 线面是把分支推到远程分支     
    $ git push origin newBranch  
 
6 创建并切换到该分支（相当于3 4）    
    $ git checkout -b newBranch
  
7 删除本地分支
    $ git branch -d <BranchName>
    
8 删除远程分支  
   $ git push origin --delete <BranchName>


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
  (如果有问题 git rebase --abort  命令可以撤销该操作)

回到主分支         
  $ git checkout master

合并工作分支的修改，此时不会产生冲突。             
  $ git merge work

提交到远程主干           
$ git push

这样做的好处是，远程主干上的历史永远是线性的。每个人在本地分支解决冲突，不会在主干上产生冲突。


将分支代码 合并到master

切换到主分支

$ git  merge newBranch(分支名称)

/××××××××××上传代码到git服务器×××××××××××××××××××××/
    
    
   进入代码目录  
   
   $git init  //初始化本地仓库   
   
   $git add * //或添加需要提交的文件     
   
   $git commit -m "init project" //提交到本地仓库的备注   
   
   $git remote add origin git@github.com:xtl1889/Text_notes.git //和远程仓库项目进行关联     
   
   $git push -u origin master //提交到远程仓库    
   
   
/××××××××××项目与git服务器断开连接×××××××××××××××××××××/    
    
 以android Studio项目为例：      
    1、进入项目根目录---->.idea--->vcs.xml     
    
      修改   
      
      <mapping directory="" vcs="Git" />     
        
      修改后   
      
      <mapping directory="" vcs="" />    
        
    2、删除跟目录下的 .git 目录  重新打开项目即可   
    
  
/×××××××××××××××××××××××××××××××/



/××××××××××××版本回退×××××××××××××××××××/                                                                                
   
      要回退的版本
    git reset --hard 139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96 

    把修改推到远程服务器
    git push -f -u origin master  
/×××××××××××××××××××××××××××××××/

/××××××××××××远程代码覆盖本地分支×××××××××××××××××××/
      
      下载远程仓库最新内容，不做合并
       git fetch --all
    1、 远程分支覆盖本地分支(如：远程master覆盖本地master分支代码 )
        进入master分支
        git reset --hard origin/master 
    2、远程master分支 覆盖本地 branch分支
        进入branch分支
         git reset --hard origin/master 

/×××××××××××××××××××××××××××××××/

git reset --hard  清理

git reset HEAD^ 回退 commit

gitk .查看冲突

git status

git checkout commit的id  回退到改提交之前的代码
git checkout master      恢复到回退时候的代码

/***问题1*************************************************************/      
有时遇到clone下来代码，在Android Studio中没有显示 Update project 和 Commit Changes 图标，而且更改代码 所在文件名没有变为蓝色(提示该文件已经修改),新建的文件名也不是红色(提示改文件为新增文件)，但是用命令提交代码是正常的。此时：VCS-->Enable Version Control Integration,选中git即可(将Android Studio项目进行初始化git)。    

/***问题2*************************************************************/            
    git branch -a  有时无法显示出来所以远程分支时
    执行 get fetch 将本地远程跟踪分支进行更新，与远程分支保持一致
    
    
    
/***问题3*************************************************************/      


  切换分支提示：
    error: The following untracked working tree files would be overwritten by merge:     
             bin/AndroidManifest.xml         
            Please move or remove them before you can merge.                    
            
       执行：
            git clean  -d  -fx    
            
    其中 
        x  -----删除忽略文件已经对git来说不识别的文件           
        d  -----删除未被添加到git的路径中的文件              
        f  -----强制运行     
        
  
  
  /***问题4*************************************************************/        
    
    git add . 后 不想提交了                 
    
    如果还没有commit  此时查看status之后，不想commit，希望撤回add之前的操作，但要保留修改（包括 新加文件、删除文件、已有文件修改等）        
    
    有两种方式                 

    一、 git reset -q                                

    二 、 git reset --mixed                                         
 
    注意不可使用 git reset --hard  或者 git reset --merge                            
    
    
    /***问题5*************************************************************/        
    
      更新或者克隆代码时提示：
      
      fatal: Could not read from remote repository.
        Please make sure you have the correct access rights
        and the repository exists.
        
     有可能是：远程代码地址有改动，本地关联的地址和远程分支地址不一致导致的。
     
      git remote -v    查看本地代码关联的地址
      git remote rm origin   删除关联的地址
      git remote add origin 新的地址路径   关联新的地址路径    
    
