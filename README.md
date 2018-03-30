
# Git 学习笔记  

*2018-03-21——2018-03-30  **Rewa Fang** 编辑*

---

## 一. 基本概念 
> 百度百科  
Git(读音为/gɪt/。)是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理。[1]  Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

简单理解Git系统就是用来管理你写项目的每个阶段、每种版本的代码。
>比如你昨天写了一天代码，写JS原生的方式写了一个组件；今天主管告诉你昨天写的方式不用了，写VUE重写一个；OK！你忍着犯罪的冲动，啪啪啪一天写了个VUE的版本。好了，好死不死；临近下班，这货又来告诉你；经过慎重考虑，还是用原生的方式；你把代码恢复一下。－－－!　　

**这种情况你肿么办？**

- 如果你昨天的代码保存过了（一般都会保存），那还好；重新替换一下即可。
- 如果你没保存，那就呵呵了。。。重新写一遍

总之无论哪种情况，你都得重新整理一次代码；代码量少还可以接受这种重复劳动。如果代码量很多呢，且有很个版本呢？是不是都要重新去整理代码？那你的工作效率将大大降低，就算公司不计较，可浪费的都是你的时间啊。。。

Git的诞生就是用来解决类似这样的事情的。管理你项目的所有版本，只要你提交一个版本；系统就会帮你记录并保存，这样你可以轻松的管理你项目的任一版本。一个命令就能退回你想要退回的版本；不需要整理任何代码。

----
### 集中式VS分布式

先说集中式版本控制系统，版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。  

![集中式](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384860735706fd4c70aa2ce24b45a8ade85109b0222b000/0)

集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊。

那分布式版本控制系统与集中式版本控制系统有何不同呢？首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。

和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了。

在实际使用分布式版本控制系统的时候，其实很少在两人之间的电脑上推送版本库的修改，因为可能你们俩不在一个局域网内，两台电脑互相访问不了，也可能今天你的同事病了，他的电脑压根没有开机。因此，分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。  

![分布式](https://cdn.liaoxuefeng.com/cdn/files/attachments/0013848607465969378d7e6d5e6452d8161cf472f835523000/0)

***
## 二. 安装与配置
### 安装方式

- **Windows**  
    在Windows上使用Git，可以从Git官网[直接下载](https://git-scm.com/downloads)安装程序，然后按默认选项安装即可。
- **Linux**  
    没装过 不知道
- **Mac**  
    没装过 不知道

***


### 配置个人信息（用户名+邮箱）

安装成功后，在开始菜单里找到“Git”->“Git Bash”。 就可开始你的Git之旅了。

通过`git config --global` 命令配置用户名和邮箱  
    
    $ git config --global user.name "Rewa Fang"
    $ git config --global user.email "fangrh0627@163.com"

>注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

***
## 三. 基础命令

1. **创建仓库**`--> git init`
   
   以F:盘为根目录 操作所有命令 （windows 7系统下）  
   
   *先创建一个空的目录*  
   
        $ f:    //进入F盘
        $ mkdir git_rewa    //创建一个空的目录 git_rewa  用来当作仓库
        $ cd git_rewa   //进入目录
        $ pwd   //查看当前目录路径
        /f/git_rewa     //我电脑上的目录路径

    *git init 命令设置当前目录为仓库*  
    
        $ git init
        Initialized empty Git repository in /f/git_rewa/.git/

    这样一个空的仓库就创建好了。  
    `.git` 目录是Git自动创建的，用来跟踪管理版本的；不可以删除。

2. **添加文件到仓库**`--> git add`  

        $ git add readme.txt    //把readme.txt 文件添加到仓库
    
    添加只要把文件放到**暂存区**  并没有提交保存到仓库；还需要用命令`git commit` 提交到仓库。
    
3. **提交到仓库**`--> git commit`  
        
        $ git commit -m 'this is test file'
        -m: 参数 后面可以注明提交文件的描述
    >添加文件到Git仓库，分两步：  
    第一步，使用命令`git add <file>`，可反复多次使用，添加多个文件；  
    第二步，使用命令`git commit`，完成。  
    >>添加和修改的步骤是一样的 都需要`git add`之后再`git commit` 每修改一次后都需要`git add` 到暂存区，然后再提交。  
    **第一次修改 -> git add -> 第二次修改 -> git add -> git commit**  
    如果不add到暂存区，那就不会加入到commit中。

        $ git add file1.txt
        $ git add file2.txt file3.txt
        $ git commit -m "add 3 files."
        
4. **查看当前状态**`--> git status`  
        
        $ git status
        On branch master
        nothing to commit, working tree clean

    `git status`命令可以让我们时刻掌握仓库当前的状态;  
    可以知道当前暂存区有哪些文件未提交。
    
5. **查看文件修改内容**`--> git diff xxx.xxx`
    
        $ git diff readme.txt 
        diff --git a/readme.txt b/readme.txt
        index 46d49bf..9247db6 100644
        --- a/readme.txt
        +++ b/readme.txt
        @@ -1,2 +1,2 @@
        -Git is a version control system.
        +Git is a distributed version control system.
         Git is free software.

    这样就能看出本次修改内容，确认无误可提交
6. **查看提交历史记录**`--> git log`  
    
        $ git log
        commit 208995cb2da8575877cef1ef06df47a0cf178cae (HEAD -> master)
        Author: Rewa Fang <fangrh0627@163.com>
        Date:   Tue Mar 6 15:31:52 2018 +0800
        
            20180306 15:31  // -m 参数的描述信息
        
        commit 11d5a84c4c2fc16fefc0051421266fb3f3156d59
        Author: Rewa Fang <fangrh0627@163.com>
        Date:   Tue Mar 6 14:51:09 2018 +0800
        
            Rewa Fang   
        
        commit e94734a4789e07960e8d93b264bfce561a9b6f4c
        Author: Your Name <fangrh0627@163.com>
        Date:   Tue Mar 6 14:47:00 2018 +0800
        
            once again

    `git log`命令显示从最近到最远的提交日志;  
    单行显示加上`--pretty=oneline`参数：
    
        $ git log --pretty=oneline
        208995cb2da8575877cef1ef06df47a0cf178cae (HEAD -> master) 20180306 15:31
        11d5a84c4c2fc16fefc0051421266fb3f3156d59 Rewa Fang
        e94734a4789e07960e8d93b264bfce561a9b6f4c once again
        16e4252f2bb5ab0ff52b28466b7986733d509374 add update
        27da7c4bc08d1450101f7ba82e5842f3ebbfc719 this is a test file readme.txt

    第一列信息是十六进制的`commit id`(版本号)
    第二列信息是提交版本描述  
    <div id="backspace"></div>
7. **版本回退**`--> git reset`  
    
        $ git reset --hard HEAD^ 

    在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，上100个版本可以写成HEAD~100。  
    也就用`commit id`的方式回退版本
        
        $ git reset --hard 208995cb

    版本号不用写全，会自动匹配。

8. **查看命令历史**`--> git reflog`  

    ```
    $ git reflog
    208995c (HEAD -> master) HEAD@{0}: commit: 20180306 15:31
    11d5a84 HEAD@{1}: reset: moving to 11d5a84
    16e4252 HEAD@{2}: reset: moving to HEAD^
    e94734a HEAD@{3}: reset: moving to HEAD^
    11d5a84 HEAD@{4}: reset: moving to 11d5a84
    e94734a HEAD@{5}: reset: moving to HEAD^
    11d5a84 HEAD@{6}: commit: Rewa Fang
    e94734a HEAD@{7}: commit: once again
    16e4252 HEAD@{8}: commit: add update
    27da7c4 HEAD@{9}: commit (initial): this is a test file readme.txt
    ```

    当退回到某个老版本时，`git log` 就不会再记录你退回之前的最新版本了；但仓库里还是存在这个版本的；只不过不显示版本号，你就无法根据版本号退回。这个时候如果你想回到最新版本时，`git reflog` 可以显示之前执行命令时的版本号。  


9. **查看工作区和版本库里面最新版本的区别**`--> git diff HEAD -- readme.txt`  
10. **退回最近一次git commit或git add时的状态**`--> git checkout -- readme.txt`  
11. **撤销暂存区的修改**`--> git reset HEAD readme.txt`  

    >* 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令` git checkout -- file`。  
    >
    >* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。  
    >
    >* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](#backspace)，不过前提是没有推送到远程库。
      
12. **删除文件**`--> git rm readme.txt`  

        $ rm test.txt
    用`rm`命令删除的时候,查看状态时Git会提示工作区与版本库不一致了,因为仅仅是删除了工作区的文件；  
    要从版本库里面删除要用命令`git rm readme.txt` 并且 `git commit`;  

    如果删错了，还没有提交到版本库，可以把误删的文件恢复到最新版本：  

        $ git checkout -- test.txt
    > 但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。  

***
## 四. GitHub 远程仓库  

- 第一步：创建`SSH KEY `   
    在用户主目录下，看看有没有`.ssh`目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建`SSH Key`：  
    ```
    $ ssh-keygen -t rsa -C "youremail@example.com"
    ``` 
- 第二步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：   
    然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容;  

- 第三步：在GitHub上新建一个仓库`git_rewa`。目前，在GitHub上的这个`git_rewa`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。  
现在，我们根据GitHub的提示，在本地的`git_rewa`仓库下运行命令：  

        $ git remote add origin git@github.com:Rewa-Fang/git_rewa.git 
    
    >[命令] git remote add [自定义远程仓库名] git@github.com:[用户名]/[仓库名].git   
        - origin: 为远程仓库在本地定义一个名称  
        - git@github.com: github 远程地址  
        - Rewa Fang:GitHub 上的用户名称  
        - git_rewa: GitHub上的仓库名称  

        $ ssh -T git@github.com  //验证是否成功连接GitHub     
        
    现在已经在本地创建了一个名为`origin`的远程仓库；连接着`Rewa-Fang`的GitHub上`git_rewa`仓库；

- 第四步： 把本地仓库所有内容推送到远程库上  

        $ git push -u origin master
    > [命令]`git push`  
    master: 分支名(主分支)  
    -u : 参数； 第一次推送的时候加，以后不需要加该参数；第一次加上之后会将本地`master`与远程的`master`分支关联起来；用简化命令`git push`可直接提交到`master`分支。  

    ***
    > *在（Create a new repo）创建远程仓库的时候，如果你勾选了`Initialize this repository with a README`（就是创建仓库的时候自动给你创建一个README文件），  那么到了你将本地仓库内容推送到远程仓库（`git push -u origin master`）的时候就会报一个`failed to push some refs to  git@github.com:michaelliao/learngit.git`。 这是由于你新创建的那个仓库里面的README文件不在本地仓库目录中，这时我们可以通过以下命令将内容合并：`$ git pull --rebase origin master`  这时候就不会报错了。*
    ***  
    
    ### 从远程仓库克隆  

        $ git clone git@github.com:Rewa-Fang/git_rewa.git 
    
    >[命令] `git clone`   
        - git@github.com: github 远程地址  
        - Rewa Fang:GitHub 上的用户名称  
        - git_rewa: GitHub上的仓库名称  

    克隆命令会从GitHub上克隆整个仓库文件夹，不仅仅是代码；所以本地不需要创建仓库。
***
## 四. 分支管理  

* **[命令]**  
  >   **查看分支**： `git branch`  
    **创建分支**：`git branch <name>`  
    **切换分支**：`git checkout <name>`  
    **创建+切换分支**：`git checkout -b <name>`  
    **合并某分支到当前分支**：`git merge <name>`    
    **删除分支**：`git branch -d <name>`  
    **查看分支合并图**：`git log --graph`  

    在没有创建分支之前，默认每次提交都是提交到主分支中；即master分支；HEAD指向master, master 指向最新的提交版本；所发HEAD指向的是当前分支最新的版本。  
    比如再创建一个新的分支dev; 并切换到dev分支；那么此时HEAD指向dev最新版本；接下来的每次提交都是提交到dev分支上；并不影响master主分支；  
    dev分支测试完成的代码，就可以合并到master主分支上；这时合并后的master与dev分支就是一样的了。dev分支完成工作任务就可以删除；删除也不会影响master分支。  

* **解决冲突**  
    当两个分支合并时，同一个文件都存在新的修改；会发生冲突：

        Auto-merging readme.txt
        CONFLICT (content): Merge conflict in readme.txt
        Automatic merge failed; fix conflicts and then commit the result.  

    遇到这种情况，就要`手动解决`冲突后再提交。    

* **`Fast forward`模式**  
    通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

    准备合并`dev`分支，请注意`--no-ff`参数，表示禁用`Fast forward`：

        $ git merge --no-ff -m "merge with no-ff" dev
        Merge made by the 'recursive' strategy.
        readme.txt |    1 +
        1 file changed, 1 insertion(+)  

    因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。  
    合并后，我们用git log看看分支历史。会显示分支及本次合并时创建的commit。

* **`Bug`分支**  
    
    项目出现BUG时，需要修复；  
    从master主分支上创建一个分支用来修复BUG后再合并。  
    如果dev分支上有正在进行编码工作，且还不满足提交的条件时；可以先把工作区保存起来，修复BUG后再重新调取出来继续dev分支的工作。  
    
    【**命令**】
     >`git stash`   把当前工作区“储藏”起来，以便让工作区保持干净；  
     `git stash list` 查看已“储藏”的工作区列表；  
     `git stash apply`  恢复工作区  
     `git stash drop`   删除“储藏”列表中的工作区
     `git stash pop`  恢复并删除“储藏”列表中的工作区  
     `git stash apply stash@{0}`  恢复指定列表中的工作区  
    
    *修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；  
    当手头工作没有完成时，先把工作现场`git stash`一下，  
    然后去修复bug，修复后，再`git stash pop`，回到工作现场。*  

    `如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。`  
* **多人协作**  

    【**命令**】 
    >`git remote -v`   查看远程库信息；  
     `git push origin branch-name` 从本地推送分支；  
     `git checkout -b branch-name origin/branch-name`  在本地创建和远程分支对应的分支  
     `git branch --set-upstream branch-name origin/branch-name`   建立本地分支和远程分支的关联  
     `git pull`  从远程抓取分支  

* **标签管理**  
  
    给某一个版本commit打上一个标签；以便回到这个版本。和版本ID一样，每个tag对应着一个版本ID。tag可以自定义命令，比版本ID容易维护。  

    【**命令**】  
    >`git tag <name>`   新建一个标签；    
     `git tag -a <tagname> -m "blablabla..."` 可以指定标签信息；    
     `git tag -s <tagname> -m "blablabla..."` 可以用PGP签名标签；  
     `git tag`   可以查看所有标签  
     `git push origin <tagname>` 推送一个本地标签；  
     `git push origin --tags` 推送全部未推送过的本地标签；  
     `git tag -d <tagname>` 删除一个本地标签；  
     `git push origin :refs/tags/<tagname>` 删除一个远程标签；  

***
## 五. 使用远程仓库（GitHub/码云）  
* GitHub  

    我们一直用GitHub作为免费的远程仓库，如果是个人的开源项目，放到GitHub上是完全没有问题的。其实GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。

    在GitHub出现以前，开源项目开源容易，但让广大人民群众参与进来比较困难，因为要参与，就要提交代码，而给每个想提交代码的群众都开一个账号那是不现实的，因此，群众也仅限于报个bug，即使能改掉bug，也只能把diff文件用邮件发过去，很不方便。

    但是在GitHub上，利用Git极其强大的克隆和分支功能，广大人民群众真正可以第一次自由参与各种开源项目了。

    如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：

        git clone git@github.com:Rewa-Fang/bootstrap.git

    一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。

    Bootstrap的官方仓库twbs/bootstrap、你在GitHub上克隆的仓库my/bootstrap，以及你自己克隆到本地电脑的仓库，他们的关系就像下图显示的那样：

    ![关系图](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384926554932eb5e65df912341c1a48045bc274ba4bf000/0)

    如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。

    如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。  
  
* 码云   

    **[参考廖雪峰Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00150154460073692d151e784de4d718c67ce836f72c7c4000)**  

***
## 六. 自定义Git配置  
* 忽略特殊文件  
    项目中总会有一些你不想提交的文件，又想放在本地项目目录下；可以用  `.gitignore`配置文件，把想要忽略的文件名写入该文件中。Git就会自动忽略这些文件。 
    Git也提供一些现成的配置文件，参考：https://github.com/github/gitignore  

    如果你确实想添加一个包含配置文件中的文件，可以用-f强制添加到Git：

        $ git add -f App.class  

    或者你发现，可能是.gitignore写得有问题，需要找出来到底哪个规则写错了，可以用git check-ignore命令检查：

        $ git check-ignore -v App.class
        .gitignore:3:*.class    App.class
    Git会告诉我们，.gitignore的第3行规则忽略了该文件，于是我们就可以知道应该修订哪个规则。  

* 配置命令简写  

    我们只需要敲一行命令，告诉Git，以后st就表示status：

        $ git config --global alias.st status  
    
    用co表示checkout，ci表示commit，br表示branch：

        $ git config --global alias.co checkout
        $ git config --global alias.ci commit
        $ git config --global alias.br branch  

    > --global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。


***
## 七. 搭建Git服务器   (Centos为例)  

* 安装git  

        $ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel //不知道啥意思
        $ yum install git

    接下来我们 创建一个git用户组和用户，用来运行git服务：

        $ groupadd git
        $ useradd git -g git

* 创建证书登录  

    收集所有需要登录的用户的公钥，公钥位于id_rsa.pub文件中，把我们的公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

    如果没有该文件创建它：  

        $ cd /home/git/
        $ mkdir .ssh
        $ chmod 755 .ssh
        $ touch .ssh/authorized_keys
        $ chmod 644 .ssh/authorized_keys  
    
* 初始化Git仓库  （以A2server为例）  
    首先我们选定一个目录作为Git仓库，假定是/home/gitserver/test.git，  
    在/home/gitserver

        $ cd /home
        $ mkdir gitserver
        $ chown git:git gitserver/
        $ cd gitserver

        $ git init --bare test.git
        Initialized empty Git repository in /home/gitserver/test.git/  

    以上命令Git创建一个空仓库，服务器上的Git仓库通常都以.git结尾。然后，把仓库所属用户改为git：

        $ chown -R git:git test.git  

* 从本地克隆仓库  

        $ git clone git@139.196.49.141:/home/gitserver/test.git
        Cloning into 'test'...
        warning: You appear to have cloned an empty repository.
        Checking connectivity... done..

    
    139.196.49.141 为 Git 所在服务器 ip ，你需要将其修改为你自己的 Git 服务 ip。

    这样我们的 Git 服务器安装就完成。