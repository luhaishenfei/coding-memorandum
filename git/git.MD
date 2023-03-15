# Baise


# ---branch option---
# 列出分支
git branch

# 切换分支
git checkout 分支名

# 创建新分支并立即切换到该分支下
git checkout -b (branchname)

# 删除分支
git branch -d (branchname)

# 分支合并

# 将 分支1 合并到当前分支去
git merge 分支1




git add -A

# push本地分支到远程github不存在分支
git push origin test

# git删除远程分支
git push origin --delete [branch_name]

# 删除本地分支区别
git branch -d 会在删除前检查merge状态（其与上游分支或者与head）。
git branch -D 是git branch --delete --force的简写，它会直接删除。



假设： dev是主分支
dev_local 是本地分支
 
1、创建本地分支：
git checkout -b dev_local
或在之前的本地分支上拉取最新数据
git pull origin dev
 
2、修改dev_local 中的代码后
git add .
git commit -m "merge dev_local to dev"
 
3、切换分支到dev
git checkout dev
 
4.合并dev_local 到 dev
git merge dev_local
 
5、push 到远程分支
git push origin dev
 
6、删除本地dev_local 分支（看开发情况，需要就删，不需要就不删除）
git branch -d dev_local