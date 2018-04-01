在学过后写一篇文章真的是特别有好处的一件事，这种复盘是最有效的。言归正传，这两天一直在不停地试验github，今天终于有时间写一篇总结。我过两天会在写一个原理篇，剖析一下暂存区这些基本原理方面的问题，今天的文章主要是复盘一下操作。
# Glthub是什么
这个我就不说太多了，做程序方面工作的几乎没有不认识它的吧。粗浅的认知就把他当做是一个可多人协同开发且能帮你托管放置源码的“服务器”吧。当然它不仅仅如此而已。
写代码这件事并不轻松，多人一起开发就更不简单了，github主要就是为了解决多人开发时的不足，比如今天A改了b页面，明天C改了d页面，来来回回最后谁也不知道自己改了什么，合并起来一团糟，github快照技术就可以解决多人协作开发的大问题。当然这就是最终的核心目标---代码管理
# 主要操作步骤
如果我想建立一个仓库，主要操作方法有两种，我个人比较喜欢后者。
#### 第一种：
（1）打开github页面新建一个仓库
（2）![点击绿色的新建一个](http://upload-images.jianshu.io/upload_images/7921365-542b45850e2b5d96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)名字就是项目名称
（3）![这里要打勾](http://upload-images.jianshu.io/upload_images/7921365-891ed7e22eb31c47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
（4）这时候远端就建立了一个新的仓库了。只不过你本地端还没有
（5）打开git输入以下命令
`git config --global user.name "XXX"`
`git config --global user.email" XXX@.com"`
输入这些是为了今后你在修改代码上传后记录会有你的名字和邮箱
你可以输入`git config -l `就可以查询到相关参数了
当然如果你后期需要修改邮箱和名字直接输入`git config --global XXX`替换就好了。
## 重点：因为你本地端与远端没有一个对应的连接，为了让它们产生匹配（就跟密码狗一样）你需要有个密码钥匙，github会生成出2个密码钥匙，一个远端一个本地端，相互对应你就可以操作了和上传了。
（6）设置区找到ssh
![ssh命令行](http://upload-images.jianshu.io/upload_images/7921365-feed57cbba315305.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
直接复制粘贴在git上输入`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`这个邮箱名称输入你注册github的。
（7）一路回车（一般我不修改ssh文件的生成地址）直到出现下图的样子
![加密文件生成成功](http://upload-images.jianshu.io/upload_images/7921365-30b528b5c522afcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
（8）git下输入cat命令打开ssh后缀为pub的公钥文件并把语句复制下来存放在下图位置
![点击新建即可](http://upload-images.jianshu.io/upload_images/7921365-799f338efc15bf2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这时你的电脑便与远端建立了密码对应关系，就可以克隆你之前在远端建立的仓库到本地端了。
（9）命令行输入`git clone git地址`这里输入ssh对应的地址，此时便建立了权限
（10）新建文件撸代码
（11）命令行分别输入 `git add .` `git commit -am "写描述"` `git push origin master`代表把master分支推送至本地端和远端来源，origin就是远端的来源
#### 第二种：
（1）打开github页面新建一个仓库
（2）![点击绿色的新建一个](http://upload-images.jianshu.io/upload_images/7921365-542b45850e2b5d96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)名字就是项目名称
（3）![这里不要打勾](http://upload-images.jianshu.io/upload_images/7921365-891ed7e22eb31c47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)注意不要打钩
（4）在本地你可以建立文件夹（仓库），建立一些文件（撸代码的产物），打开git，输入`git config --global user.name "名字"``git config --global user,email "邮箱"`
（5）`git init` 建立.git初始化本地仓库
（6）`git remote add origin gitXXX(ssh地址)`  这样便建立了对应关系
注意：如果没有创建公钥私钥，还是要按照方法一中的办法建立密码对应联系
（7）`git add .` `git commit -am "miaoshu"` `git push origin master`就可以上传成功了。
以上就是建立仓库并进行简单的修改上传的操作步骤。
# 分支操作
# 额外的命令行
本篇因为是基础篇，所以不涉及太多额外的命令行，只介绍了一些常用的用于复盘。
1. `git config -l`：可以查看相关参数，例如上传时对应的邮箱和名字
2.`git remote -v`:用于查看地址别名（来源）对应的地址
3.`git remote add 别名 ssh地址`用于建立远端别名与地址的对应关系 。例：`git remote add origin2 git@xxx.com`
4.`git remote rename 原来源 新来源`例：`git remote rename origin2 glob1`此命令将把origin2替换成glob1的来源
5.`git remote remove 来源` 例：`git remote remove glob1` 此命令将删除该来源以及所对应的地址
6.`git remote set-url 标签 地址`例：`git remote set-url glob1 git@qq.com`此命令将会修改glob1标签所对应的地址
7.`git config --global "user.name" XX``git config --global "user.email" XX`这个命令只需要输入一次就可以了，以后每次上传都会自动记录这些信息，但是如果你某个项目中突然想用别的名字或邮箱，但是别的项目都不变，那么你只需要在上传该项目之前输入这个命令，但是切记不需要加`--global`即可
8.mkdir -p "/cmdd/dec/"
注：(不加引号也可成功，但是如果你建立的文件夹有特殊符号例如空格，就要引起来让bash明白你建立的是一个整体
9.`whoami`可以查看本机用户名是什么
10.`touch`可以改变文件的时间
11.`curl -L 链接地址 > 文件名` 下载文件
12.`wget -p -H -e robots=off 链接地址` 下载整站（当前页面）

先更新到这里，以后用到了陆续在更，目前这些已经基本够用。