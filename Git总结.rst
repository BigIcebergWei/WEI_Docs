.. _header-n0:

Git总结
=======

.. contents::
资料：https://www.runoob.com/git/git-tutorial.html

`张果\_博客园\_一小时学会Git <https://www.cnblogs.com/best/p/7474442.html#_label0>`__

https://git-scm.com/

.. _header-n8:

一、Git 简介
------------

.. _header-n9:

1、简介
~~~~~~~

**优点：**

-  适合分布式开发，强调个体。

-  公共服务器压力和数据量都不会太大。

-  速度快、灵活。

-  任意两个开发者之间可以很容易的解决冲突。

-  离线工作。

**缺点：**

-  模式上比SVN更加复杂。

-  不符合常规思维。

-  代码保密性差，一旦开发者把整个库克隆下来就可以完全公开所有代码和版本信息。

.. _header-n31:

2、Git 常用术语
~~~~~~~~~~~~~~~

-  **仓库（Repository）**

受版本控制的所有文件修订历史的共享数据库。

可以简单理解成一个目录，这个目录里面的所有文件都可以被 Git
管理起来，每个文件的修改、删除，Git
都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

-  **工作区（WorkSpace)**

当前正在编辑的版本的文件目录。

-  **工作树（Working tree）**

用来表示工作区的文件的修改情况。

-  **暂存区/索引（Staging area/Index）**

暂存区也叫，在提交更改（commit）前可以暂存工作区的变化。

-  **提交（Commit）**

对各自文件的工作副本做了更改，并将这些更改提交到仓库

--------------

-  **分支（Branch）**

从主线上分离开的副本，默认分支叫master

-  **合并（Merge）**

将某分支上的更改联接到此主干或同为主干的另一个分支

-  **头（HEAD）**

头是一个象征性的参考，最常用以指向当前选择的分支。

--------------

-  **签入（Checkin）**

将新版本复制回仓库。

-  **签出（Checkout）**

从仓库中将文件的最新修订版本复制到工作空间。

--------------

-  **冲突（Conflict）**

多人对同一文件的工作副本进行更改，并将这些更改提交到仓库

--------------

-  **锁（Lock）**

获得修改文件的专有权限。

-  **修订（Revision）**

表示代码的一个版本状态。Git通过用SHA1 hash算法表示的ID来标识不同的版本。

-  **标记（Tags）**

标记指的是某个分支某个特定时间点的状态。通过标记，可以很方便的切换到标记时的状态。

.. _header-n95:

二、Git 理论基础
----------------

.. _header-n96:

1、工作区域
~~~~~~~~~~~

|image1|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：Git 工作区域</center></body></html>

工作区、暂存区、历史仓库区、远程仓库

**工作区**\ ：当前的工作目录，修改、查看文件。

**暂存区**\ ：由工作区添加，可保存一些临时的更改。

**历史仓库区**\ ：存放所有提交的版本的信息。Head
指针指向最近一次提交的版本。

**远程仓库**\ ：远程仓库，托管代码的服务器，保存完整的仓库。

.. _header-n105:

2、工作流程
~~~~~~~~~~~

Git 的工作流程一般是这样的：

1. 在工作目录中添加、修改文件；

2. 将需要进行版本管理的文件放入暂存区域；

3. 将暂存区域的文件提交到 Git 仓库；

4. 工作完毕后将本地仓库 Push 到远程仓库。

因此，Git
管理的文件有三种状态：已修改(modified)，已暂存(staged)，已提交(committed)。

.. _header-n119:

三、Git 使用
------------

.. _header-n120:

1、下载与安装
~~~~~~~~~~~~~

**下载**

Git
官网下载过慢，可以用国内镜像网站：\ `Git镜像 <https://npm.taobao.org/mirrors/git-for-windows/>`__\ 。

Git 各版本之间有可能有冲突，注意版本问题。

**安装**

没有特殊需求的话默认安装即可。

.. _header-n126:

软件使用
^^^^^^^^

下载的软件里有三款：Git Bash、Git CMD、Git GUI

分别对应不同的操作方式，Bash 是基于 Linux 命令行的，CMD 则是
Windows，GUI 是图形界面操作。

优先使用 Bash，熟练一点之后使用 GUI 会更方便一些。

.. _header-n131:

2、Git 配置
~~~~~~~~~~~

``git config``

.. _header-n133:

（1）查看配置
^^^^^^^^^^^^^

Git 的配置有三种级别：system、global、local。

.. code:: shell

   #完整查看配置信息
   git config -l
   #查看 Git 的环境详细配置

   ##分级别查看
   git config --system --list
   #system config
   #系统所有用户的的配置信息

   git config --global  --list
   #global config
   #当前用户的配置信息

   git config --local  --list
   #local config
   #当前仓库的配置信息

.. _header-n136:

（2）Git 配置文件
^^^^^^^^^^^^^^^^^

在Windows系统中，Git在$HOME目录中查找 .gitconfig 文件（一般位于
C:\Documents and Settings$USER下）

1. /etc/gitconfig：包含了适用于系统所有用户和所有项目的值。(C:\Program
   Files\Git\mingw64\etc\gitconfig)

2. ~/.gitconfig：只适用于当前登录用户的配置。(C:\Users\Administrator.gitconfig)

3. 位于 Git 项目目录中的 .git/config：适用于特定git项目的配置。

.. _header-n145:

（3）用户名与邮箱
^^^^^^^^^^^^^^^^^

安装 Git 后首先要做的事情是设置你的用户名称和 e-mail 地址。

这是非常重要的，因为每次提交 Git 都会使用该信息。

.. code:: shell

   git config --global user.name "BigIceberg"  			#名称
   git config --global user.email 357230620@qq.com   		#邮箱

.. _header-n149:

（4）添加或删除配置项
^^^^^^^^^^^^^^^^^^^^^

.. code:: shell

   #添加配置项
   git config [--local|--global|--system]  section.key value

   #删除配置项
   git config [--local|--global|--system] --unset section.key

例如：

.. code:: shell

   git config --global color.ui true   	#打开所有的默认终端着色
   git config --global alias.ci commit   	#令别名 ci 是 commit 的别名

.. _header-n153:

（5）常见配置项
^^^^^^^^^^^^^^^

.. code:: shell

   [alias]  
   co = checkout  
   ci = commit  
   st = status  
   pl = pull  
   ps = push  
   dt = difftool  
   l = log --stat  
   cp = cherry-pick  
   ca = commit -a  
   b = branch 

   user.name  #用户名
   user.email  #邮箱
   core.editor  #文本编辑器  
   merge.tool  #差异分析工具  
   core.paper "less -N"  #配置显示方式  
   color.diff true  #diff颜色配置  
   alias.co checkout  #设置别名
   git config user.name  #获得用户名
   git config core.filemode false  #忽略修改权限的文件  

.. _header-n157:

四、Git 操作
------------

|image2|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：Git 常用操作</center></body></html>

.. _header-n160:

1、获取 Git 仓库
~~~~~~~~~~~~~~~~

主要由两种方式：新建、克隆远程仓库

.. _header-n162:

（1）新建
^^^^^^^^^

在工作目录下：

.. code:: shell

   git init 

新建工作目录：

.. code:: shell

   git init [Directory]

.. _header-n167:

（2）克隆远程仓库
^^^^^^^^^^^^^^^^^

将远程服务器上的仓库完全镜像一份至本地，而不是取某一个特定版本，所以不是
checkout，语法格式如下：

.. code:: shell

   # 克隆一个项目和它的整个代码历史(版本信息)至当前目录
   git clone [url]

.. _header-n170:

2、Git 文件操作
~~~~~~~~~~~~~~~

.. _header-n171:

（1）文件状态
^^^^^^^^^^^^^

.. _header-n172:

文件状态转换
''''''''''''

版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

|image3|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：文件状态转换图</center></body></html>

-  **Untracked**: 未跟踪, 此文件在文件夹中, 但并没有加入到git库,
   不参与版本控制. 通过\ ``git add`` 状态变为\ ``Staged``.

-  **Unmodify**: 文件已经入库, 未修改,
   即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处,
   如果它被修改, 而变为\ ``Modified``. 如果使用\ ``git rm``\ 移出版本库,
   则成为\ ``Untracked``\ 文件

-  **Modified**: 文件已修改, 仅仅是修改, 并没有进行其他的操作.
   这个文件也有两个去处,
   通过\ ``git add``\ 可进入暂存\ ``staged``\ 状态,
   使用\ ``git checkout`` 则丢弃修改过, 返回到\ ``unmodify``\ 状态,
   这个\ ``git checkout``\ 即从库中取出文件, 覆盖当前修改

-  **Staged**: 暂存状态. 执行\ ``git commit``\ 则将修改同步到库中,
   这时库中的文件和本地文件又变为一致, 文件为\ ``Unmodify``\ 状态.
   执行\ ``git reset HEAD filename``\ 取消暂存,
   文件状态为\ ``Modified``\ 。

-  **Commited**\ ：已提交，成为仓库中一个正式明确的版本。

.. _header-n187:

查看文件状态
''''''''''''

.. code:: shell

   #查看指定文件状态
   git status [filename]

   #查看所有文件状态
   git status

.. _header-n189:

（2）增删文件/目录
^^^^^^^^^^^^^^^^^^

若想增加文件或目录到仓库版本中，须先移入暂存区。

.. code:: shell

   # 添加指定文件到暂存区
   $ git add [file1] [file2] ...

   # 添加指定目录到暂存区，包括子目录
   $ git add [dir]

   # 添加当前目录的所有文件到暂存区
   $ git add .

从暂存区删除。

.. code:: shell

   #直接从暂存区删除文件，工作区则不做出改变
   git rm --cached <file>

   #暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
   git reset HEAD <file>...

移除工作区所有未跟踪文件。

.. code:: shell

   git clean [options] 
   #一般会加上参数-df，-d表示包含目录，-f表示强制清除。

.. _header-n196:

（3）文件修改
^^^^^^^^^^^^^

查看文件修改后的差异。

.. code:: shell

   git diff [files]
   #若不加 files 则查看所有有改动的文件。

.. _header-n199:

**签出**
''''''''

检出命令git
checkout是git最常用的命令之一，同时也是一个很危险的命令，因为这条命令会重写工作区

常见使用：

.. code:: shell

   git checkout branch
   #检出 branch 分支。
   #更新 HEAD 以指向 branch 分支，以及用 branch 指向的树更新暂存区和工作区。

   git checkout
   #汇总显示工作区、暂存区与HEAD的差异。
   git checkout HEAD
   #同上

   git checkout -- filename
   #用暂存区中 filename 文件来覆盖工作区中的 filename 文件。
   #相当于取消自上次执行 git add filename以来（如果执行过）的本地修改。
   #file_name 为 . 时表示所有文件。

   git checkout branch -- filename
   #维持HEAD的指向不变。用 branch 所指向的提交中 filename 替换暂存区和工作区中相应的文件。
   #注意会将暂存区和工作区中的filename文件直接覆盖。
   #file_name 为 . 时表示所有文件。

   git checkout commit_id -- file_name
   #如果不加commit_id，那么表示恢复文件到本地版本库中最新的状态。
   #file_name 为 . 时表示所有文件。

.. _header-n203:

（4）忽略文件
^^^^^^^^^^^^^

有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。

2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。

3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。

4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。

5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。

如：

.. code:: shell

   #为注释
   *.txt #忽略所有 .txt结尾的文件
   !lib.txt #但lib.txt除外
   /temp #仅忽略项目根目录下的TODO文件,不包括其它目录temp
   build/ #忽略build/目录下的所有文件
   doc/*.txt #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt

.. _header-n219:

（5）文件提交
^^^^^^^^^^^^^

通过add只是将文件或目录添加到了index暂存区，使用commit可以实现将暂存区的文件提交到本地仓库。

.. code:: shell

   # 提交暂存区到仓库区
   $ git commit -m [message]

   # 提交暂存区的指定文件到仓库区
   $ git commit [file1] [file2] ... -m [message]

   # 提交工作区自上次commit之后的变化，直接到仓库区，跳过了add,对新文件无效
   $ git commit -a

   # 提交时显示所有diff信息
   $ git commit -v

   # 使用一次新的commit，替代上一次提交
   # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
   $ git commit --amend -m [message]

   # 重做上一次commit，并包括指定文件的新变化
   $ git commit --amend [file1] [file2] ...

撤销上一次的提交

.. code:: shell

   git reset --hard HEAD~1

.. _header-n224:

（5）日志与历史
^^^^^^^^^^^^^^^

查看提交日志

.. code:: shell

   git log

查看 Bash 的命令输入历史

.. code:: shell

   history

查看所有分支日志

.. code:: shell

   git reflog

.. _header-n231:

3、Git 分支
~~~~~~~~~~~

**分支策略**

在分支上独立工作。

master主分支应该非常稳定，用来发布新版本，一般情况下不允许在上面工作，工作一般情况下在新建的dev分支上工作，工作完后，比如上要发布，或者说dev分支代码稳定后可以合并到主分支master上来。

Git 切换分支的速度非常快。

.. _header-n236:

（1）分支原理
^^^^^^^^^^^^^

当我们创建新的分支，例如\ ``dev``\ 时，Git新建了一个指针叫\ ``dev``\ ，指向\ ``master``\ 相同的提交，再把\ ``HEAD``\ 指向\ ``dev``\ ，就表示当前分支在\ ``dev``\ 上：

|image4|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：分支讲解1</center></body></html>

你看，Git创建一个分支很快，因为除了增加一个\ ``dev``\ 指针，改改\ ``HEAD``\ 的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对\ ``dev``\ 分支了，比如新提交一次后，\ ``dev``\ 指针往前移动一步，而\ ``master``\ 指针不变：

[|image5|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：分支讲解2</center></body></html>

假如我们在\ ``dev``\ 上的工作完成了，就可以把\ ``dev``\ 合并到\ ``master``\ 上。Git怎么合并呢？最简单的方法，就是直接把\ ``master``\ 指向\ ``dev``\ 的当前提交，就完成了合并：

|image6|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：分支讲解3</center></body></html>

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除\ ``dev``\ 分支。删除\ ``dev``\ 分支就是把\ ``dev``\ 指针给删掉，删掉后，我们就剩下了一条\ ``master``\ 分支：

|image7|

.. raw:: html

   <html xmlns="http://www.w3.org/1999/xhtml"><head></head><body><center>图：分支讲解4</center></body></html>

.. _header-n251:

（2）分支中常用指令
^^^^^^^^^^^^^^^^^^^

.. code:: shell

   # 列出所有本地分支
   git branch

   # 列出所有远程分支
   git branch -r

   # 列出所有本地分支和远程分支
   git branch -a

   # 新建一个分支，但依然停留在当前分支
   git branch [branch-name]

   # 新建一个分支，并切换到该分支
   git checkout -b [branch]

   # 新建一个分支，指向指定commit
   git branch [branch] [commit]

   # 新建一个分支，与指定的远程分支建立追踪关系
   git branch --track [branch] [remote-branch]

   # 切换到指定分支，并更新工作区
   git checkout [branch-name]

   # 切换到上一个分支
   git checkout -

   # 建立追踪关系，在现有分支与指定的远程分支之间
   git branch --set-upstream [branch] [remote-branch]

   # 合并指定分支到当前分支
   git merge [branch]

   # 选择一个commit，合并进当前分支
   git cherry-pick [commit]

   # 删除分支
   git branch -d [branch-name]

   # 删除远程分支
   git push origin --delete [branch-name]
   git branch -dr [remote/branch]

.. _header-n254:

（4）Git GUI
~~~~~~~~~~~~

通过命令行可以深刻的理解 Git，Git GUI 或 IDE 插件却可以更加直观操作
Git。

.. _header-n257:

五、远程仓库
------------

还没写

.. |image1| image:: https://s3.ax1x.com/2021/02/03/yMS858.png
   :target: https://imgchr.com/i/yMS858
.. |image2| image:: https://s3.ax1x.com/2021/02/03/ylpeFP.png
   :target: https://imgchr.com/i/ylpeFP
.. |image3| image:: https://s3.ax1x.com/2021/02/03/yl98je.jpg
   :target: https://imgchr.com/i/yl98je
.. |image4| image:: https://s3.ax1x.com/2021/02/04/y3Zu4g.png
   :target: https://imgchr.com/i/y3Zu4g
.. |image5| image:: https://s3.ax1x.com/2021/02/04/y3ZnUS.png
.. |image6| image:: https://s3.ax1x.com/2021/02/04/y3ZMCQ.png
   :target: https://imgchr.com/i/y3ZMCQ
.. |image7| image:: https://s3.ax1x.com/2021/02/04/y3ZmE8.png
   :target: https://imgchr.com/i/y3ZmE8
