# study
study
Git study 

http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374831943254ee90db11b13d4ba9a73b9047f4fb968d000

git pull—>git add——>git commit——>git push origin master

通过git init命令把这个目录变成Git可以管理的仓库
初始化一个Git仓库，使用git init命令。

添加文件到Git仓库，分两步：
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit -m “注解”提交更改，实际上就是把暂存区的所有内容提交到当前分支。

要随时掌握工作区的状态，使用git status命令。

如果git status告诉你有文件被修改过，用git diff HEAD -- readme.txt可以查看修改内容。


HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard [commit_id || HEAD^ || HEAD^^]。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。



命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。



命令git rm fineName用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。


要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git(eg:git remote add origin git@github.com:michaelliao/learngit.git)；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；




Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除


用git log --graph命令可以看到分支合并图
git log --graph --pretty=oneline --abbrev-commit




合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并
git merge --no-ff -m "merge with no-ff" dev


修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。


因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。(eg:git branch --set-upstream dev origin/dev)

配置别名:
	git config --global alias.co checkout
 	git config --global alias.ci commit
 	git config --global alias.br branch