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

5. ​