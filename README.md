学习Git用法
===========
Git is a version control system. Git is free software.
-----------
### 创建Git版本库
### 时光机穿梭
#### 版本回退
1. 查看log git log 或者 git log \<file\>
2. 查看版本修改或者文件修改 git show \<file | versionId\>
#### 工作区和暂存区

#### 管理修改
1. Git管理的是修改，而不是文件

#### 撤销修改
1. 未执行git add的修改，git checkout -- file
2. 已经执行git add放到暂存区的修改，git reset HEAD file 

#### 删除文件
1. 删除本地文件 rm test.txt
2. 删除版本库文件 git rm test.txt && git commit -m "remove test.txt"

### 远程仓库
#### 添加远程仓库
1. 在GitHub上创建一个新的仓库
2. git remote add origin https://github.com/yongbiaoshi/gitlearn.git
3. git push --set-upstream origin master 
#### 从远程库克隆
1. git clone https://github.com/yongbiaoshi/gitlearn.git
> *注：Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。*
### 分支管理
#### 创建与合并分支
- 查看分支：git branch
- 创建分支：git branch \<name\>
- 切换分支：git checkout \<name\>
- 创建+切换分支：git checkout -b \<name\>
- 合并某分支到当前分支：git merge \<name\>
- 删除分支：git branch -d \<name\>
> *注：Git鼓励大量使用分支*
#### 解决冲突
- 冲突之后，手动解决冲突后再提交。git status查看冲突文件。
> *注：解决方式就是手动编辑，然后git add、git commit*
- 查看分支合并情况 git log --graph --pretty=oneline --abbrev-commit
> *注：--graph：图表，--pretty=online：单行显示日志，--abbrev-commit：版本号缩写*
#### 分支管理策略

通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

在实际开发中，我们应该按照几个基本原则进行分支管理：
1. 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
2. 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

**命令**
- 切换到分支dev git checkout dev
- 切回分支master git checkout master
- 合并（禁用Fast forward） git merge --no-ff -m "merge with no-ff" dev
> *注：因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。*