## 什么是Bash？
* Bash是分布式版本控制系统，没那么复杂，简单理解为它就是个程序，只是能做很多了不起的事情
* 你平时操作电脑，用鼠标控制文件，这些都叫做“可视化操作”，与它对应的就是命令行操作即GltBash
* 你可以在Bash下可以输入各种命令符，通过它就可以轻松的操控电脑中的程序或文件

它长成这样...![BASH初始化界面](http://upload-images.jianshu.io/upload_images/7921365-59e0e4ec14139aad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 我能用它做什么？
* 操控你的电脑
* 写脚本
## 为什么要学Bash？
* 如果你是一名程序工作者，工作中会经常接触
* 提高你的工作效率。一句命令能解决的问题，如果用可视化操作需要花费相对长的时间
* 更稳定，通过命令行你很清晰的知道你做的事情
* 用代码操作更省心，不必在打开N多个窗口和文件
## 如何学好命令行？
不必花太多功夫去看各种命令，更不必去死记硬背，这样你很快就被吓到了。你要做的就是看完这篇文章，掌握最基本的一些“增”“删““改““查”命令行，有了这些基础后，平时操作电脑时多用命令行来进行操作，每天学几个新命令，慢慢的就可以彻底掌握git命令行了。
##### 1.cd命令
代码：` cd /路径/`
例子：`cd /c/`就进入了C盘中。
什么时候会用到：当你查找、删除一个文件的时候，你需要找到该文件所在的盘符位置并到达该文件所对应的位置。

![进入C盘](http://upload-images.jianshu.io/upload_images/7921365-ace07000d2375038.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 2.mkdir命令
代码：`mkdir 文件夹名称`
例子：`mkdir A` 建立一个名为“A”的文件夹

![在C盘中建立A文件夹](http://upload-images.jianshu.io/upload_images/7921365-062ac1f0e0de69c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 3.touch命令
代码：`touch 文件名称`
例子：`touch A.txt` 建立一个名为“A”的文本。当然你可以建立任何文件

![建立A.txt](http://upload-images.jianshu.io/upload_images/7921365-05a7a92e39d63208.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 4.cp命令
代码：`cp 文件1 文件2`
例子：`cp A.txt  B.txt` 复制“A”文本，粘贴为B文本。

![复制粘贴文件](http://upload-images.jianshu.io/upload_images/7921365-d82949f24932e4fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 5.cp -r命令
代码：`cp 目录1 目录2`
例子：`cp A.txt  B.txt` 复制“A”文本，粘贴为B文本。
什么时候会用到：当你复制一个文件夹（该目录下有文件）的时候，你需要- r，否则无法成功复制。

![在C盘下复制A文件夹粘贴为B文件夹](http://upload-images.jianshu.io/upload_images/7921365-9379db882edbee80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 6.mv命令（1）
代码：`mv A C`
例子：`cp A C` 使A文件夹的名字变为C。当然改变文件的名字也如此操作

![将A文件夹名称改为C](http://upload-images.jianshu.io/upload_images/7921365-8b6a0b04433ce2eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 7.mv命令（2）
代码：`mv C B`
例子：`cp C B` 将已经改变为C的文件夹移动到B文件夹。当然改变文件的名字也如此操作
（1）与（2）的区别：默认为修改名称，当发现改的名称与当前目录下别的文件一致是便会将文件移动到别的目录中。MV具有修改名称与移动两个功能。

![将C目录移动到B目录中](http://upload-images.jianshu.io/upload_images/7921365-07188f70c4bbef10.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 8.echo命令（1）
代码：`echo XXX > 文件`
例子：`cp 123 > A.txt` 将“123”字符串输入到A文本中

![文本中显示了我们输入的“123”](http://upload-images.jianshu.io/upload_images/7921365-694fc328bdcf17eb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 9.echo命令（2）
代码：`echo XXX >> 文件`
例子：`cp 789 >> A.txt` 将“789”字符串输入到A文本中
（1）与（2）的区别：如果你直接按照（1）的方法输入789，你打开文本后会发现字符串“123”没了，其实它被你的新命令覆盖了。如果想在该文本不变的基础上输入新的字符串或代码，那么你需要使用（2）的命令

![新增789字符串](http://upload-images.jianshu.io/upload_images/7921365-06d8cd0b364742f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 10.ls命令
代码：`ls`
例子：`ls` 将显示你当前目录下所有的文件

![B文件夹下的文件都被显示出来了](http://upload-images.jianshu.io/upload_images/7921365-682ca355b94c72a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
是不是很简单？
当然还有更巧妙的
你可以试着输入`ls -l`以及`ls -a`
你会发现罗列显示出了父目录以及文件大小建立修改时间等相关参数

![ls -a与ls -l](http://upload-images.jianshu.io/upload_images/7921365-66ad0e32b31fe23e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 11.rm命令
代码：`rm -r 文件夹` `rm  文件`
例子：`rm -r C` 将删除C目录，`rm  A.txt`将删除A文件

![删除C文件夹和A文本](http://upload-images.jianshu.io/upload_images/7921365-2c9e06ec5ce0c9bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
说明：请擅用rm-r命令。
##### 12.pwd命令
代码：`pwd`
例子：`pwd` 将你当前所在的路径显示出来

![会很直观的显示你的工作目录](http://upload-images.jianshu.io/upload_images/7921365-2669184e010f968d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 13.clear命令
代码：`clear`
例子：`clear` 将你当前bash上已输命令清空

![感觉很乱](http://upload-images.jianshu.io/upload_images/7921365-c468843cce84c5c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![输入后就会把命令清除](http://upload-images.jianshu.io/upload_images/7921365-5f219d5dfd327018.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
以上13个命令就是操作bash上最重要的增删改查，操作几次就能很轻松的记住。只要入门了，后面学起来就简单了
## PS：其实，电脑一开始都是命令行操作的，后来才有了可视化。如今的你只不过是学了十几年的可视化操作，没接触过命令行操作，才会觉得可视化简单命令行复杂，其实那只不过是因为你不习惯命令行的操作模式而已，想想你最初玩Windows不也是各种不懂吗？