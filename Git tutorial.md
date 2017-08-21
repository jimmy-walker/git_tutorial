### Git tutorial

0. 安装后配置

      git config --global user.name "你的名字" 
      git config --global user.email "你的邮件地址" 

1. 在本机生成key，github添加ssh key，官方有文档

   第一步，创建SSH Key。在用户主目录下，看看有没有.ssh目录(C:\Users\jimmylian\.ssh)，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
   `ssh-keygen -t rsa -C "你的邮件地址"`

   第二步，登陆GitHub，打开“Account settings”，“SSH Keys”页面,然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。

2. 初始化一个Git仓库，使用git init命令。

3. 添加文件到Git仓库，分两步：

  第一步，使用命令git add \<file>，注意，可反复多次使用，添加多个文件。

  如果提示： LF will be replaced by CRLF，那么设置`git config --global core.autocrlf false`

  第二步，使用命令git commit -m "xxx"，完成。

4. ​