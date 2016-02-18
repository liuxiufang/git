# git的简介、安装、使用
### 1. git的来源
> Linus在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？那么问题来了，很多有兴趣的编者，便开始自我研究，开发Samba的Andrew试图破解BitKeeper的协议，从此git便诞生了。

> Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。

> 有人又会说为 什么不用svn、 cvs 这些版本控制呢!那么小编会告诉你，svn、 cvs都是集中式的版本控制系统，而git 则是分布式版本控制系统，那么问题又来了，两者又有什么区别呢？

> 首先，集中式版本控制是存放在中央服务器的，而开发者是从本地工作的，所以工作者是从中央服务器取得最新的版本，然后进行工作，工作完成后，在把文件推送给中央服务器， 由此可见，如果中央服务器出现问题，那么工作者就不能愉快的工作了，而且集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊。
> 哪布式版本控制系统又如何工作呢？分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。也可以通过github 存储托管， 工作完成后可以推送给github，方便其他的工作者方便的使用和继承。

> 简单的介绍下，那么现在小编带你们开始安装和使用git！

### 2. git的安装
######  在Linux上安装Git
首先，你可以试着输入git，看看系统有没有安装Git：
一般linux 会自带git 功能,那么接下来可以设置一下自己所属git的

`$ git config --global user.name "Your Name"`  
`$ git config --global user.email "email@example.com"`  

注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址 

那么好现在才刚刚开始使用git！

什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。  
` mkdir learngit `  
如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。  
` $ git init `  
初始化仓库  
` Initialized empty Git repository in /Users/michael/learngit/.git/`  
瞬间git仓库创建好了，那么会在目录下面生生一.git的目录可用ls -ah 查看  
把文件添加到仓库 总共分两步:  
` $ git add file.txt`  
` $ git commit -m "describe"`  
简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。  
嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。  
现在我们成功提交了一个文件到仓库中，那么可以查看一下状态，看看有木有修改过的文件  
` $ git status `  
` # On branch master `  
` # Changes not staged for commit: `  
` #   (use "git add <file>..." to update what will be committed) `  
` #   (use "git checkout -- <file>..." to discard changes in working directory) `  
` # `  
` #    modified:   readme.txt `  
` # `  
` no changes added to commit (use "git add" and/or "git commit -a") `  
也可以通过
` $ git diff `  
来对比两个文件的差异  
```
git diff readme.txt  
diff --git a/readme.txt b/readme.txt  
index 46d49bf..9247db6 100644  
--- a/readme.txt  
+++ b/readme.txt  
@@ -1,2 +1,2 @@  
-Git is a version control system.  
+Git is a distributed version control system.  
 Git is free software.  
 ```
 git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个“distributed”单词。  
 想查看git的日志可以
 ` $ git log `  
 git log命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是append GPL，上一次是add distributed，最早的一次是wrote a readme file。 如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：  
 ```
 $ git log --pretty=oneline  
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL  
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed  
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file  
```  
需要友情提示的是，你看到的一大串类似3628164...882e1e0的是commit id（版本号），和SVN不一样，Git的commitid不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。  

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：  

如果提交了文件，存在错误想撤销回到上一个版本：  
```
$ git reset --hard HEAD^  
HEAD is now at ea34578 add distributed  
```  
注意：Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。  

例如:  
```
$ git log  
commit ea34578d5496d7dd233c827ed32a8cd576c5ee85  
Author: Michael Liao <askxuefeng@gmail.com>  
Date:   Tue Aug 20 14:53:12 2013 +0800  

    add distributed  
 
commit cb926e7ea50ad11b8f9e909c05226233bf755030  
Author: Michael Liao <askxuefeng@gmail.com>  
Date:   Mon Aug 19 17:51:55 2013 +0800  

    wrote a readme file  
 
$ git reset --hard 3628164  
HEAD is now at 3628164 append GPL  

```  
那么文件已经成功的回退到指定的版本。  
现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？  

在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到add distributed版本时，再想恢复到append GPL，就必须找到append GPL的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：  

```
$ git reflog  
ea34578 HEAD@{0}: reset: moving to HEAD^  
3628164 HEAD@{1}: commit: append GPL  
ea34578 HEAD@{2}: commit: add distributed  
cb926e7 HEAD@{3}: commit (initial): wrote a readme file  

```  

说到这里，那么下面来认识一下git 工作区和暂存区  

所谓的工作区，就是你现在本地的能看的目录比如刚刚创建的learngit就是你的工作区  
版本库：就是你通过 $ git commit 把目录提交到的地方，  
前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；  

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。 

可以查看暂存区和最近一次提交的不同:  
` $ git diff --cached `  
注意的是，只有在 暂存区的文件commit后才能提交到版本库当中。  

git diff：是查看工作区与暂存区的差别的。   
git diff --cached：是查看暂存区与commit的差别的。  
git diff HEAD：是查看工作区和commit的差别的。（你一定没有忘记，HEAD代表的是最近的一次commit的信息）  

学会了 提交、查看那么又有人会问到，如果我写错了，想撤销我刚才的操作该如何做呢！别急下面介绍一下如何撤销：  
你可以发现，Git会告诉你，git checkout -- file可以丢弃工作区的修改：  
`$ git checkout -- readme.txt`  
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：  
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；  
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
总之，就是让这个文件回到最近一次git commit或git add时的状态。  

Git同样告诉我们，用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区：  
```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt

```

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  

创建完了，那么我想删除刚刚创建的文件该如何操作呢?    
第一步：首先是从你本地删除，第二步其次是从版本库中删除掉  
```
$ git rm test.txt  
rm 'test.txt'  
$ git commit -m "remove test.txt"  
[master d17efd8] remove test.txt  
 1 file changed, 1 deletion(-)  
 delete mode 100644 test.txt  
 
 ```
 
现在，文件就从版本库中被删除了。  

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：  

`$ git checkout -- test.txt`  

git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。  
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。  

到目前为止，我们已经掌握了如何在Git仓库里对一个文件进行时光穿梭，你再也不用担心文件备份或者丢失的问题了。  
其实一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下。  
实际情况往往是这样，找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。  
在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：  

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：  

`$ ssh-keygen -t rsa -C "youremail@example.com"`  

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。  

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH   Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。  

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：   
为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。  

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。  

准备工作已经做好了，那么如何 让本地的文件同步到github上去呢？ 接下来小编告诉你。  

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：  
在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：  
现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：  
` $ git remote add origin git@github.com:michaelliao/learngit.git `
注意：把上面的michaelliao替换成你自己的GitHub账户名  

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。  
下一步，就可以把本地库的所有内容推送到远程库上：  
```
$ git push -u origin master  
Counting objects: 19, done.  
Delta compression using up to 4 threads.  
Compressing objects: 100% (19/19), done.  
Writing objects: 100% (19/19), 13.73 KiB, done.  
Total 23 (delta 6), reused 0 (delta 0)  
To git@github.com:michaelliao/learngit.git  
 * [new branch]      master -> master  
Branch master set up to track remote branch master from origin.  

```  
把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。  

由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。  

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样  

从现在起，只要本地作了提交，就可以通过命令：  

` $ git push origin master `  

SSH警告  

当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：  

The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.  
RSA key fingerprint is xx.xx.xx.xx.xx.  
Are you sure you want to continue connecting (yes/no)?  

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。  

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：  

Warning: Permanently added 'github.com' (RSA) to the list of known hosts.  

这个警告只会出现一次，后面的操作就不会有任何警告了。  

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。  

如何让github的文件克隆到本地的工作区域中：  
```
$ git clone git@github.com:michaelliao/gitskills.git  
Cloning into 'gitskills'...  
remote: Counting objects: 3, done.  
remote: Total 3 (delta 0), reused 0 (delta 0)  
Receiving objects: 100% (3/3), done.  

$ cd gitskills  
$ ls  
README.md  

```  
在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。  
那么开始创建一个分支  

首先，我们创建dev分支，然后切换到dev分支：  
```
$ git checkout -b dev   
Switched to a new branch 'dev'  

```  
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：  

```
$ git branch dev  
$ git checkout dev  
Switched to branch 'dev'  

```

然后，用git branch命令查看当前分支：  

```
$ git branch  
* dev  
  master  
```  
git branch命令会列出所有分支，当前分支前面会标一个*号。  

然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改，加上一行：  

然后提交：  
```
$ git add readme.txt   
$ git commit -m "branch test"  
[dev fec145a] branch test  
 1 file changed, 1 insertion(+)  
 
 ```

现在，dev分支的工作完成，我们就可以切换回master分支：  

```
$ git checkout master  
Switched to branch 'master'  

```  

切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：  

现在，我们把dev分支的工作成果合并到master分支上：  
```
$ git merge dev  
Updating d17efd8..fec145a  
Fast-forward  
 readme.txt |    1 +  
 1 file changed, 1 insertion(+)  
```  
git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。  

注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。  

当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。  

合并完成后，就可以放心地删除dev分支了：  
```
$ git branch -d dev  
Deleted branch dev (was fec145a).  
```
删除后，查看branch，就只剩下master分支了：  

$ git branch  
* master  

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。  

 Git鼓励大量使用分支：  

查看分支：git branch  

创建分支：git branch <name>  

切换分支：git checkout <name>  

创建+切换分支：git checkout -b <name>  

合并某分支到当前分支：git merge <name>  

删除分支：git branch -d <name>  

有分支就会有冲突  
如果您把分支上的文件修改后，提交到版本库中，切换到主干上，然后修改文件后 也提交，然后合并分支和master上面的 内容，就会发生 冲突我们可以直接查看readme.txt的内容：  
```
Git is a distributed version control system.  
Git is free software distributed under the GPL.  
Git has a mutable index called stage.  
Git tracks changes of files.  
<<<<<<< HEAD  
Creating a new branch is quick & simple.  
=======  
Creating a new branch is quick AND simple.  
>>>>>>> feature1  
```  
Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：  

Creating a new branch is quick and simple.  

再提交：  
```
$ git add readme.txt   
$ git commit -m "conflict fixed"  
[master 59bc1cb] conflict fixed   

```

冲突解决了，可以安心 编写程序了  

还可以用带参数的git log也可以看到分支的合并情况：  
```
$ git log --graph --pretty=oneline --abbrev-commit  
*   59bc1cb conflict fixed  
|\  
| * 75a857c AND simple  
* | 400b400 & simple  
|/  
* fec145a branch test  
...  

最后，删除feature1分支：  

$ git branch -d feature1  
Deleted branch feature1 (was 75a857c).  
```  
注意：通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。  
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。  
准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：  
```
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt |    1 +
 1 file changed, 1 insertion(+)
 ```
 

因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。  

合并后，我们用git log看看分支历史：  
```
$ git log --graph --pretty=oneline --abbrev-commit  
*   7825a50 merge with no-ff  
|\  
| * 6224937 add merge  
|/  
*   59bc1cb conflict fixed  
...  
```  















 


  
  






