---
title: 【教程】git学习
date: 2016-07-28
tags: [教程,Git,GitHub]
categories: Git
---
# 一、简介  #
Git是目前世界上最先进的分布式版本控制系统（没有之一）。
## 1. Git的诞生 ##
Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！  
Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。
<!-- more -->
## 2. 集中式vs分布式 ##
中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。  
首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。
# 二、安装Git #
**在Windows上安装Git：**[下载地址](http://pan.baidu.com/s/1skFLrMt#path=%252Fpub%252Fgit)
安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。
# 三、创建版本库 #
版本库又名仓库（repository），可简单理解为一个目录，这个目录里的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都能追踪历史，或者在将来某个时刻可以“还原”。  
## 1. 创建版本库 ##
①创建一个空目录，自己选择合适的地方；  
**使用windows系统，为了避免各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文；**
②通过命令`git init`把目录变成可以管理的仓库；  
可以通过命令`git init file`创建一个文件夹并把这个文件夹变成Git可以管理的仓库；  
上面创建的是一个空的仓库（empty Git repository），此目录下有个`.git`的目录，这个目录是用了跟踪管理版本库的，谨慎修改；如果为看到此目录，使用`ls -ah`命令可以使默认隐藏的目录显示出来；  
 ## 2. 把文件添加到版本库 ##
所以的版本控制系统，只能跟踪文本文件的改动，比如txt文件，网页，程序代码等，都能明确地知道每次的改动内容；而图片，视频这些二进制文件，虽然能通过版本控制系统管理，但是没法跟踪文件的变化，只能把二进制文件每次改动串起来，例如图片从100k变为120k，但是到底改了什么，版本控制系统不知道，也没法知道；  
**文本是有编码的，强烈建议使用标准的UTF-8，所有语言使用同一种编码，既没有冲突，又被所有平台所支持；**  
**windows系统中，不要使用自带的记事本！！！**  
①创建一个文件，并放在Git仓库的目录下（子目录也行）；  
②用命令`git add`把文件添加到仓库；执行完成后，无任何显示，说明添加成功；  
③用命令`git commit`把文件提交到仓库；一般使用`git commit -m "xxx"`的方式提交，`-m`后面输入的是本地提交的说明，最好是有意义的，这样可以从历史记录中方便地找到改动记录；    
## 3. 小结 ##
初始话一个Git仓库，使用`git init`命令；
添加文件到Git仓库，分两步：
- 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
- 第二步，使用命令`git commit`，完成。
# 四、时光穿梭机 #
- 命令`git status`使我们时刻掌握仓库当前的状态；  
- 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容；
## 1. 版本回退 ##
使用`git log`命令查看历史记录；如果感觉内容太多，可以使用`git log --pretty=oneline`命令；  
`git log`命令可以看到一大串的字符是`commit id`（版本号）；  
回退到上一个版本，首先，Git必须知道是当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，上一个版本用`HEAD^`表示，上上一个版本就是`HEAD^^`，往上100个版本就写`HEAD~100`;  
版本回退使用`git reset`命名，回到上一个版本用命令`git reset --hard HEAD^`;  
想回到未来的某个版本：如果命令窗口未关闭，可以找到想回到的未来版本的`commit id`,使用命令`git reset --hard commit id`;如果命令窗口关闭，那么可以使用命令`git reflog`查看自己的每一次命令，找到要回到的未来版本的`commit id`,使用命令`git reset --hard commit id`；
## 2. 工作区和暂存区 ##
工作区（Working Directory）：在自己的电脑里能看到的目录；  
版本库（Repository）：工作区有一个隐藏目录`.git`，这个是Git的版本库；Git版本库里最重要的是stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。
`git add`把文件添加进去，实际上把文件修改添加到暂存区；  
`git commit`提交修改，实际上把暂存区的所有内容提交到当前分支；
## 3. 管理修改 ##
Git跟踪并管理的是修改，并非文件；  
如果暂存区和工作区存在差异，那么通过`git diff HEAD --file`查看差异；  
提交文件的时候，可以把多次提交到暂存区的文件一次提交到HEAD里面；
## 4. 撤销修改 ##
①当自己改乱了工作区的每个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`;  
②当自己不但改乱了某个文件的内容，还添加到了缓存区，想丢弃修改，分两步，第一步用命令`git reset HEAD file`,就回到了①，第二版按①操作；  
③已经提交了不合适的修改到版本库时，想要撤销本次修改，版本回退（前提是没有推送到远程库）；
## 5.删除文件 ##
在Git中，删除也是一个修改操作；  
一般情况下，通常直接在文件管理器中把没用的文件删了，或者是用`rm`命令删了；  
如果确实要从版本库中删除该文件，那就用命令`git rm file`删掉，并且`git commit`，现在文件从版本中被删除了  ；  
如果是删错了，因为版本库里还有，所有可以轻松的把误删的文件恢复到最新版本，使用命令`git checkout -- flie`;  
`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”；  
命令`git rm`用于删除一个文件；如果一个文件已经被提交到版本库，那么不用担心误删，但是要小心，只能恢复到最新版本，会丢失最近一次提交后修改的内容；  
# 五、远程仓库 #
[GitHub](https://github.com/)提供Git仓库托管服务，只需要注册帐号，就能免费获得Git远程仓库；  
1. 创建SSH Key：在用户主目录下，如果有.ssh目录，并且目录下面有`id_rsa`(这个是私钥，不能泄漏)和`id_rsa.pub`（这个是公钥，可以放心的告诉任何人）这两个文件直接跳到下一步；如果没有，打开Git Bash（window下），用命令`ssh-keygen -t rsa -C "your email@example.com"`创建；
2. 登录GitHub，打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，点“Add Key”，你就应该看到已经添加的Key；
## 1. 添加到远程仓库 ##
现在是本地已经创建了一个Git仓库后，又想在GitHub上创建一个Git仓库，并且让两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让他人通过该仓库来协作；  
①登录GitHub，在右上角找到“New repository”按钮，创建一个新的仓库，在Repository name填上名称，其他保持默认设置，点击“Create Repository”按钮，就成功创建一个新的Git仓库；  
②此时，GitHub上的这个仓库还是空的，我们把本地的仓库通过命令`git remote add origin git@server-name:path/repo-name.git`和远程库连接起来，用命令`git push -u origin master`第一次推送master分支的所有内容；    
③此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
## 2. 从远程仓库克隆 ##
假设从零开始，那么最好的方法是先创建远程库，然后从远程库克隆；  
①首先，登录GitHub，创建一个新的仓库，名称自定义；勾选`Initialize this repository with a README`,这样GitHub会自动为我们创建一个README.md文件，创建完成后，可以直接看到；
②现在远程库已经准备好了，下一步用命令 `git clone 远程库地址` 克隆一个本地库；  

Git支持多种协议，默认的`git://`（速度最快）使用ssh，也可以使用`https`（速度慢，最大的麻烦是每次推送都必须输入口令，但在某些只开放http端口的公司内部只能使用次协议）等协议；
# 六、分支管理 #
## 1. 创建与合并分支 ##
每次提交，Git把它们串成一条时间线，这条时间线就是一个分支；到目前为止，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支；`HEAD`严格来说并不是指向提交，而是指向`master`，`master`才指向提交，所以`HEAD`指向的就是当前分支；   
①一开始，`master`分支是一条线，Git用`master`指向最新的提交，在用`HEAD`指向`master`，就能确定当前分支及当前分支的提交点，每次提交，`master`分支就会向前移动一步，这样随着自己不断提交，`master`分支的线越来越长；   
②当我们创建新的分支，例如`dev`时，Git新建一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上（Git创建分支除了增加一个指针，改改`HEAD`的指向，工作区的文件没有任何变化！）；   
③从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针向前移动一步，而`master`指针不变；假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上，最简单的方法就是直接把`master`指向`dev`的当前提交，就完成了合并（合并分支只是改变指针，工作区内容无变化！）；   
④合并完成后，甚至可以删除`dev`分支，删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下一条`master`分支；  
----
查看分支：`git branch`    
创建分支：`git branch <name>`   
切换分支：`git checkout <name>`   
创建+切换分支：`git checkout -b <name>`   
合并某分支到当前分支：`git merge <name>`   
删除分支：`git branch -d <name>`   
## 2. 解决冲突 ##
如果两个分支都有提交新内容，并且新内容为一个地方，那么会产生冲突，此时Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，此时，必须手动解决冲突后再提交，通过`git status`可以告诉我们冲突的文件，直接修改冲突文件，再提交，此时冲突解决；  
用带参数的`git log`可以看到分支合并情况：`git log --graph --pretty=oneline --abbrev-commit`;   
最后删除分支;
## 3. 分支管理策略 ##
通常，合并分支时，如果可能，Git会用`Fast forward`（快速合并）模式，但这种模式下，删除分支后，会丢掉分支信息；  如果要强制禁用`Fast forward`模式，Git会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息；  
合并分支的时候，使用命令`git merge --no-ff -m "合并记录" <name>`，表示禁用`Fasr forward`模式，用`git log`可以查看分支历史；   
**在实际开发中，我们应该按照几个基本原则进行分支管理：**
1. 首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
2. 干活都在`dev`分支上，`dev`分支是不稳定的，到每个时候，发布版本时，再把`dev`分支合并到`master`上，在`master`分支上发布版本； 
3. 多人合作时，每个人都在`dev`分支上干活，每个人都有自己的分支，时不时的往`dev`分支上合并就可以了；
----
合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出曾经做过合并，而`fast forward`合并就看不出来曾经做个合并；
## 4. Bug分支 ##
在Git中，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除；   
接到一个bug时，我们想创建一个分支 `issue-1`来修复它，但是当前正在`dev`上进行的公司还没有提交（工作进行到一半，无法提交），Git提供了一个`stash`功能，可以把当前工作现场“存储”起来，等修改完成后可恢复现场后继续工作，使用命令`git stash`进行存储，此时用`git status`查看工作区，是干净的（除非有没有被Git管理的文件），此时可以放心的创建分支来修改bug；   
首先确定在那个分支上修复bug，假定需要在`master`分支上修复，就从`master`创建临时分支，然后修复bug，合并分支，删除临时分支`issue-1`；   
现在接着回到`dev`分支上干活，用命令`git stash list`查看隐藏起来的内容，现在有两种方法恢复：①用`git stash apply`恢复，但是恢复后stash内容并未删除，需要用`git stash drop`来删除；②用`git stash pop`,恢复内容的同时把stash内容也删了； 用命令`git stash list`查看，此时为空；   
可以多次stach，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令`git stash apply stash@{0}`;
## 5. Feature ##
添加一个新功能时，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支；   
如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除；
## 6. 多人协作 ##
当从远程仓库克隆时，实际上Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是origin；  
查看远程库的信息，用`git remote`，或者用`git remote -v`显示更详细的信息；  
1. 推送分支：   
推送分支就是把该分支上的所有本地提交推送到远程库；推送时，要指定本地分支，这样Git就会把该分支推送带远程库对应的远程分支上，比如推送到master分支`git push origin master`，推送到dev分支`git push origin dev`;   
但是并不是一定要把本地分支往远程推送，判读方法：   
   - `master`分支是主分支，因此要时刻与远程同步；
   - `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
   - bug分支只用于在本地修改bug，没必要推送到远程（除非老板要看修复的bug）；
   - feature分支是否推动到远程，取决与自己是否和小伙伴合作在上面开发； 
2. 抓取分支：
多人协作时，大家都会往`master`和`dev`分支上推送各自的修改；   
当从远程库clone时，默认情况下，只能看到本地的`master`分支，要是需要在`dev`分支上开发，就必须创建远程`origin`和`dev`分支到本地，用命令`git checkout -b dev origin/dev`命令创建本地`dev`分支；   
进行远程推送，如果失败，因为远程库的代码和自己试图推送的提交有冲突，解决办法是：先用`git pull`把最新的提交从`origin/dev`抓下来，然后本地合并，解决冲突，在推送；   
`git pull`也失败了，原因是没有指定本地的`dev`分支和远程的`origin/dev`分支的链接，用命令`git branch --set-upstream dev origin/dev`设置链接，然后再pull；如果`git pull`成功，但是合并有冲突，需手动解决，解决后提交再push；   
多人协作的工作模式通常是这样;
   - 首先，试图同过用`git push origin branch-name`推送自己的修改；
   - 如果推送失败，则因为远程分支比自己的本地更新，需要先`git pull`试图合并（如果`git pull`提示"no tracking information"，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`）；
   - 如果合并有冲突，则解决冲突，并在本地提交；
   - 没有冲突或解决掉冲突之后，再用`git push origin branch-name`推送就能成功；
3. 小结：
- 查看远程库信息，使用`git remote -v`;
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git push`抓去远程的新提交；
- 在本地创建和远程分支对应的分支,使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，先处理冲突；
# 七、标签管理 #
在发布新本版时，通常现在版本库中打一个标签，这样就唯一确定了打标签时刻的版本，将来无论何时取某个标签的版本，就是把那个打标签的时刻的历史版本取出来，所以标签也是版本库的一个快照；GIt的标签虽然是版本库的快照，但其实它就是指向某个commit的指针；   
## 1. 创建标签 ##
- 切换到需要创建标签的分支上，通过命令`git tag <name>`可以打一个新标签（这个标签默认是打在最新提交的commit上的）；
- 通过命令`git tag`查看所有标签；
- 通过命令`git tag <name> commit id`可以在任意一次提交的信息上打上标签；
- 标签不是按照时间顺序列出，而是按字母排序的；
- 可以用`git show <name>`查看标签信息；可以创建带有说明的标签，用命令`git tag -a <tagname> -m "解释文字" commit id`；
- 可以通过命令`git tag -s <tagname> - m "解释文字" commit id`用私密签名一个标签（签名采用PGP签名，因此首先安装gpg（GnuPG）,如果没有找到gpg，或者没有gpg密钥对，就会报错，如果报错，请参考GnuPG帮助文档配置Key）；
## 2. 操作标签 ##
- 如果标签打错了，用命令`git tag -d <tagname>`删除；
- 如果要推送某个标签到远程，使用命令`git push origin <tagname>`；
- 如果一次推送所有标签到远程，使用命令`git  push origin --tags`；
- 删除已经推送到远程的标签，先用命令`git tag -d <tagname>`从本地删除,然后用命令`git push origin :refs/tags/<tagname>`从远程删除（要查看是否真的从远程库删除了标签，可以登录GitHub查看）；
# 八、使用GitHub #
- 如何克隆别人的项目：Fork；
- 如何把项目拉取到本地，使用命令`git clone git@github.com:用户名/项目名.git（一定要从自己的帐号下clone仓库，这样才能推送修改）；
- 如果想修改别人的项目，需要在GitHub上发起一个pull request；
# 九、自定义Git #
Git显示不同的颜色`git config --gobal color.ui true`;    
## 1. 忽略特殊文件  ##
某些时候，必须把某些文件放到Git工作目录中，但又不能提交他们，比如保存了数据库密码的配置文件等，每次`git status`都会显示`Untracked files ...`，在Git工作区的根目录下创建一个特殊的`.gitignore`文件，然后把要忽略的文件名填进去，Git就会自动忽略这限额文件；GitHub为我们准备了各种配置文件，只需要组合一下就可以使用了；https://github.com/github/gitignore   
忽略文件的原则是：
- 忽略操作系统自动生成的文件，比如缩略图等；
- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另外一个文件自动生成的，那自动生成的文件没必要放进版本库，比如jaca编译产生的.class文件；
- 忽略自己的带有敏感信息的配置文件，比如存放口令的配置文件；
----
**小结：**
- 忽略某些文件时，需要编写`,gitignore`;
- `.gitignore`文件本身要放在版本库里，并且可以对`.gitignore`做版本管理；
## 2.配置别名  ##
`git config --global alias.st status`等；  
配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用；   
每个仓库的Git配置文件都放在`.git/config`文件里；   
别名在[alias]后面，要删除别名，直接把对应的行删掉就行；  
当前用户的Git配置文件放在用户主目录下的一个隐藏文件`.gitconfig`中；   
## 3. 搭建Git服务器 ##
省略...
# 十、总结 #
```
git命令   任何操作都需要以 git 命令为开头
本地操作：
git init  初始化一个本地仓库  新建为 master主分支
git status  查看当前分支状态
git add  <文件名>   将文件更改添加到分支状态中 相当于文件等待被提交
git commit -m <"描述信息">  提交并添加描述信息
git branch  查看分支   前面带*号的为当前所在分支
git branch <分支名称>  新建分支
git checkout <分支名>  切换分支
git checkout -b <分支名>  新建分支并切换到此分支
git merge <分支名>   将指定分支名合并到当前分支  一般为切换到主分支使用此命令
git merge --no-ff -m "提交描述" <分支名>   合并分支并提交
git branch -d <分支名>  有新建分支，那肯定有删除分支，假如这个分支新建错了，或者a分支的代码已经顺利合并到 master 分支来了，那么a分支没用了，需要删除，这个时候执行 git branch -d a 就可以把a分支删除了
git branch -D <分支名>  强制删除分支，不管分支是否有未提交合并的代码

git tag 查看所有标签
git tag <标签名> 在当前状态下新建一个标签，可用来当作版本号使用
git tag -a <标签名称> -m <"标签描述"> <提交id>  在指定的提交状态下新建一个标签
git show <标签名称>   查看标签的详情
git tag -d <标签名> 删除标签
git push origin <标签名>   推送标签到远程仓库
git push origin --tags  推送所有未推送的标签
git push origin :refs/tags/<标签名>   删除远程标签，本地要先删除后才可以


git checkout <标签名> 切换到标签名指定的状态
git diff <文件名> 查看文件修改内容

git log      查看提交日志   --pretty=oneline  此参数减少输出信息  穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
git reflog   要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
git log --graph --pretty=oneline --abbrev-commit   查看分支合并图
git reset --hard <HEAD^||提交ID> 穿梭到指定提交版本
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

git checkout -- <文件名>  将指定的文件恢复到最近一次 commit或add操作时候的状态
git reset HEAD <文件名>   将指定的文件从暂存区的修改撤销掉（unstage），重新放回工作区
git rm <文件名>		 删除指定的文件

git stash  把当前工作现场“储藏”起来，等以后恢复现场后继续工作
git stash list 查看暂存状态
git stash apply 恢复暂存状态
git stash drop  删除暂存状态
git stash pop   恢复并删除暂存状态
git stash apply <stash@{0}>  恢复指定的暂存状态


远征仓库操作:
git clone <远程地址>  从远征仓库拷贝过来代码，相当于建立本地分支
git pull 将最新的提交从远程仓库抓取下来
git push  将本地修改后的代码提交到远程仓库
git push <远程仓库名，默认origin> <本地分支名>  将指定的分支推送到远程分支上

git remote -v 查看远程仓库  -v 为详细信息

git checkout -b <本地支分支名> <远程仓库名，默认origin>/<远程支分支名> 拉取远程主分支下的支分支。。。
git branch --set-upstream <本地支分支名> <远程仓库名，默认origin>/<远程支分支名>  将本地分支与远程指定的分支关联起来

//以下为先有本地库，再建立远程库操作所用的命令
git remote add origin <URL地址> 本地库与远征库关联
git push -u origin master 关联后，使用命令第一次推送master分支的所有内容，   -u参数为推送当前分支所有内容

cat <file>
```