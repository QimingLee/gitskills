Git
$ git config --global user.name LiQiming
一、创建版本库
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
$ pwd
/c/Users/STEVEN'S ROG STRIX/learngit
STEVEN'S ROG STRIX@LAPTOP-MQSNEMIR MINGW64 ~/learngit
$ git init
Initialized empty Git repository in C:/Users/STEVEN'S ROG STRIX/learngit/.git/
STEVEN'S ROG STRIX@LAPTOP-MQSNEMIR MINGW64 ~/learngit (master)
$ git add readme.txt
STEVEN'S ROG STRIX@LAPTOP-MQSNEMIR MINGW64 ~/learngit (master)
$ git commit -m "wrote a readme file"
[master (root-commit) 146805f] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
初始化一个Git仓库，使用git init命令。
添加文件到Git仓库，分两步：
使用命令git add <file>，注意，可反复多次使用，添加多个文件；
使用命令git commit -m <message>，完成。
二、时光穿梭机
1.修改文件
git status 掌握仓库的状态，查看结果
git diff    
git add readme.txt
git status
git commit -m “  ” 
2.版本回退
git reset --hard HEAD^  or HEAD~100 or commit_id
git log (pretty=oneline)提交历史
git reflog 查看历史命令
//相当于改变了指针的位置
3.工作区和暂存区
    
4.管理修改
Git跟踪并管理的是修改，而非文件。
git cat readme.txt
git diff HEAD --  readme.txt 查看当前工作区与版本库最新版本的区别
每次修改，如果不用git add到暂存区，那就不会加入到commit中。
5.撤销修改
    场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，
就回到了场景1，第二步按场景1操作。
        场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
6.删除文件
rm test.txt  文件管理器删除
git status
git rm test.txt 版本库删除
git commit -m “ remove”
git checkout -- text.txt  
三、远程仓库
1.添加远程库
  要关联一个远程库，使用命令
git remote add origin git@server-name:path/repo-name.git；
关联一个远程库时必须给远程库指定一个名字，origin是默认习惯命名；
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，就可以使用命令git push origin master推送最新修改；
2.从远程库克隆
git clone git@github.com:QimingLee/gitskills.git
要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
Git支持多种协议，包括https，但ssh协议速度最快。
四、分支管理
1.创建与分支合并
   Git branch 
   Git branch <name>  创建分支
   Git checkout <name>  git switch <name> 切换分支
   Git checkout -b <name>  git switch -c<name> 创建+切换分支
   Git merge <dev> 将某分支合并到当前分支
   Git branch -d <name> 删除某分支
2.解决冲突
    当Git无法自动合并分支，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。
3.分治策略
    
  git merge --no-ff -m "merge with no-ff" dev
  合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
4.Bug分支
git stash
Git stash list
Git stash apply  恢复不删除
Git stash drop   删除
Git stash pop    恢复并删除
Git cherry-pick +文件序列 在master分支上修复的bug合并到Dev分支
5.Feature分支
  开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
6.多人协作
   Git remote   查看远程库的信息
   Git remote -v  显示详细信息
   Git push origin master 主分支
   Git push origin dev    开发分支
   git clone git@github.com:QimingLee/learngit.git
   Git branch
   git checkout -b dev origin/dev
   多人协作的工作模式通常是这样：
首先，可以试图用git push origin <branch-name>推送自己的修改；
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
如果合并有冲突，则解决冲突，并在本地提交；
没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。
7.rebase
五、标签管理
1.创建标签
    命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
命令git tag可以查看所有标签。
2.操作标签
git tag -d v0.1  删除本地标签
Git push origin  <tagname> 推送到远程
Git push origin  --tags 一次性全部推送到远程
git push origin :refs/tags/v0.9 删除一个远程标签

六、使用Github 
在GitHub上，可以任意Fork开源仓库；
自己拥有Fork后的仓库的读写权限；
可以推送pull request给官方仓库来贡献代码。
七、自定义Git
     忽略某些文件时，需要编写.gitignore；
.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！
八、搭建Git服务器