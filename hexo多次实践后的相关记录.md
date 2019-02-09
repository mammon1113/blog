# hexo多次实践后的相关记录
其实和过去的操作并无分别，但是因为换电脑和更改删除多次后，出现了一些问题。经过多次实践，总结出一套更方便的流程
------------
####进入一个安全的目录，比如 cd ~/Desktop 或者 cd ~/Documents，也就是仓库目录
####在 GitHub 上新建一个空 repo，repo 名称是「你的用户名.github.io]
####npm install -g hexo-cli，安装 Hexo
####hexo init myBlog
####cd myBlog
####npm i
####hexo new 开博大吉，你会看到一个 md 文件的路径
####npm install hexo-deployer-git --save，安装 git 部署插件
####hexo deploy
截至到此都是正常的操作流程
但是由于电脑已经安装过一次了，所以有时候会遇到错误（新电脑装hexo几乎不出错）
出错点提示：新电脑或格式化的机子几乎不出问题
1.  npm install -g hexo-cli 报错，大多数是淘宝镜像的原因，执行 npm install -g cnpm --registry=https://registry.npm.taobao.org 
参考：https://www.cnblogs.com/zhvon/p/5351043.html
2. hexo init myBlog，出现“Start blogging with Hexo!”则成功
3.npm install报错，执行 npm config set registry https://registry.npmjs.org/
在执行 npm i ,如果还不行，执行npm install -g cnpm --registry=https://registry.npm.taobao.org
在执行cnpm install
参考：https://segmentfault.com/q/1010000010751949
4.执行 npm install hexo-server --save，如果成功，则提示“+ hexo-server@0.3.3”
参考：https://blog.csdn.net/weixin_41196185/article/details/79124015
5.执行npm install hexo-deployer-git --save 部署成功则显示“hexo-deployer-git@1.0.0”
注：检测是否安装成功：hexo -v node-v npm-v
-------------
新电脑装hexo，按照原本的教程走。
只不过，另外找个地方，下载orange-geXXX的仓库（博客生成程序），将里面的source和themes复制替换到myblog里面，其中config.ymi可以自行修改，也可以直接复制粘贴到新的hexo博客生成程序里面（myblog/也就是or-g仓库）
如果没有KEY，必须要修改config.ymi为http登录模式，在发布新md的时候，提示输入用户名和密码，验证通过后，就发布成功了，此时myblog文件夹中会出现一个deploy的文件夹。如果电脑有KEY，就没什么问题了，不需要额外修改为http的链接。
------------
用户名.io的仓库，是浏览hexo的程序文件，也就是生成出来可供浏览的index