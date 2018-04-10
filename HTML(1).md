制作网页离不开html，html就像是页面的骨架，必不可少，十分重要。学习过后介绍一些必备的知识。
# html/xhtml/html5
html（HyperText Markup Language）有很多版本，其中现在主流的就是html5版本。
1.HTML是超文本标记语言，语法较松散
2.为了解决该问题，衍生出xhtml
2.xhtml语法较为严谨，后来诞生了HTML5，过渡期用xml（可扩展标记语言），所有标签必须闭合
3.HTML5标签不用闭合
总结：XHTML是当前HTML版的继承者。HTML语法要求比较松散，这样对网页编写者来说，比较方便，但对于机器来说，语言的语法越松散，处理起来就越困难，对于传统的计算机来说，还有能力兼容松散语法，但对于许多其他设备，比如手机，难度就比较大。因此产生了语法要求更加严格的XHTML。
> http://www.w3.org/TR/html5可查看具体的技术文档（specifications）
# 表现（内容）、样式、行为分离原则
1.HTML内容、样式（css）、行为（js），彼此要相互分离
2.html尽量不要出现行内样式
3.html的重点是语义化
# 文档声明
`<！DOCTYPE HTML>`就是html5的文档声明，写html的时候必须加上，以便告诉浏览器要使用html5，注意大写。否则浏览器可能会出现乱码。
# 基础标签
1.根元素`<html lang="en">`代表该页面默认是英文进行读取，如果浏览器判断是英文，如果用户有翻译插件就会提示翻译。
2. 关于mata
(1)`<mata charset="utf-8"> `代表编码格式用uft-8（主流），当然如果页面是用别的编码格式的也可修改。其实后端响应页面的时候会对用户的页面进行Content-type设置。详见HTTP
    (2) `<meta name="viewport" content="width=device-width, initial-scale=1.0">`代表手机端自适配窗口大小
    (3)` <meta http-equiv="X-UA-Compatible" content="ie=edge">`代表浏览器加载内核方式，用IE内核渲染
    (4)`meta http-equiv='expires' content='时间' `：【expires期限】，告诉浏览器到了某个时间就重新传输一次页面。
    (5)`<mata name="keywords" content="关键字">`代表该网页的关键字，用于搜索引擎抓取排名优化
    (6)`<mata name="description" content="网页描述">`代表该网页的文字描述，用于搜索引擎读取，用户也可在搜索引擎看到其针对于该页面的描述信息。
3. <title>标题</title>该标签中的内容将会显示在浏览器的标题栏
总结：html着重强调语义化，开发者应选用合适的元素， 使用合理的代码结构进行开发。这样不仅便于开发者阅读，也能使浏览器和搜索引擎更好地进行解析。
要注意的是，当无注释和内容为前提下，head标签、body标签、甚至html标签都可省略(omitted)
# html基本元素
我将制作页面所使用过的并且经常使用的标签进行下罗列，以便备查
### 1.常用元素

标签 | 用法 | 代码
----|------|--------
h1~h6 | 在需要写文章标题时使用  | <h2>仅次于大标题的标题</h2>
a | 多用于插入链接  | <a href="" targer="_blank" title="" >xxx</a>
div | 给页面划块 | <div class=""></div>
p | 段落 |<p>内容</p>
###### 1.a链接（anchor锚点），targer表示页面打开的方式，title写上后点击链接会看到展现文字。 如果href=#XXXX 代表锚点，XXXX就是别的元素的ID
###### 2.div(divde)多用来给页面分区块，使得结构严谨。一个页面基本分三部分进行划分，例如“页头(header)、内容区块(content)、页脚(footer)”，然后在针对每一块再次细分即可。

---

标签 | 用法 | 代码
----|------|--------
strong | 强调  | <p>特价只需<strong>500</strong>元</p>
em | 一般强调  | <p>今天写了<em>5</em>篇文章</p>
span | 无语义 | <p>打开一个<span>地址</span></p>
small | 语义为不重要的 |<small>内容</small>
kbd | 书写键盘按键 |<kbd>ctrl</kbd>+<kbd>c</kbd>
###### 1.strong语义化表示重要，表强调，会默认加粗（有的浏览器可能不会）
###### 2.span标签没有任何语义，只是用来圈起来，代表横向划分（divide span）
###### 3.em表示有点重要，次于strong
###### 4.small表示不重要的
###### 5.em表示语气重，strong表示地位重

---

标签 | 用法 | 代码
----|------|--------
img | 插入图片  | <p>特价只需<strong>500</strong>元</p>
b | 加粗  | <p>今天写了<em>5</em>篇文章</p>
ul | 无序列表 | 样式如下

``` javascript 
<ul>
  <li></li>
  <li></li>
</ul>
```
###### 1.<b>与<strong>虽然两者都会加粗（有的浏览器strong的默认样式不加粗），但是语义完全不同，<strong>表示强调，而<b>仅表示加粗。
###### 2.<img>的alt属性代表可选文字的展示，同时也利于搜索引擎优化
###### 3.无序列表（unsort orderd list）用于展现有顺序的列表

---

标签 | 用法 | 代码
----|------|--------
ol | 有序列表 | 样式如下
``` javascript 
<ol>
  <li></li>
  <li></li>
</ol>
```
###### 有序列表（order list）用于展现有顺序的列表

---

标签 | 用法 | 代码
----|------|--------
dl | 标题:内容 | 样式如下
``` javascript 
<dl>
  <dt></dt>
  <dd></dd>
</ol>
```
###### 描述列表，多用于展现标题对应内容的形式

---

标签 | 用法 | 代码
----|------|--------
iframe | 嵌入页面 | 样式如下
``` javascript 
<iframe src="XX.com" name="d" ></iframe>
<a href="ZZ.com" target="d" >SSS</a>
```
###### 该标签用于在当前页面嵌入一个页面，多与a标签合用。当我点击a链接，就会在iframe窗口中展示a链接

---

标签 | 用法 | 代码
----|------|--------
table | 展现表格 | 样式如下
``` javascript 
<table>
<thead>
<tr>
<th>姓名</th><th>性别</th><th>成绩</th>
</tr>
</thead>
<tbody>
<tr>
<td>小明</td><td>男</td><td>80</td>
</tr>
<tr>
<td>小花</td><td>女</td><td>90</td>
</tr>
</tbody>
<tfoot>
<tr>
<td>合计</td><td>2人</td><td>170</td>
</tr>
</tfoot>
</table>
```
###### <table>标签，用于展现一个表格,可省略thead tbody tfoot 会自动补全.


---
