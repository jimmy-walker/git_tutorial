### Git tutorial

0. 安装后配置

      **git config --global user.name "你的名字"** 
      **git config --global user.email "你的邮件地址"** 

1. 在本机生成key，github添加ssh key，官方有文档

   第一步，创建SSH Key。在用户主目录下，看看有没有.ssh目录(C:\Users\jimmylian\.ssh)，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
   `ssh-keygen -t rsa -C "你的邮件地址"`

   第二步，登陆GitHub，打开“Account settings”，“SSH Keys”页面,然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。

2. 初始化一个Git仓库，使用git init命令。

3. 添加文件到Git仓库，分两步：

  第一步，使用命令**git add \<file>**，注意，可反复多次使用，添加多个文件。就是把文件修改添加到暂存区（stage）。

  如果提示： LF will be replaced by CRLF，那么设置**git config --global core.autocrlf false**

  如果对文件夹内有几处操作，可以对文件夹add从而减少次数。

  第二步，使用命令**git commit -m "xxx"**，完成。实际上就是把暂存区的所有内容提交到当前分支。

  ​

  ![](Working Directory and Repository.jpg)

4. 在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步

   第一步，在本地仓库下执行：**git remote add origin [git@github.com:jimmy-walker/git_tutorial.git](git@github.com:jimmy-walker/git_tutorial.git) ** ，远程库的名字就是origin，所以代表从远程得到origin库。

   第二步，执行**git push -u origin master**，我们第一次推送`master`分支时，加上了`-u`参数，代表upstream表示：Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令：`git push origin master`，代表将本地的master分支push到远端的origin分支。

   注：如果是直接从GitHub上clone下来的，那么修改后直接**git push origin master**即可。

5. 修改回撤

   常用操作已经用红圈圈出，注意git reset --soft我自己认为还不如直接用--hard。因为一般而言git commit后修改区域和暂存区域都是空的。

   `--` 的名称叫做double dash，是bash的内置命令，用来标记可选命令选项的结束。即在它后面的带 `--` 的字符串，不被当做是一个命令选项。

   > More precisely, a double dash (--) is used in bash built-in commands and many other commands to signify the end of command options, after which only positional parameters are accepted.

   举例：在 grep 命令中 `-V` 原本是一个可选的命令参数(options)，打印出 grep 命令的版本。

   但结合`--`后，以下命令表示在 d1.txt 文件中查找 "-V" 字符串`grep -- -V d1.txt`

   Git 的一些命令中，借鉴了这种用法。使用 `--` 去隔离开“树”与“路径”。

   例如，你想还原 一个文件 `path/to/file.txt`，在Git中使用如下命令

   `git checkout path/to/file.txt`

   但是天杀的居然有一个文件名字就叫做 "master"如果你套用上面的命令，想还原“master”文件

   `git checkout master`

   最终起的效果是变成切换到了master分支上。

   正确的做法是使用 `--`，这样它后面的字符串不会当做“树”，而认为是文件路径。

   `git checkout -- master`

   ![](git-flow.png)

   ​

6. 部分修改

   重要概念：**当修改与暂存区都无东西时，工作区与本地库相等。**如果有一个东西，那么说明两者不相等。而如果commit了a文件和b文件，想保留新的a文件和上一版本的b文件，那用**git reset HEAD^ b**把上一版本中的b文件重新放入缓存区以及修改处。**此时工作区和本地库相等都是HEAD版本，所以需要checkout和commit同时修改工作区和本地库**。

   ![](git reset HEAD^ file.png)

7. 删除文件


   其实这里的删除文件是上图中修改的一个例子而已。

   还是用上述方法添加到暂存区或是放弃修改，只不过除了add之外，还可以用**git rm**

   `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

