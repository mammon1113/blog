# CSS的全称
层叠样式表(英文全称：Cascading Style Sheets)
样式定义如何显示Html元素，样式通常储存在样式表。实现了内容与样式相分离。
``` javascript 
h1 {
  color: red;
  font-size: 20px;
  /*这是注释*/
}
a:hover{
  color: red;

}
```
![css格式](http://upload-images.jianshu.io/upload_images/7921365-d7e9e0742059a505.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# CSS的引入方式
* 内联样式
将css内容写进需要渲染的标签中
`<h1 style="color: red; font-size: 20px;"></h1>`
一般来说很少会采用这种方式去写css。
首先，代码将会变得冗长，不利于维护，也无法实现html与css相互分离的特点。其次相同的样式不能统一引用，将降低效率。
* 内部样式（嵌入式）
将css样式写入style标签中，放在页面里。
``` javascript 
<style type="text/css">
  h1 {
    color: red;
    font-size: 20px;
  }
</style>
```
通常会将内部样式放入head当中，这种引入比较适合单页面，可以一目了然地查看 HTML 结构和 CSS 样式。但是写入的css样式也仅仅对其本身页面有效，不利于多页面开发，且内部样式结构将会使代码过长，不利于阅读和维护。
* 外部样式
``` javascript 
<head>
  <link rel="stylesheet" type="text/css" href="index.css">
</head>
```
将样式独立出来并通过寻址来进行引用的方式，这种引入方式不仅结构清晰，html/css相互独立相互分离，且让开发人员可以多次重复利于同一css文件进行开发，减少了代码冗余，利于维护。这种方式也是目前css引入的主流方式，推荐使用。
* 导入样式
``` javascript 
<style>
  @import url("hello.css");
  @import "world.css";
</style>
``` 
导入样式有如上两种方式的写法。这与外部样式（导入样式也是外部样式的一种）本质上很相似，都是通过外部的css文件来进行渲染。但是会有所差别。
区别：
（1）加载快慢的区别：
通常HTML加载的同时，将会同时下载css进行渲染，但是@import方式则会等待页面全部加载完毕后，在进行下载。所以如果页面采用@import的方式进行渲染，用户网络条件不好时将有可能会导致页面渲染不完全、失败、闪烁等情况。
（2）兼容性的区别：
link标签本身无兼容性问题。然而@import是 CSS2.1 才出现的概念，低版本浏览器可能会出现不支持的现象，无法正确导入外部样式文件。不过，现在的主流浏览器版本基本都不会出现无法正确加载的现象了。
（3）范围的区别：
link是XHTML标签，除了加载css之外，还可以定义RSS等其他内容。@import只能写入css样式。
（4）DOM控制区别：
dom无法直接控制@import，只能通过控制link实现加载不同css文件
总结：一般使用外部样式。其他三种用的很少，并不建议直接使用。
# css引入路径的正确写法：
这里又要说到相对路径与绝对路径了。
1、相对路径：相对于当前文件的路径。
2、绝对路径：是目录在硬盘上真正的路径。
"./"：代表目前所在的目录。
"../"：代表上一层目录。
以"/"开头：代表根目录。
如果非要去举例的话..小黄pian的存储地址从头到尾你无不烂熟于心，那个地址就是绝对路径，没跑了。闭着眼睛你都知道在哪个地方存着。
但是在css引用中，通常用到相对路径与http外部链接路径（网站路径）
以外部方式为例，简单的说下关于href的规则。
![内容区块](http://upload-images.jianshu.io/upload_images/7921365-2fd4ea8033c4204f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
不难看出，根目录下有S1文件夹和Image/Image.jpg，S1内有P1.html文件和S2文件夹。S2下有P2.html和P2.Img文件。
1、文件在当前目录:
P2.html访问P2.Img
`<link rel="stylesheet"  href=”./Page2Image.jpg”>
或者
<link rel="stylesheet" href=”./Page2Image. jpg”>`
2、文件在上一层目录
P1.html访问Image下的Image.jpg
`<link rel="stylesheet"  href=”../Image/Image.jpg”>`
P2.html访问Image下的Image.jpg
`<link rel="stylesheet"  href=”../../Image/Image.jpg”>`
3、文件在下一层目录
P1.html访问S2文件夹下的P2.Img
`<link rel="stylesheet"  href=”./S2/P2.Img”>`
`<link rel="stylesheet"  href=”S2/P2.Img”>`
为何要花那么多笔墨说这些是因为相对路径和绝对路径还是蛮重要的，尤其是当页面引入很多图片和链接的时候，很容易出错。
总结一下

路径 | 含义  
----|------
css/a.css | 当前css目录下的a.css文件（相对路径）
./css/a.css | 当前css目录下的a.css文件（相对路径）
b.css | 当前css目录下的b.css文件（相对路径）
../imgs/a.png | 父目录下（上一个目录）的imgs目录中的a.png文件  
/Users/hunger/project/css/a.css | 根目录下的users...的a.css文件（绝对路径）
/static/css/a.css | 会获取到网站根目录下的static目录-->css目录-->a.css文件（多用于服务器中的static目录）  
http://cdn.jirengu.com/kejian1/8-1.png | 外部链接地址（通过http协议寻址到某服务器中的文件）  

# 如何加载图片
还是路径的问题。
1.可以将图片上传至服务器端，通过相对路径引用到img标签当中。
2.可以将图片上传至图床中，生成出网站链接地址，将该url引入到img的src属性中。
# 
# html和css的书写规范
1.css中语法使用小写，缩写
2.id和class使用有意义的单词，分隔符建议使用-
3.属性值是0的省略单位
4.属性名冒号后面添加一个空格(属性值前面)
5.属性与属性之间要有分号，最好换号书写
6.meta标签中的编码格式建议使用 "UTF-8"
7.html5的声明类型为<!DOCTYPE html>要注意该大写的最好大写
8.css选择器 与 { 之间要有空格
更多可参考[HTML简介篇](http://www.jianshu.com/p/6b4321d1828f "Title")
# 开发者工具
作为一名前端开发人员，这是必须掌握的一项实用技术，用起来极其方便。
通常调试css的时候也经常用到，说一些最近常用的技巧。
1.选中styles中的某项需要调节的css属性，切换属性值即可看到页面的变化，这是学习css的最好途径，看起来也很直观。
2.调节像素的时候可以选中该样式按住"alt"+“上或下”即可调节。
3.console控制台我想经常会用到，但是介绍一个更好地调试方法。
![image.png](http://upload-images.jianshu.io/upload_images/7921365-bb9c52754ac2922a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这里测试js代码会更轻松。
[开发者工具篇](http://www.jianshu.com/p/07ce3cb6798c "Title")
[备查](http://www.jianshu.com/p/cf36d48652f4 "Title")

