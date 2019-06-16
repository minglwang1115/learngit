- 设置用户名：  git config --global user.name "myname"
- 设置邮箱:  git config --global user.email "myemail@xx.com"
>`初次使用必须先设置上面两个，用于区分不同用户`
- 创建版本库:  git init
- 添加文件:  git add readme.me
- 提交文件:  git commint -m "日志记录"
>`-m 相当于提交时的一个备注，用于记录这次提交都干了什么`
- 查看状态:  git status
- 查看工作区与暂存区(git add后的内容)版本对比:  git diff
- 查看暂存区(git add后的内容)与仓库分支(git commit后的内容)版本对比:  git diff --cached
- 查看工作区与仓库分支(git commmit后的内容)版本对比:  git diff HEAD -- filename
- 查看提交日志:  git log
- 版本回退:  git reset HEAD^
> `HEAD表示当前版本，HEAD^表示上一个版本，HEAD^^表示上上一个版本，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100`
- 查看命令历史记录:  git reflog
> `可以查看到每次的commit id,用于版本回退或回到未来版本`
- 丢弃工作区的修改:  git checkout -- file
>两种情况：
>一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
>一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
>总之，就是让这个文件回到最近一次git add时的状态。
- 撤销暂存区的修改:  git reset HEAD file
> git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
- 删除文件:  git rm file
> 注意一旦提交至版本库将无法恢复
> 1.如果你用的rm删除文件，那就相当于只删除了工作区的文件，如果想要恢复，直接用git checkout -- <file>就可以 2.如果你用的是git rm删除文件，那就相当于不仅删除了文件，而且还添加到了暂存区，需要先git reset HEAD <file>，然后再git checkout -- <file> 3.如果你想彻底把版本库的删除掉，先git rm，再git commit
- 添加远程库  git remote add origin git@github.com:XXX/learngit.git
- 将本地分支推送到远程仓库  git push origin master
- 克隆到本地仓库  git clone 远程仓库地址
- 查看分支：git branch
- 创建分支：git branch <name>
- 切换分支：git checkout <name>
- 创建+切换分支：git checkout -b <name>
- 合并某分支到当前分支：git merge <name>
> 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
- 删除分支：git branch -d <name>
- 暂使存储当前工作现场: git stash
> git stash应用场景：设A为游戏软件 1、master 上面发布的是A的1.0版本 2、dev 上开发的是A的2.0版本 3、这时，用户反映 1.0版本存在漏洞，有人利用这个漏洞开外挂 4、需要从dev切换到master去填这个漏洞，正常必须先提交dev目前的工作，才能切换(未提交就直接切换分支的话会报错，提醒必须先提交当前分支)。 5、而dev的工作还未完成，不想提交，所以先把dev的工作stash一下。然后切换到master 6、在master建立分支issue101并切换. 7、在issue101上修复漏洞。 8、修复后，在master上合并issue101 9、切回dev，恢复原本工作，继续工作。
- 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
>关联后，使用命令git push -u origin master第一次推送master分支的所有内容；把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
>此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
- 查看远程库信息，使用git remote -v；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
- 从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
- 创建标签:  git tag <name>
> 对某次提交创建标签  git tag <name> <commitid>
> 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：git tag -a v0.1 -m "version 0.1 released" 1094adb
- 查看标签列表:  git tag
- 查看某个标签详情:  git show <tagname>
- 命令git push origin <tagname>可以推送一个本地标签；
- 命令git push origin --tags可以推送全部未推送过的本地标签；
- 命令git tag -d <tagname>可以删除一个本地标签；
- 命令git push origin :refs/tags/<tagname>可以删除一个远程标签。