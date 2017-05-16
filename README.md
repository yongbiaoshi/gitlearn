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
- 查看远程分支：git branch -r
- 查看所有分支：git branch -a
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

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

在实际开发中，我们应该按照几个基本原则进行分支管理：
1. 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
2. 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

> **命令**
- 切换到分支dev git checkout dev
- 切回分支master git checkout master
- 合并（禁用Fast forward） git merge --no-ff -m "merge with no-ff" dev
> *注：因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。*

#### Bug分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

> **命令**
- 暂存当前修改 git stash 作用：把当前工作现场“储藏”起来，等以后恢复现场后继续工作
- 查看暂存内容 git stash list
- 恢复暂存内容 git stash apply stash@{0}
- 删除暂存内容 git stash drop
- 恢复的同时把stash内容也删了 git stash pop

#### Feature分支
开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D \<name\>强行删除。

> **命令**
- 强制删除分支 git branch -D \<name\>

#### 多人协作
当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

**推送分支**
> 推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：git push origin master
> 但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
> * master分支是主分支，因此要时刻与远程同步；
> * dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
> * bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
> * feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

多人协作的工作模式通常是这样：

首先，可以试图用`git push origin branch-name`推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

> **命令**
- 查看远程库信息 git remote
- 查看远程库详细信息 git remote -v，如果没有推送权限，则看不到push地址。
- 推送分支 git push origin \<分支名称\> 例：git push origin dev
- 在本地创建和远程分支对应的分支 git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致
- 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name
- 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。

### 标签管理

#### 创建标签
- 创建标签 git tag [-m \<msg\> | -F \<file\>] \<tagname\> [\<head\>]，创建标签，指定名称、版本号HEAD、描述信息
- git tag -l 列表所有标签
- git shwo \<tagname\> 查看标签说明

#### 操作标签
- 命令git push origin \<tagname\>可以推送一个本地标签；
- 命令git push origin --tags可以推送全部未推送过的本地标签；
- 命令git tag -d \<tagname\>可以删除一个本地标签；
- 命令git push origin :refs/tags/\<tagname\>可以删除一个远程标签。
