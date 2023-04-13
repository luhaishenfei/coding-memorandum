# Baise

git add -A
git add .
git commit -m "xxxxxx"

或在之前的本地分支上拉取最新数据
git pull origin dev
 
# 列出分支
git branch

# 切换分支
git checkout 分支名

# 创建新分支并立即切换到该分支下
git checkout -b (branchname)

# 将本地分支与远程分支关联
git remote add origin https://github.com/luhaishenfei/kafka.git

# 删除分支
git branch -d 会在删除前检查merge状态（其与上游分支或者与head）。
git branch -D 是git branch --delete --force的简写，它会直接删除。

# 分支合并

# 将 分支1 合并到当前分支去
git merge 分支1


## push推送

# push本地分支到远程github不存在分支
git push origin test

# git删除远程分支
git push origin --delete [branch_name]

# ---远程分支---

# git设置本地与远程分支关联
1.为了避免每次都进行验证，在git进行绑定ssh
mkdir ~/.ssh　　
ssh-keygen -t rsa -C "xxx@qq.com"
将生成的公钥粘贴到git中


2.本地推送代码到git（初始情况下，git中无项目）
在项目目录执行如下操作：

git init（初始化本地仓库）

git remote add origin https://github.com/xxx.git（相当于和远程建立了关系，origin是远程仓库的别名，可以自定义，相当于代替了url）

3.从远程分支拉取代码到本地

格式：git pull <远程主机名> <远程分支>:<本地分支> 

可简化为 git pull <远程主机名> <远程分支>（从远程分支拉取代码合并到本地当前分支）

示例：git pull origin master（这样就会将远程分支关联下来到本地当前分支）

4.查看本地与远程分支关联情况

git branch -vv

5.设置本地与远程分支关联

git branch --set-upstream-to=origin/branch branch（前面branch为远程分支名，后面branch为本地分支名）

6.创建远程分支

格式：git push <远程主机名> <本地分支名>（省略远程分支名，把本地分支推送到它追踪的远程分支）

示例：git push origin master　　（将本地的 master 分支推送到 origin 主机的 master 分支）

7.创建远程分支并且关联到远程分支

格式：git push --set-upstream <远程主机名(远程仓库名，一般设为origin)> <本地分支名>:<远程分支名>

示例：git push --set-upstream origin local:remote

8.提交本地test分支到远程的master分支：

格式：git push <远程主机名> <本地分支名>:<远程分支名>

示例：git push origin test:master

9.如果当前分支与多个主机存在追踪关系，则可以使用 -u 选项指定一个默认主机，这样后面就可以不加任何参数使用git push

git push -u origin master（将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了，git push -u origin master 相当于 git branch --set-upstream-to=origin/master master（将远程仓库origin的master分支与本地仓库master分支关联）加 git push origin master）

10.删除远程分支

git push origin :master（推送一个空分支到远程分支，其实就相当于删除远程分支)   或   git push origin --delete xxx

11.remote: CODING 提示: Authentication failed. remote: 认证失败，请确认您输入了正确的账号密码

git config --system --unset credential.helper（即可重新弹窗填写密码）

12.回退版本

git reset --hard b2342afas7s8as7d7d98989fa98f9f9

git push -f origin develop

13.撤销上次提交（撤销后修改的代码也会撤销，log中会撤销上次提交记录）

git reset --hard HEAD^（HEAD是指向最新的提交，上一次提交是HEAD^，上上次是HEAD^^，也可以写成HEAD～2 ，依次类推）

git push -f origin master

--------




