<html lang="en"><head>
    <meta charset="UTF-8">
</head>
<body marginheight="0">
<h1><center>Git操作</center></h1>
<p>在Windows上安装Git：
从<code>http://msysgit.github.io/</code>下载msysgit。msysgit是Windows版的Git，然后按默认选项安装即可。
安装完成后，在开始菜单里找到“Git”-&gt;“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

</p>
<h2>第一部分：在Git仓库里管理文件历史</h2>
<h4>1. 配置git客户端</h4>
<p>代码：
</p>
<pre><code>$ git config --global user.name "yourName"
$ git config --global user.email "youremail@example"</code></pre>
<p>备注：git config命令的--global参数 表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。 

</p>
<h4>2. 创建本地Git库</h4>
<p>2.1 首先，选择一个合适的地方，创建一个空目录：

</p>
<p>代码：
</p>
<pre><code>$ mkdir D:\workspace
$ cd D:\workspace
$ pwd</code></pre>
<p>备注：mkdir命令用于创建目录；cd命令用于进入目录；pwd命令用于显示当前目录。
如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。

</p>
<p>2.2 初始化一个Git仓库

</p>
<p>其次，把这个目录变成Git可以管理的仓库：
代码：
</p>
<pre><code>$ git init</code></pre>
<p>备注：瞬间Git就把仓库建好了，并生成一个默认隐藏的.git目录。
.git的目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。
如需显示.git目录，请输入命令：
</p>
<pre><code>$ git ls -ah</code></pre>
<h4>3 将文件添加到本地Git库</h4>
<p>3.1 首先编写一个文本文件 readme.txt，然后将其保存到先前创建的目录下。

</p>
<p>备注：编写的所有文本文件一定要放到先前创建的目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。
所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等。
而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，
也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。
Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的。
因为文本是有编码的，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。
千万不要使用Windows自带的记事本编辑任何文本文件。建议你下载Notepad++代替记事本,记得把Notepad++的默认编码设置为UTF-8 without BOM即可。

</p>
<p>3.2 将文件修改添加到Git库暂存区：

</p>
<p>代码：
</p>
<pre><code>$ git add readme.txt</code></pre>
<p>备注：执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。该命令可反复多次使用，git add 后面可以接多个文件名。

</p>
<p>重点：将工作区中的所有修改一次性地提交到暂存区：
代码：
</p>
<pre><code>$ git add *</code></pre>
<p>3.3 将暂存区的所有内容提交到当前分支上：

</p>
<p>代码：
</p>
<pre><code>$ git commit -m "wrote a readme file"</code></pre>
<p>备注：-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。


</p>
<h4>4. 查看Git库当前的状态：</h4>
<p>代码：
</p>
<pre><code>$ git status</code></pre>
<p>备注：如果对文件的所有改动都成功提交到Git仓库了，那么Git会告诉我们当前没有需要提交的修改，而且，工作目录是干净（working directory clean）的。

</p>
<h4>5. 查看修改，然后把修改提交到Git版本库</h4>
<p>5.1 查看修改内容：

</p>
<p>代码：
</p>
<pre><code>$ git diff readme.txt</code></pre>
<p>备注：git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式。知道了对readme.txt作了什么修改后，再把它提交到仓库就放心多了。

</p>
<p>5.2 提交修改的内容

</p>
<p>代码：
</p>
<pre><code>$ git add readme.txt
$ git commit -m "add item 4.5.6"</code></pre>
<p>备注：提交修改和提交新文件的操作是一样的。


</p>
<h4>6. 版本的后退与前进</h4>
<p>6.1 版本的概念：

</p>
<p>你不断对文件进行修改，然后不断提交修改到版本库里，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。
一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

</p>
<p>6.2 查看版本提交历史：

</p>
<p>代码：
</p>
<pre><code>$ git log  //查看详情
$ git log --pretty=oneline //将一条历史记录显示在一行</code></pre>
<p>备注：git log命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以加上--pretty=oneline参数。

</p>
<p>6.3 版本号：

</p>
<p>大串类似3628164...882e1e0的是commit id（版本号），是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，
以你自己的为准。

</p>
<p>6.4 返回到最新提交的版本

</p>
<p>代码：
</p>
<pre><code>$ git reset --hard HEAD</code></pre>
<p>备注：所有未被添加到暂存区的文件修改都会丢失的。

</p>
<p>6.5 版本回退：

</p>
<p>首先找到需要回退到的版本号，然后回退到指定版本
代码：
</p>
<pre><code>$ git log --pretty=oneline        //查看版本号
$ git reset --hard commit_id     //回退到指定版本
$ git reset --hard HEAD^        //回退到上一个版本</code></pre>
<p>备注：Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^。

</p>
<p>当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

</p>
<p>6.6 查看文本内容：

</p>
<p>代码：
</p>
<pre><code>$ cat readme.txt</code></pre>
<p>6.7 查看命名提交记录

</p>
<p>代码：
</p>
<pre><code>$ git reflog</code></pre>
<p>6.8 版本前进：

</p>
<p>首先找到要前进到的版本号，然后前进到指定版本
</p>
<pre><code>$ git reflog 
$ git reset --hard commit_id</code></pre>
<p>备注：Git提供git reflog用来记录你的每一次命令。


</p>
<h4>7.工作区和暂存区</h4>
<p>工作区：就是你在电脑里能看到的目录。
版本库：工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，
以及指向master的一个指针叫HEAD。
需要提交的文件修改通过
</p>
<pre><code>$ git add &lt;file&gt; 命令通通放到暂存区，然后，通过
$ git commit -m "somemessage" 命令一次性提交暂存区的所有修改到当前分支。</code></pre>
<p>一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的。

</p>
<h4>8.管理修改</h4>
<p>Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。
什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，
甚至创建一个新文件，也算一个修改。每次修改，如果不add到暂存区，那就不会被commit提交到分支上。每次修改后可以先add 最后在一次性commit 提交。

</p>
<p>8.1 查看工作区和版本库里面最新版本的区别

</p>
<pre><code>$ git diff HEAD -- readme.txt</code></pre>
<h4>9.撤销修改</h4>
<p>9.1 丢弃工作区的修改，用命令git checkout -- file。

</p>
<p>代码：
</p>
<pre><code>$ git checkout -- readme.txt</code></pre>
<p>备注：命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。
git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。

</p>
<p>9.2 丢弃已添加到暂存区的修改，分两步：

</p>
<p>第一步 用命令git reset HEAD file把暂存区的修改撤销掉（unstage），重新放回工作区。第二步丢弃工作区的修改。
代码：
</p>
<pre><code>$ git reset HEAD readme.txt
$ git checkout -- readme.txt</code></pre>
<p>备注：git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。执行此命令后，暂存区是干净的，工作区有修改。

</p>
<p>9.3 撤销提交，参考版本回退一节，不过前提是没有推送到远程库。

</p>
<p>代码：
</p>
<pre><code>$ git reset --hard HEAD^</code></pre>
<p>备注：一旦你把“stupid boss”提交推送到远程版本库，你就真的惨了……


</p>
<h4>10. 删除文件</h4>
<p>在Git中，删除也是一个修改操作：要删除的文件不论其存放位置是在工作区、暂存区、还是版本库，要删除该文件第一个命令必须是 rm 命令。
注意：
</p>
<pre><code>$ rm &lt;file&gt; 命令删除工作区的文件，是对工作区的修改。</code></pre>
<p>10.1 要删除的文件目前还在工作区：

</p>
<p>要彻底删除该文件，直接在文件管理器中把该文件删了，或者用rm命令删除。
代码：
</p>
<pre><code>$ rm test.txt</code></pre>
<p>备注：该条命令执行后，就OK了。

</p>
<p>10.2 要删除的文件目前还在暂存区：

</p>
<p>要彻底删除该文件分为两步：第一步 rm <file>命令 第二步 git rm <file> 命令。
代码：
</file></file></p>
<pre><code>$ rm test.txt
$ git rm test.txt</code></pre>
<p>备注：执行完第一条命令时，如果想撤销删除操作，可以使用 git checkout -- test.txt命令撤销rm <file>命令。如果执行了 git rm命令，那么删除不能被撤销。

</file></p>
<p>10.3 要删除的文件目前已被提交到了版本库。

</p>
<p>删除文件分为三步：
第一步 rm <file> 命令 
第二步 git rm <file> 命令 
第三步 git commit 命令

</file></file></p>
<p>代码：
</p>
<pre><code>$ rm test.txt
$ git rm test.txt
$ git commit -m "remove test.txt</code></pre>
<p>备注：当执行完第一条命令时，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了。
执行完第一步，现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit；
另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
代码：
</p>
<pre><code>$ git checkout -- test.txt    //撤销对工作区文件的删除操作</code></pre>
<p>备注：git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
如果执行了 git rm命令，那么删除不能被撤销。
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，
你会丢失最近一次提交后你修改的内容。


</p>
<h2>第二部分：远程仓库</h2>
<h4>11.远程仓库</h4>
<p>问题1：Git是分布式版本控制系统，那么同一个Git仓库，如何分布到不同的机器上呢？

</p>
<p>方法1：自己搭建一台运行Git的服务器。找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，
并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

</p>
<p>方法2：从Github网站上免费获得Git远程仓库。

</p>
<p>问题2：获取Git远程仓库的步骤有哪些？

</p>
<p>第一步 登陆Github网站，注册一个GitHub账号。

</p>
<p>第二步 创建SSH Key
在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，
可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash）。
创建SSH Key：
代码：
</p>
<pre><code>$ ssh-keygen -t rsa -C "youremail@example.com"</code></pre>
<p>备注：把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可。

</p>
<p>第三步 找到SSH Key密匙 
在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，
id_rsa.pub是公钥，可以放心地告诉任何人。

</p>
<p>第四步 添加SSH Key密匙
登陆GitHub，打开“Account settings”，“SSH Keys”页面；然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容；
点“Add Key”，你就应该看到已经添加的Key

</p>
<p>问题3：为什么GitHub需要SSH Key呢？
因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，
就可以在每台电脑上往GitHub推送了。

</p>
<p>备注：在GitHub上免费托管的Git仓库，任何人都可以看到，所以，不要把敏感信息放进去。如果你不想让别人看到Git库，有两个办法，一个是交点保护费，
让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，
所以别人也是看不见的。


</p>
<h4>12. 添加远程仓库</h4>
<p>你现在已经在本地创建了一个Git仓库，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，
又可以让其他人通过该仓库来协作。

</p>
<p>12.1 添加远程仓库的步骤：

</p>
<p>第一步：登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库。在Repository name填入本地已初始化的Git库名，其他保持默认设置，
点击“Create repository”按钮，就成功地创建了一个新的Git仓库。

</p>
<p>第二步：把一个已有的本地仓库与之关联。
根据GitHub的提示，在本地的仓库下运行命令：
代码：
</p>
<pre><code>$ git remote add origin git@github.com:个人的Git账户名/本地仓库名.git</code></pre>
<p>备注：添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

</p>
<p>第三步：把本地库的所有内容推送到远程库上
代码：
</p>
<pre><code>$ git push -u origin master</code></pre>
<p>备注：把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，
加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，
在以后的推送或者拉取时就可以简化命令。
推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样。

</p>
<p>从现在起，只要本地作了提交，就可以通过命令：
</p>
<pre><code>$ git push origin master</code></pre>
<p>把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

</p>
<p>备注：分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，当有网络的时候，
再把本地提交推送一下就完成了同步！



</p>
<h4>13. 从远程库克隆</h4>
<p>假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

</p>
<p>第一步：登陆GitHub，创建一个新的仓库，名字叫gitskills，勾选Initialize this repository with a README，
这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件。

</p>
<p>第二步：打开Git Bash，使用cd 命令 切换到你想要进的目录：
代码：
</p>
<pre><code>$ cd d:\</code></pre>
<p>第三步：使用git clone命令，将远程库克隆到本地D盘下。
代码：
</p>
<pre><code>$ git clone git@github.com:个人的Git账户名/gitskills.git
$ cd gitskills
$ ls</code></pre>
<p>备注：如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。
你也许还注意到，GitHub给出的地址不止一个，还可以用<code>https://github.com/michaelliao/gitskills.git</code>这样的地址。实际上，Git支持多种协议，
默认的git://使用ssh，但也可以使用https等其他协议。
使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。


</p>
<h4>14.分支管理</h4>
<p>14.1 什么是分支

</p>
<p>分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。
如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了Git又学会了SVN！

</p>
<p>14.2 分支有什么作用

</p>
<p>假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。
如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。
现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，
直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

</p>
<p>14.3 Git分支的特点

</p>
<p>Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成！无论你的版本库是1个文件还是1万个文件。


</p>
<h4>15.创建与合并分支</h4>
<p>15.1 创建分支

</p>
<p>代码：
</p>
<pre><code>$ git branch dev //创建dev分支
$ git checkout dev //切换到dev分支
$ git checkout -b dev //创建并切换到dev分支</code></pre>
<p>15.2 查看当前分支

</p>
<p>代码：
</p>
<pre><code>$ git branch</code></pre>
<p>15.3 操作当前分支

</p>
<p>代码：
</p>
<pre><code>$ git add readme.txt
$ git commit -m "add some new info"</code></pre>
<p>15.4 切换回master分支

</p>
<p>代码：
</p>
<pre><code>$ git checkout master</code></pre>
<p>15.5 合并分支 

</p>
<p>代码：
</p>
<pre><code>$ git merge dev</code></pre>
<p>15.6 删除分支

</p>
<p>代码：
</p>
<pre><code>$ git branch -d dev</code></pre>
<h4>16. 解决冲突</h4>
<p>16.1 冲突产生的原因:

</p>
<p> 不同分支提交的对同一文件的修改交叉了。也就是对同一文件的同一部分不同分支提交的修改发生了重叠，产生了冲突。
遇到这种情况必须手动解除冲突：Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突。

</p>
<p>解决步骤：

</p>
<p>首先 使用 git status查看冲突的文件
代码：
</p>
<pre><code>$ git status</code></pre>
<p>其次 打开工作区中发生冲突的文件。
Git用&lt;&lt;&lt;&lt;&lt;&lt;&lt;，=======，&gt;&gt;&gt;&gt;&gt;&gt;&gt;标记出不同分支的内容，我们需要在文件中进行手动修改后保存，再提交。
代码：
</p>
<pre><code>$ git add readme.txt
$ git commit -m "conflict fixed"</code></pre>
<p>16.2 查看分支的合并情况

</p>
<pre><code>$ git log --graph --pretty=oneline --abbrev-commit</code></pre>
<p>16.3 最后删除分支

</p>
<p>代码：
</p>
<pre><code>$ git branch -d dev</code></pre>
<h4>17. 分支管理策略</h4>
<p>通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
为了保存分支信息，需要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

</p>
<p>17.1 使用--no-ff方式的git merge：

</p>
<p>第一步：新建并切换到dev分支
代码：
</p>
<pre><code>$ git checkout -b dev</code></pre>
<p>第二步：修改readme.txt文件，并提交一个新的commit

</p>
<p>第三步：切换到master分支
</p>
<pre><code>$ git checkout master</code></pre>
<p>第四步：合并dev分支，请注意--no-ff参数，表示禁用Fast forward
</p>
<pre><code>$ git merge --no-ff -m "merge with no-ff" dev</code></pre>
<p>因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

</p>
<p>第五步：查看分支历史
</p>
<pre><code>$ git log --graph --pretty=oneline abbrev-commit</code></pre>
<p>17.2 分支策略

</p>
<p>在实际开发中，我们应该按照几个基本原则进行分支管理：

</p>
<p>首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

</p>
<p>那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

</p>
<p>你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

</p>
<p>合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。


</p>
<h4>18. bug分支管理</h4>
<p>每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。
当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交，
并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？
幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。

</p>
<p>具体操作步骤：
第一步：把当前工作现场“储藏”起来，等以后恢复现场后继续工作
</p>
<pre><code>$ git stash</code></pre>
<p>第二步：使用git status查看工作区 如果是干净的就可以放心地创建分支来修复bug
</p>
<pre><code>$ git status</code></pre>
<p>第三步：确定在那个分支上修复bug
假定需要在master分支上修复，就从master创建临时分支。
</p>
<pre><code>$ git checkout master
$ git checkout -b issue-101</code></pre>
<p>第四步：修复bug然后提交
</p>
<pre><code>$ git add readme.txt
$ git commit -m "fix bug 101"</code></pre>
<p>第五步：合并临时分支
</p>
<pre><code>$ git checkout master
$ git merge --no-ff -m "merged fix bug 101" issue-101</code></pre>
<p>第六步：删除临时分支
</p>
<pre><code>$ git branch -d issue-101</code></pre>
<p>工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
另一种方式是用git stash pop，恢复的同时把stash内容也删了；

</p>
<p>第七步：回到之前的分支，恢复储藏的工作区
</p>
<pre><code>$ git checkout dev
$ git stash list   //查看储藏
$ git stash apply stash@{0} //</code></pre>
<p>可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令。


</p>
<h4>19.feature分支管理</h4>
<p>软件开发中，总有无穷无尽的新的功能要不断添加进来。
添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，
完成后，合并，最后，删除该feature分支。

</p>
<p>开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

</name></p>
<p>代码：
</p>
<pre><code>$ git checkout -b feature-vulcan
$ git add vulcan.js
$ git commit -m "add vulcan.js"
$ git checkout dev
$ git branch -d feature-vulcan</code></pre>
<p>销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令git branch -D feature-vulcan。
</p>
<pre><code>$ git branch -D feature-vulcan</code></pre>
<h4>20. 多人协作（难点）</h4>
<p>当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。
要查看远程库的信息，用git remote，或者，用git remote -v显示更详细的信息。

</p>
<p>代码：
</p>
<pre><code>$ git remote -v</code></pre>
<p>命令输出后，显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。

</p>
<p>20.1 推送分支：

</p>
<p>推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上。
如果要推送其他分支，比如dev 直接改一下代码中的分支名就可以了。

</p>
<p>代码：
</p>
<pre><code>$ git push origin master</code></pre>
<p>但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
    master分支是主分支，因此要时刻与远程同步；
    dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
    bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
    feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

</p>
<p>20.2 抓取分支：

</p>
<p>多人协作时，大家都会往master和dev分支上推送各自的修改。
当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。因为本地新建的分支如果不推送到远程，对其他人就是不可见的；
现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支。
注意：本地必须已经创建dev分支，并且已将dev分支推送到了远程库，如果没有推送，那么远程库就不包含dev分支，克隆远程库的人执行下面的代码会出错。

</p>
<p>代码：
</p>
<pre><code>$ git checkout -b origin/dev</code></pre>
<p>现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：

</p>
<p>代码：
</p>
<pre><code>$ git add readme.txt
$ git commit -m "add d/gitskills/workspace/readme.txt"
$ git push origin dev</code></pre>
<p>你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你在自己的工作区也对同样的文件作了修改，并试图推送。
</p>
<pre><code>$ git add readme.txt 
$ git commit -m "d盘 add sometext in readme.txt"
$ git push origin dev</code></pre>
<p>推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，
然后，在本地合并，解决冲突，再推送。
</p>
<pre><code>$ git pull</code></pre>
<p>git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：再pull：
</p>
<pre><code>$ git branch --set-upstream dev origin/dev
$ git pull</code></pre>
<p>这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：
</p>
<pre><code>$ git status</code></pre>
<p>打开工作区中的文件，手动修改冲突
</p>
<pre><code>$ git add readme.txt
$ git commit -"fixed conflict in readme.txt"
$ git push origin dev</code></pre>
<p>因此，多人协作的工作模式通常是这样：
    首先，可以试图用git push origin branch-name推送自己的修改；
    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    如果合并有冲突，则解决冲突，并在本地提交；
    没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。
这就是多人协作的工作模式，一旦熟悉了，就非常简单。


</p>
<h4>21. 标签管理</h4>
<p>发布一个版本时，我们通常先在版本库中打一个标签，这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，
就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

</p>
<p>Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），
所以，创建和删除标签都是瞬间完成的。

</p>
<p>21.1 创建标签

</p>
<p>在Git中打标签非常简单，首先，切换到需要打标签的分支上：然后，敲命令git tag <name>就可以打一个新标签：可以用命令git tag查看所有标签：
</name></p>
<pre><code>$ git checkout master
$ git tag v1.0
$ git tag</code></pre>
<p>默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？
方法是找到历史提交的commit id，然后打上就可以了
</p>
<pre><code>$ git reflog --pretty=oneline abbrev-commit</code></pre>
<p>比方说要对add merge这次提交打标签，它对应的commit id是6224937，敲入命令：
</p>
<pre><code>$ git tag v0.9 6224937
$ git tag</code></pre>
<p>注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：
</tagname></p>
<pre><code>$ git show v1.0</code></pre>
<p>还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字
</p>
<pre><code>$ git tag -a v1.1 -m "version 0.1 released" 3628164</code></pre>
<p>用命令git show <tagname>可以看到说明文字：
</tagname></p>
<pre><code>$ git tag show v1.1</code></pre>
<p>还可以通过-s用私钥签名一个标签：
</p>
<pre><code>$ git tag -s v1.2 -m "signed version 0.2 released" fec145a</code></pre>
<p>签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错：如果报错，请参考GnuPG帮助文档配置Key。

</p>
<p>用命令git show <tagname>可以看到PGP签名信息：
</tagname></p>
<pre><code>$ git show v1.2</code></pre>
<p>用PGP签名的标签是不可伪造的，因为可以验证PGP签名。验证签名的方法比较复杂，这里就不介绍了。

</p>
<p>21.2 操作标签

</p>
<p>如果标签打错了，也可以删除：
</p>
<pre><code>$ git tag -d v1.0</code></pre>
<p>因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
如果要推送某个标签到远程，使用命令git push origin <tagname>：
</tagname></p>
<pre><code>$ git push origin v1.2</code></pre>
<p>或者，一次性推送全部尚未推送到远程的本地标签：
</p>
<pre><code>$ git push origin --tags</code></pre>
<p>如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
</p>
<pre><code>$ git tag -d v1.3</code></pre>
<p>然后，从远程删除。删除命令也是push，但是格式如下：
</p>
<pre><code>$ git push origin :refs/tags/v1.3</code></pre>
<p>要看看是否真的从远程库删除了标签，可以登陆GitHub查看。


</p>
<h4>22. 使用GitHub</h4>
<p>我们一直用GitHub作为免费的远程仓库，如果是个人的开源项目，放到GitHub上是完全没有问题的。其实GitHub还是一个开源协作社区，通过GitHub，
既可以让别人参与你的开源项目，也可以参与别人的开源项目。

</p>
<p>如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页<a href="https://github.com/twbs/bootstrap，">https://github.com/twbs/bootstrap，</a>
点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：一定要从自己的账号下clone仓库，这样你才能推送修改。
如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。
</p>
<pre><code>$ git clone SSH</code></pre>
<p>如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。
如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。


</p>
<h4>23. 自定义git</h4>
<p>23.1 让Git显示颜色

</p>
<p>在安装Git一节中，我们已经配置了user.name和user.email，实际上，Git还有很多可配置项。
比如，让Git显示颜色，会让命令输出看起来更醒目：
</p>
<pre><code>$ git config --global color.ui true</code></pre>
<p>这样，Git会适当地显示不同的颜色，比如git status命令：文件名就会标上颜色。
我们在后面还会介绍如何更好地配置Git，以便让你的工作更高效。

</p>
<p>23.2 忽略特殊文件(重点)

</p>
<p>实际项目中，很多文件都是不需要版本管理的，比如Python的.pyc文件和一些包含密码的配置文件等等。但这些文件又必须存放于Git工作目录中，这就造成了每次git status都会显示Untracked files ...。

</p>
<p>为了解决这个问题，在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。这个文件的作用就是告诉Git哪些文件不需要添加到版本管理中。一般来说每个Git项目中都需要一个“.gitignore”文件。

</p>
<p>你不需要从头写<code>.gitignore</code>文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：
<a href="https://github.com/github/gitignore">https://github.com/github/gitignore</a>

</p>
<p>忽略文件的原则是：
    （1）忽略操作系统自动生成的文件，比如缩略图等；
    （2）忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的
    .class文件；
    （3）忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。


</p>
<p>23.2.1 配置需要忽略的文件

</p>
<p>假设你在Windows下进行Python开发，Windows会自动在有图片的目录下生成隐藏的缩略图文件，如果有自定义目录，目录下就会有Desktop.ini文件，
因此你需要忽略Windows自动生成的垃圾文件：
然后，继续忽略Python编译产生的.pyc、.pyo、dist等文件或目录：
加上你自己定义的文件，最终得到一个完整的.gitignore文件，内容如下：

</p>
<pre><code>#### Windows:
Thumbs.db
ehthumbs.db
Desktop.ini

#### Python:
*.py[cod]
*.so
*.egg
*.egg-info
dist 
build

#### My configurations:
db.ini
deploy_key_rsa</code></pre>
<p>被过滤掉的文件就不会出现在你的GitHub库中了，当然本地库中还有，只是push的时候不会上传。

</p>
<p>最后一步就是把.gitignore也提交到Git，就完成了！当然检验.gitignore的标准是git status命令是不是说working directory clean。


</p>
<p>23.2.2 配置需要不能忽略的文件

</p>
<p>需要注意的是，gitignore还可以指定要将哪些文件添加到版本管理中：

</p>
<pre><code>!*.zip
!/mtk/one.txt</code></pre>
<p>唯一的区别就是规则开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中。

</p>
<p>为什么要有两种规则呢？想象一个场景：我们只需要管理/mtk/目录中的one.txt文件，这个目录中的其他文件都不需要管理。那么我们就需要使用：

</p>
<pre><code>/mtk/
!/mtk/one.txt</code></pre>
<p>假设我们只有过滤规则没有添加规则，那么我们就需要把/mtk/目录下除了one.txt以外的所有文件都写出来！

</p>
<p>最后需要强调的一点是，如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。

</p>
<p>简单来说，出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。

</p>
<p>所以大家一定要养成在项目开始就创建.gitignore文件的习惯，否则一旦push，处理起来会非常麻烦。

</p>
<p>使用Windows的童鞋注意了，如果你在资源管理器里新建一个.gitignore文件，它会非常弱智地提示你必须输入文件名，但是在文本编辑器里“保存”或者
“另存为”就可以把文件保存为.gitignore了。


</p>

<h4>24 配置别名</h4>

<p>为部分命令配置别名，操作时直接使用别名。

</p>
<p>敲一行命令，告诉Git，以后st就表示status：
</p>
<pre><code>$ git config --global alias.st status</code></pre>
<p>用co表示checkout，ci表示commit，br表示branch
</p>
<pre><code>$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch</code></pre>
<p>--global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

</p>
<p>命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区。既然是一个unstage操作，就可以配置一个unstage别名：
</p>
<pre><code>$ git config --global alias.unstage 'reset HEAD'</code></pre>
<p>配置一个git last，让其显示最后一次提交信息：
</p>
<pre><code>$ git config --global alias.last 'log -1'</code></pre>
<p>甚至还有人丧心病狂地把lg配置成了：
</p>
<pre><code>$ git config --global alias.lg "log --color --graph 
--pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)&lt;%an&gt;%Creset' --abbrev-commit"</code></pre>
<p>24.1 通过修改配置文件修改别名

</p>
<p>配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

</p>
<p>24.1.1 当前仓库的Git配置文件

</p>
<p>每个仓库的Git配置文件都放在.git/config文件中：
</p>
<pre><code>$ cat .git/config</code></pre>
<p>别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

</p>
<pre><code>[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1</code></pre>
<p>24.1.2 当前用户的Git配置文件

</p>
<p>当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：
</p>
<pre><code>$ cat .gitconfig</code></pre>
<p>别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。

</p>
<pre><code>[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com</code></pre>
<p>配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。


</p>
<p>Edit By <a href="http://mahua.jser.me">MaHua</a></p>
</body></html>