```
git init  创建版本库
git add <filename> <filename2> ...  添加文件到仓库
git commit -m "commit msg"   提交-日志

git remote add origin <remote repositery>   关联远程库
git clone <远程地址>       克隆远程仓库到当前目录

git branch dev 创建dev 分支
git checkout dev 切换到dev分支
git checkout -b dev 创建并切换到dev分支

git branch  查看当前分支
git branch -d dev 删除dev 分支

git stash 存档未完成工作，未添加的工作，命令会使工作区域clean.当push 之后可以使用git stash list 查看，使用git stash pop 恢复并删除存档

加别名
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch

-先删后加
git remote rm origin
git remote add origin [url]

- 修改远程的名字
把 origin2 重命名为 origin
git remote rename origin2 origin


删除远程分支
git push [远程名]  :[远程分支名]
git push origin :translate  --------- 相当于用空白代替了远程分支，达到删除目的

获取远程分支
git fetch 远程名  如git fetch origin

创建分支并与远程分支链接
git checkout -b [要创建的本地分支名] [远程名]/[远程分支名]

把本地分支推送到远程
git push [远程名]  [要创建的远程分支名]: [本地分支名]
如果是 git push origin [本地分支名] 则会在远程创建一个与本地分支名相同的分支并与本地分支相关联。
.gitignore 忽略文件需要版本库中没有这个文件，如果已经有了这个文件，添加到ignore也没用

修改最近的 commit 的 message
git commit --amend
会打开一个编辑器

git commit --amend -m "new commit message"

回退
假如git log 显示的结果为
commit id1
commit id2
git reset --soft id2    当前指向 id2, 把 id1 的修改变成 已添加 待提交 状态
git reset --hard id2   把 id2 时的代码完全覆盖到本地，本地为 clean 状态，丢失 id1 所做的所有修改。
如果你还记得 id1, 可以通过 git reset --hard commit-id 回到之前的状态; 
也可以使用 git reset id1 找回之前所做的修改，状态是待 add 状态。

```
