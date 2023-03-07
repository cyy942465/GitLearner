# 远程连接

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911160948454.png" alt="image-20220911160948454" style="zoom:80%;" />

## 步骤

1. `git init`初始化本地仓库
2. `git remote add origin url` 建立连接，origin引用url
3. `git push -u origin master `将数据同步到master

# Branches

## 理论

local branch 和 remote branch没有什么关系

remote tracking branch 是 local branch 的只读副本

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911165854225.png" alt="image-20220911165854225" style="zoom:80%;" />

local tracking branch 与 remote tracking branch连接

是remote branch 的副本

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220912102511164.png" alt="image-20220912102511164" style="zoom:80%;" />

## 命令

1. `git branch -a`： 查看本地和remote tracking branch的分支
    ![image-20220911165707203](C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911165707203.png)

2. `git push origin 分支名`： 将当前分支的数据推送到远程分支，如果分支名没有则会在远程创建新分支
   但是当前分支不是local tracking branch

3. `git push -u origin 分支名`： 将当前分支设置为对应分支的local tracking branch

4. `git ls-remote`：获取所有远程分支
    <img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220911171151287.png" alt="image-20220911171151287" style="zoom:80%;" />

5. `git fetch origin `： remote tracking branch与远程仓库分支合并
6. `git pull origin 分支名`： 拉取远程仓库的分支并与本地当前分支合并,相当于fetch和merge的合并
7. `git branch --track “local tracking branch” “remote tracking branch(origin/)”` ： 创建连接到remote tracking branch 的 local tracking branch，两个名称需要保持一致便于后面push

## 总结

### 分支

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220912105128190.png" alt="image-20220912105128190" style="zoom: 80%;" />

# clone

将远程仓库复制到本地

## 命令

- `git clone url`： 复制仓库，并且会位于main的一个local tracking branch内
- `git branch -m master main`： 把master分支改名为main

# 删除和提交远程分支

## 删除分支

- `git branch --delete --remotes 分支名（origin/）`：删除远程分支（remote tracking branch）
- `git push origin --delete 分支名（feature）`： 删除remote branch

## 撤销commit

1. `git reset --hard HEAD~1`：撤销本地commit
2. `git push --force origin master`： 同步远程

#  Fork 和 pull request

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20220912203819736.png" alt="image-20220912203819736" style="zoom:80%;" />

# 项目开发实例

## .gitignore

node_modules

## git branch -m master main

将master分支更名为main

## git pull

拉取远程仓库的最新状态

## git merge 分支名

合并

# ssl

```
git config --global http.sslVerify "false"
```

