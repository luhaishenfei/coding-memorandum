git add -A

# push本地分支到远程github不存在分支
git push origin test

# git删除远程分支
git push origin --delete [branch_name]

# 删除本地分支区别
git branch -d 会在删除前检查merge状态（其与上游分支或者与head）。
git branch -D 是git branch --delete --force的简写，它会直接删除。