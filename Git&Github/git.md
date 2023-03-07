# The Basics

## 工作原理

### commit

用于跟踪文件的变化，而不是一次次存储文件

在branch中管理

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220910152518529.png" alt="image-20220910152518529" style="zoom:80%;" />

### .git隐藏文件

add会先被提交到缓存区（staging area），然后由commit将改变提交到commits中

![image-20220910153449645](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220910153449645.png)

### Branches

#### master

所有的commit默认会被提交到master branch中，管理着项目的不同版本

#### 其他分支

项目的完整副本，拥有master中的所有commit，同时也可以独立于该分支工作

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220910154013427.png" alt="image-20220910154013427" style="zoom:80%;" />

#### merge

将其他分支的commit整合到master中

## 命令

### git init

初始化Git reporsitory

### git status

查看当前git存储库(reporsitory)的状态

### git add 文件名

`git add .`跟踪项目文件中的所有文件，添加到缓存区

### git commit -m “message内容”

将缓存区的文件提交到存储区

### git log

打印日志，记录着每一次commit的ID

### git checkout

用于切换不同的分支 `git checkout branchName`

### git branch

查看当前分支

`git branch branchName` 创建一个新的分支

### 创建分支的快捷方式

`git checkout -b branchName` 

创建一个分支并切换到当前分支

### git merge 分支名

将另一个分支合并到当前分支

## HEAD

### the HEAD

hte HEAD是当前分支最新一次更新（commit）的引用

### detached HEAD

查看特定的commit，不属于任何分支

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911122550546.png" alt="image-20220911122550546" style="zoom:80%;" />

![image-20220911122746437](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911122746437.png)

## 新命令

### git switch

`git switch 分支名`： 切换到另一个分支

`git switch -c 分支名`：创建并切换到新的分支

## Deleting Data

### 命令

#### git ls-files

查看暂存区文件

#### git rm/add 文件名

从暂存区中实际删除文件

之后再使用commit指令

### 撤回在缓存区的变化

缓存区：还没add，刚保存

#### 撤回文件内的变化

使用 `git checkout ./文件名`

或者使用 `git restore ./文件名`

#### 撤回新建的文件/未被追踪的文件

使用 `git clean -dn` 列出会删除的文件

再使用 `git clean -df`进行删除

### 撤回在add

暂存区：add之后

#### 撤回文件内的变化

使用 `git reset 文件名` 再使用 `git checkout 文件名`返回到之前的状态

或者直接使用 `git restore --staged 文件名` 再使用 `git checkout 文件名`

### 撤回commit

- `git reset --soft HEAD~1`：将最后一次commit删除，但是仍然保留再缓存区
- `git reset HEAD~1`：如果要删除缓存区文件，但是工作区仍然会保留文件
- `git reset --hard HEAD~1`：彻底删除该文件

### 删除branch

`git branch -D 分支名`

## .gitignore

记录需要忽略的文件或文件夹

- `*.log`: 所有以.log结尾的文件

- `!`:表示豁免的文件
- `file-name/*`: 表示忽略文件夹内的所有文件

# 进阶

## git stash

允许保存为add的更改

### 用法

- `git stash`：保存工作进度并返回到最新的一次commit

- `git stash apply`： 返回更改

- `git stash list`： 列出存储的所有更改，配合 `git stash apply 编号`可以返回到指定的修改

  最上面的（0）永远是最新的stash
  ![image-20220911141433030](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911141433030.png)

- `git stash push -m ""`：保存进度时会添加描述信息

- `git stash pop 编号`： 取出保存的进度，从stash list 中删除

- `git stash drop 编号`：单纯删除stash list里面的项目

- `git stash clear`： 删除所有的stash

## git reflog

可用于查找三十天内的所有commits

找到reset的commit

![image-20220911142805489](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911142805489.png)

再次reset，回滚到这次commit

### 应用场景

删除分支后回滚该分支的commit

## 合并分支

### 合并类型

#### fast-forward

没有创建新的commit，只是单纯的移动HEAD

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911143804034.png" alt="image-20220911143804034" style="zoom:80%;" />

`git commit --squash feature`： 将其他分支的commit合成一个commit并add到要merge的分支中

#### Recursive Merge

在master中会有要merge分支的所有commit并且提交一个merge commit来合并

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911145725517.png" alt="image-20220911145725517" style="zoom:80%;" />

`git merge --no-ff ` 

### rebasing

创建与分支相同的commit来合并到master上

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911150319336.png" alt="image-20220911150319336" style="zoom:80%;" />

`git rebase 分支名`

### cherry-pick

挑选特定的commit与master进行merge，创建该commit的副本（新ID）并提交到master中

`git cherry-pick ID`

### Conflicts

同个文件的内容在不同分支中被改变后merge

`git merge --abort`：中止合并

`git diff`： 显示冲突内容

#### 处理

- 接收当前
- 接收改变
- 合并

选择后需要提交commit让merge生效

## git tag

为commit添加索引标签

`git tag 标签 ID`: 为commit 添加索引标签

`git tag` ： 显示当前所有的索引标签	

`git show 标签` ： 显示该标签对应commit的信息

`git tag --d 标签`：删除该索引标签

`git tag -a 索引标签 -m "message"` ： 为当前commit添加标签