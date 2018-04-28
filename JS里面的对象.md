# 全局对象
ECMAScript 规定全局对象叫做 global，但是浏览器把 window 作为全局对象（浏览器先存在的）
全局对象分为两种
* ECMAScript规定的
1.global.parseInt
2.global.parseFloat
3.global.Number
4.global.String
5.global.Boolean
6.global.Object
.
.
.

* 浏览器私有的
1.alert（弹框）
2.prompt(用户填写)
3.comfirm(确认)
4.console.log(开发者)
5.console.dir
6.window.document
7.window.document.createElement
8.window.document.getElementById
document的对象是由w3c规定的
.
.
.

# 全局函数
1.	Number
var n = new Number(1) 创建一个 Number 对象
1与 new Number(1) 的区别是什么？看内存图
从图中可以看到，n.toString()是不可行的，因为没有这个属性。但是为什么当使用n.toString()的时候是可以运行的呢。就是因为JS在知道你要n.toString()的时候生成一个临时的对象，假设为temp，temp = new Number(1),temp里面有很多方法比如toString()。最终就相当于temp.toString()。temp用完就没有用了。这是一个临时的转换。
![内存图](http://upload-images.jianshu.io/upload_images/7921365-0123ae506bbbbaa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.	String
var s = new String('hello') 创建一个 String 对象
'hello' 与 new String('hello') 的区别是什么？和Number一样
介绍一下String的相关属性
![image.png](http://upload-images.jianshu.io/upload_images/7921365-c00e4da82d8fe427.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](http://upload-images.jianshu.io/upload_images/7921365-5d728d2740039148.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](http://upload-images.jianshu.io/upload_images/7921365-a4ea40c8d56271ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* toString()的一些常用API
``` '     username    '.trim()    //"username" ```   可以去除多余空格

```javascript
var s1 = 'hello'
var s2 = 'world'
s1.concat(s2)  // "helloworld"  
s1 // ''hello''
s2 // ''world''
concat可使两个字符串相连接
```
```javascript
var s1 = 'hello'
s1.slice(0,1)
// "h"
s1.slice(0,3)
// "hel"
slice翻译过来是切片的意思，简单的来理解就是第一个参数表示从第几个开始，0就是从头开始，3代表切3个字符串，结果是"hel"。
```
```javascript
var s1 =  'hello'
s1.replace('e','o')
// "hollo"
s1
// "hello"
替换想要替换的字符串，但是并不改变原变量
```
3.	Boolean

var b = new Boolean(true) 创建一个 Boolean 对象
true 与 new Boolean(true) 的区别是什么？同上。

4.	Object

```javascript
var o1 = {}
var o2 = new Object()
```
o1 和 o2 看起来没区别。
虽然表示的都是空对象，但是并不是一回事，地址不同，所以这是两个不同的对象。

# 公用属性
所有对象都有 toString 和 valueOf 属性，那么我们是否有必要给每个对象一个 toString 和 valueOf 呢？
很明显不需要。

1.object的公用属性，通过简易内存图可以看到每一个对象都有一个```__proto__```，```__proto__```这个地址存储着object的公用属性，比如toString和 valueOf ，所有的object数据类型，都有一个```__proto__```指向这个公用属性方便调用里面的方法。
```javascript
var o1 ={}
var o2 = {}
o1.__proto__ === o2.__proto__
//  true
```
![object公用属性](http://upload-images.jianshu.io/upload_images/7921365-f9bfae2adf75cb3f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.toString(16)等方法，是属于Number的公用属性，当需要用的时候，一样会有一个``` __proto__ ```指向这些公用属性，同时指向``` __proto__ ```里面还有一个``` __proto__ ```，将会指向Object的公用属性。方便你调用valueOf等方法。要注意的是Object和Number的toString是不同的，Number的toString()方法可以输出16位的。
![Number的公用属性](http://upload-images.jianshu.io/upload_images/7921365-705028a265fa8ee2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![Number的公用属性](http://upload-images.jianshu.io/upload_images/7921365-3790f3cd554a5872.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
---------------------------------------------------------------------------------
![总结图](http://upload-images.jianshu.io/upload_images/7921365-5cacb412fdf359ec.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
总结：JS 的做法是把 toString 和 valueOf 放在一个对象里（暂且叫做公用属性组成的对象）然后让每一个对象的``` __proto__ ```存储这个「公用属性组成的对象」的地址。Object的公有属性是所有对象的公有属性。
```javascript
var s1 = new Number()
s1.__proto__ === Number.prototype
true
// true
``
可以推断出
```javascript`
var s1 = new Number()
s1.__proto__ === Number.prototype
 //    true
var w1 = new Boolean()
w1.__proto__ === Boolean.prototype
//     true
var o1 = {}
o1.__proto__ === Object.prototype
 //    true
w1.__proto__.__proto__ === Object.prototype
//     true
Number.prototype.__proto__ === Object.prototype
//     true
```
公有属性之间的关系
![总结1](http://upload-images.jianshu.io/upload_images/7921365-4f24c32e48932988.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
重点：
var 对象 = new 函数()
对象.__proto__ === 函数.prototype
![总结2](http://upload-images.jianshu.io/upload_images/7921365-09d66e87a84aea42.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
