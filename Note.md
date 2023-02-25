


笔记作于https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000


## 何为git？
git是一个分布式版本控制软件。能够记录文件的改动，甚至做到多人协同编辑
### 分布式与集中式的区别
集中式的版本库是在服务器上。集中式版本控制软件如SVN
分布式的版本库可以在多台电脑上，版本交替可在电脑之间直接完成，一般会使用一个服务器（例github）作为中间层方便交替


## 工作区和版本库的概念
正常工作区域的文件夹就叫工作区
版本库是git init创建的.git文件夹

### 暂存区
暂存区用来暂时保留修改（add）
当所有修改结束后，可以使用commit将暂存区中所有的修改添加到分支

### 分支
一开始git会自动创建一个master的分支


## 操作



### 文件操作
#### 添加文件到暂存区
> 把要提交的所有添加放到暂存区

git add [filename]


#### 将文件（从版本库）删除
> 把删除命令添加到暂存区

git rm [filename]


#### 提交文件到仓库
> 一次性把暂存区的所有修改提交到分支

git commit
git commit -m "some comment"

#### 查看文件变化
```
git diff  -- [filename]			查看工作区文件和暂存区文件的区别
git diff HEAD -- [filename]		查看工作区文件和最新版本的对应文件的区别
git diff [commit id] [filename]		查看文件和对应版本中的文件的区别
```

#### 丢弃工作区修改

```
git checkout -- [filename]

必须加上 -- 否则会被当做是切换分支
若file之前未放入暂存区，则从版本库中恢复
若file之前放入暂存区，则从暂存区恢复
```

### 分支/版本相关
#### 创建版本库
git init	初始化版本库

#### 分支相关

##### 创建分支

一：
git branch [branchName]
二：
git checkout -b [branchName]
创建并切换分支
三：
git switch -c [branchName]
创建并切换分支

##### 切换分支
方法一：
git checkout [branchName]
方法二：
git checkout -b [branchName]
创建并切换分支
方法三：
git switch  [branchName]
切换分支。推荐


##### 合并分支
git merge [branchName]
> 让当前分支与指定分支合并

##### 删除分支
git branch -d [branchName]

git branch -D [branchName]
> 若branch还没有merge就使用-d删除会git会报错
> 此时使用-D可以强制删除此分支

##### 查看分支
git branch
> 显示所有分支，当前分支前有*表示


##### 查看分支/版本信息
git log
```
commit 1679dcde285aafa5ba955357453a63d63f1e6abd (HEAD -> master)
Author: BAZ <1344395710@qq.com>
Date:   Sun Dec 16 10:41:19 2018 +0800

    append GPL

commit e2371ba23e261bcdb9e34286d4708e2ed8afede8
Author: BAZ <1344395710@qq.com>
Date:   Sun Dec 16 10:35:44 2018 +0800

    test using status,diff

commit 6e26953719e8815cd25268b6529f6611f73d7bb5
Author: BAZ <1344395710@qq.com>
Date:   Sun Dec 16 10:11:24 2018 +0800

    multiply test
```

git log --pretty=oneline
> 只显示commit id和comment

--graph
> 以图的形式显示分支的情况
> 常用于显示多个分支之间的关系

--abbrev-commit

> 缩写commit id


```
1679dcde285aafa5ba955357453a63d63f1e6abd (HEAD -> master) append GPL
e2371ba23e261bcdb9e34286d4708e2ed8afede8 test using status,diff
6e26953719e8815cd25268b6529f6611f73d7bb5 multiply test
ad9bb867f6ebce6d2ad25aabe95853d9ad38a5b6 my first git
```

##### 查看全部分支（包括HEAD前的）

git reflog

##### 分支整理

git rebase

#### 版本相关
##### 版本回退

```
git reset --hard HEAD

> HEAD当前版本，HEAD^表示上一个版本，HEAD^^表示上上个版本，以此类推。HEAD~100表示上一百个版本

git reset --hard [commit id]

> 这里commit id可以不写全（但最少要有四个字符），有自动补全

git reset HEAD [filename]

> 删除将该文件在暂存区的修改
```




#### 标签
##### 创建标签
git tag [tag]
> 在当前分支的当前版本下创建标签

git tag [tag] [commit id]
> 对指定commit创建标签
> commit id可以缩写

git tag -a [tag] -m "comment" [commit id]
> 设置说明文字（-m）
> 这里的-m参数和git commit的-m意思一样，作用的对象不一样。
> tag的-m作用于tag，表示tag的说明文字
> commit的-m作用于commit，表示commit的说明文字

##### 删除标签
git tag -d [tag]


##### 查看所有标签
git tag
> 标签按字符串比较排序


##### 查看标签对应的版本信息
git show [tag]

##### 推送标签至远程库
git push origin [tag]
> 推送某一个tag

git push origin --tags
> 推送所有tage


##### 删除远程库的标签
git tag -d [tag]
git push origin :refs/tags/[tag]





### 存储工作区
#### 存储当前工作区
git stash
> 存储后会自动跳转到当前分支的当前版本

#### 查看已存储的工作区列表
git stash list

#### 恢复并删除工作区
git stash pop

#### 恢复工作区
git stash apply
> 恢复后会自动显示git status的信息

#### 从列表中删除存储的工作区
git stash drop



### 掌握仓库状况
git status
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```







### 查看git命令log
git reflog

```
1679dcd (HEAD -> master) HEAD@{0}: reset: moving to HEAD
1679dcd (HEAD -> master) HEAD@{1}: commit: append GPL
e2371ba HEAD@{2}: commit: test using status,diff
6e26953 HEAD@{3}: commit: multiply test
ad9bb86 HEAD@{4}: commit (initial): my first git
```



### 远程仓库相关
详见https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013752340242354807e192f02a44359908df8a5643103a000
SSH连接
#### 关联一个远程库
git remote add origin git@server-name:path/repo-name.git
例:
git remote add origin git@github.com:TF-BAZ/GitTest.git



#### 推送
git push origin [branchname]
branchname一般为master
第一次推送：
git push -u origin [branchname]



#### clone
git clone [path]
例：
`git clone git@github.com:TF-BAZ/CloneTest`