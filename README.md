学习Git用法
===========
Git is a version control system. Git is free software.
-----------
### 创建Git版本库
### 时光机穿梭
#### 版本回退
1. 查看log git log 或者 git log \<file\>
2. 查看版本修改或者文件修改 git show \<file | logid\>
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
Creating a new branch is quick & simple.