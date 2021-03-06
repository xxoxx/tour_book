## 配置
```shell
# 设置commit log中提交人的姓名和邮箱,仅在当前项目使用则用"--local"选项
$ git config --global user.name "xxx"
$ git config --global user.email "xxx@gmail.com"
# git命令的别名
$ git config --global alias.co checkout
$ git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
# 设置default editor
$ git config --global core.editor "vim"
# Git能够为输出到你终端的内容着色(高亮彩色显示)
$ git config --global color.ui true
# 设置显示中文文件名
$ git config --global core.quotepath false
# 设置git commit时的模板
$ git config --global commit.template $HOME/.gitmessage.txt
# 显示全部配置,部分则添加选项"--local|--global|--system"
$ git config -l
```

## 其他
- `git show <$id>` : 显示最近或某次提交的内容
- `git help <command>` :  显示command的help

## add
- `git add -u <file>` : 将文件修改提交到暂存区,"-u"表示仅添加修改和删除的文件,不包括新增.
- `git add .` : 将当前目录及其子目录内所有修改提交到暂存区

## rm
- `git rm <file>` : 将文件从工作区删除,仓库中的保留
- `git rm --cached <file>` : Git 将不再跟踪此文件，但它仍然保留在工作目录

## commit
- `git commit` : 向仓库提交,会启动一个文本编辑器来输入commit message.
- `git commit -m <message>` : 使用指定的commit message向仓库提交,此时不用启动文本编辑器
- `git commit --amend` : 修改最近一次的commit message

## reset

## diff
```shell
# 比较工作区和暂存区文件差异,"--stat"表示仅输出diff的统计信息,没有变动细节,"file"表示仅查看指定的文件
$ git diff [--stat] [<file>]
# 比较两次提交之间的差异
$ git diff <$id1> <$id2>
# 在两个分支之间比较
$ git diff <branch1>..<branch2>
# 比较暂存区和版本库差异
$ git diff --cached
```

## checkout
```shell
# 切换分支
$ git checkout <branch>
# 基于当前分支或$id创建新的分支，并且切换过去
$ git checkout [<$id>] -b <new_branch>
# 切换tag或切换commit
$ git checkout v1.0
$ git checkout ffd9f2dd68f1eb21d36cee50dbdd504e95d9c8f7
# 放弃工作区的修改
git checkout a.md
# 撤销对工作区修改(用git add或git commit中最近的文件来覆盖),"--"(参考bash)表示选项的结束,两个横线后面的部分都会被认为是参数了，而不再是前面的命令的选项了;"[<$id>|<branch>]"表示使用哪个commit或分支的文件来覆盖.
git checkout [<$id>|<branch>] [--] <file>；
git checkout . # .表示撤销当前目录及其子目录内所有文件的修改
```

## branch
- `git branch -r` : 查看所有的远程分支
- `git branch -a` : 查看所有分支(本机分支+远程分支)
- `git branch -v` : 查看各个本地分支最近的commit message
- `git branch <new_branch>` : 创建新分支new_branch,但不会立即切换到new_branch分支
- `git branch -d <branch>` : 删除分支branch

## fetch

## pull
- `git pull` : 抓取远程仓库所有分支更新并合并到本地

## push
- `git push` : push所有分支
- `git push origin master` : 将本地主分支推到远程主分支
- `git push -u origin master` : 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
- `git push origin <local_branch>:<remote_branch>` : 创建远程分支
- `git push origin :<remote_branch>` : 先删除本地分支，然后再push删除远程分支

## stash
```shell
# 把当前分支所有没有commit的代码(暂存区和工作区)先stash起来.message指stash记录的备注,"-u"表示新增文件也stash,"-a"表示在"-u"基础上.gitignore忽略的文件也stash,"-k"表示在stash后不会将暂存区重置,默认会重置暂存区和工作区.
$ git stash [save "message"] [-a -u -k]
# 查看stash记录
$ git stash list
# 还原某一stash,保留stash记录，默认恢复最近的;"--index"表示不仅恢复工作区，还恢复暂存区(默认情况下,恢复stash时原先暂存区的文件变更会回到工作区)
$ git stash apply [--index] [<stash>]
# 还原某一stash,删除该stash记录，默认恢复最近的
# git stash pop [--index] [<stash>]
# 删除某一个stash，默认删除最近的
$ git stash drop [<stash>]
# 清空stash
$ git stash clear
```

## remote
- `git remote` : 列出已经存在的远程分支
- `git remote -v` :  列出远程分支的详细信息(显示对应的克隆地址)
- `git remote show remote-name` : 查看某个远程仓库的详细信息
- `git remote add <name> <url>` : 添加一个新的远程仓库
- `git remote rename <old-name> <new-name>` : 重命名某个远程仓库在本地的简称
- `git remote rm <remote-name>` : 删除某个远端仓库
- `git remote set-url <remote-name> url` : 修改远程仓库的url

## log
- `git log [--stat] [-n] [-p] <file>` : 查看提交记录,"--stat"表示会显示提交的统计信息,"-n"表示选择显示前n条记录,"-p"表示按补丁格式显示commit的变更,"file"表示指定文件
