# 记录一些常用的代码
（一段时间不用经常忘记）
***
## github相关
```
//配置用户信息

git config user.name "your name" --global
git config user.email "your email" --global

//初始化仓库

git init

//添加远程仓库

git remote add 别名 "链接地址(ssh)" //（别名一般是 origin）
git remote -vv //(获得仓库信息)
ssh-keygen -C "comment备注" //(生成密钥对)进入用户家目录的 .ssh 文件夹，找到刚才建立的 id_rsa.pub 文件，以文本方式打开，复制其中的内容。
//在github setting中点击 New SSH Keys，将复制的公钥内容粘贴到 Key 输入框，并给该 SSH Key 定义一个 Title；然后Add SSH key 添加该 Key。

//提交推送

<!-- 如果你觉得 git add 提交缓存的流程太过繁琐，Git 也允许你用 -a 选项跳过这一步。命令格式如下： -->
git commit -a

git add . //提交所有修改的和新建的数据暂存区
git add -u 
git add –update//提交所有被删除和修改的文件到数据暂存区
git add -A 
git add –all//提交所有被删除、被替换、被修改和新增的文件到数据暂存区
git status//查看状态
git commit -m "input yours message"//提交文件更改
git push -u origin main//推送到main分支


# 创建并切换到 main 分支
git checkout -b main
# 推送 main 分支到远程，并设置追踪关系
git push -u origin main


//删除仓库中文件

git pull origin master
dir  //查看有哪些文件夹
git rm -r --cached //要删除的文件夹
git commit -m '删除了169.\Majority\\ Element'
然后直接 git push -u origin master(或者git push)

git mv -f （100.\Same\ Tree） （100.Same_Tree）
git add -u 100.Same_Tree   #添加新文件
git add -u newfolder (-u选项会更新已经追踪的文件和文件夹)
git commit -m \"修改文件名\"
git push origin master
```
***
## Linux相关
```
xvfb-run qq --no-sandbox //前台启动napcat
```
***
```
top      //查看系统负载(动态)
ps aux  //查看所有进程
ps aux | grep "name" //查看指定进程
screen -S "name"
screen -r "name"//恢复指定编号或名称的视窗任务
screen -X -S "name" quit
screen ls
ctrl + a + d//暂时离开当前视窗
ctrl + a + k//关闭当前视窗
```
## Others
```
redis-server.exe //windows启动redis
```
