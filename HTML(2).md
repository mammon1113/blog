### 补充元素
最近用到的一些标签
1.`<base>`标签，翻译过来是基于的意思，该标签的功能在于设置相对路径。
``` javascript
<head>
  <base href="http://mystation/web/">
  <base target="_blank" >
</head>
<body>
  <img src= "1.png">
</body>
```
上面的代码里，假设你的站点在web目录中，如果你不用该标签，那么引用 web目录中的一个图片只能采用`<img src= "xxx/web/1.gif" >`
但是用base设置后，就可以直接如上面的代码使用规定的默认地址。另外该标签放在`<head>`里面
2.`nav`元素，如页面中有导航条需要写，则要用的该标签，翻译过来是navigation，一般导航条的时候用`<nav></nav>
用到新的随时待更...
# 关于总结
## 常见的浏览器及其对应内核：
> 1.使用Trident的是internet explorer，国产的绝大部分浏览器。Trident是就是ie内核.
> 2.使用Gecko的是Mozilla Firefox，使用 Gecko 内核的浏览器也有不少，如 Netscape MozillaSuite/SeaMonkey 等.
> 3.使用Presto的是opera，这是目前公认网页浏览速度最快的浏览器内核.
> 4.使用WebKit的有苹果的safari，谷歌的chrome，还有国产的大部分双核浏览器其中一核就是WebKit.
## 关于行内元素与块元素
1.块元素：block-element，特点是不管内容有多少，自动换行，同时占满整行，块元素可以放文本行内元素或者其他块元素。在css里面可以设定默认样式为display:inline则变为行内元素，默认 display 为 block:div ul li h1 p 等默认样式为块元素。
2.行内元素：又叫内联元素，inline-element,特点是只占内容的宽度，默认不会换行。行内元素一般放置文本或者其他行内元素。在css里面设置display:block即为块元素。
另外，html标签是没有块级元素和内联元素的区别的，只有在css里面才会有。css可以变换块级元素和内联元素的样式的。html是不管样式的，也不该归html管，html的块元素和内联元素都只是css的默认样式而已。
##  空元素与替换元素
1.空元素：标签里面不能有内容（即「空元素」）例如:input、img、hr、br、mata、link等
2.可替换元素:可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。可替换元素展现不是由css控制的，这些元素是外观渲染独立于css的外部对象。简单地说就是一些元素自带宽和高，大多数就是可替换元素。例如:<img>、<input>、<textarea>、<select>、<object>
3.不可替换元素：html 的大多数元素是不可替换元素，即其内容直接表现给用户端（例如浏览器）例如：<p>段落的内容</p>
段落<p>是一个不可替换元素，文字“段落的内容”全被显示。