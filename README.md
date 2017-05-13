学习Git用法
===========
Git is a version control system. Git is free software.
-----------
1. 创建Git版本库
2. 时光机穿梭
> 版本回退

> 工作区和暂存区

> 管理修改
>> Git管理的是修改，而不是文件

> 撤销修改
>> 1. 未执行git add的修改，git checkout -- file
>> 2. 已经执行git add放到暂存区的修改，git reset HEAD file 

> 删除文件
>> 1. 删除本地文件 rm test.txt
>> 2. 删除版本库文件 git rm test.txt && git commit -m "remove test.txt"

3. 远程仓库
> 添加远程仓库
>> 1. 在GitHub上创建一个新的仓库
>> 2. git remote add origin https://github.com/yongbiaoshi/gitlearn.git
>> 3. git push --set-upstream origin master 
