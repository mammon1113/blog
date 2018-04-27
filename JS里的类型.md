# 类型的转换
1.任何类型转字符串 (toString方法)
* 数字转字符串
```javascript
var n = 55
n.toString() // '55'
```
全局方法```String(n) // '55'```
* 布尔转字符串
```javascript
var n = true
n.toString() // 'true'
```
* null不能转，没有toString方法
* undefined不能读toString属性，所以不能转
![image.png](http://upload-images.jianshu.io/upload_images/7921365-8bdd424967d0d282.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* object转字符串
```javascript
var obj = {name:'liu'}
undefined
obj.toString() // "[object Object]"
```
![image.png](http://upload-images.jianshu.io/upload_images/7921365-8e0865a65dd3f175.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* 转字符串最简便的方法
```javascript
1 + ''   // '1'
true + '' // 'true'
var obj = {}
obj + ''  // '{object object}'
```
![image.png](http://upload-images.jianshu.io/upload_images/7921365-39ed9177dcda3f5b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

任何类型（包括null/undefined）+空字符串（' '）即可转换为字符串类型
由于加号只能加相同类型的东西，所以会尝试改变类型，优先会尝试改变为字符串，所以1 + '1' = '11'
2.任何类型转boolean
* 可以使用 boolean()，括号中为值
![boolean的一些例子](http://upload-images.jianshu.io/upload_images/7921365-a61976544d7614e0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
只有（空字符串、null、undefined、0、NaN ）这五个falsy值转化为布尔值是false
* 任何类型取反两次则转化为布尔
```!! undefined // false```
3.任何类型转number
* Number(x) 用 Number('2') // 1
* parseInt(x, 10)
* parseInt('2',10) // 2  
* 小数的情况可以用 parseFloat('1.23')  // 1.23
* 任何类型 - 0 就可以转化为 Number 
  ```'23' - 0  // 23 ```
* 任何类型取正就可以转化为Number 
``` +'23'  // 23 ```
![parseInt的一些特殊例子](http://upload-images.jianshu.io/upload_images/7921365-cdb24d5f27b614ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
需要读取的进制要写明，这是JS的一个小BUG。parseInt会尽量读取数字。
# 内存图
先说说内存。我们知道每台计算机都有内存。一块内存插在机器上，机器开机后给浏览器分配一定的内存，浏览器给不同页面继续分配内存，每个页面又会给js分配内存。这就是分配内存的大体描述。
这里主要考虑的是js块面。
大概会分配成两个大区块，一边为代码区（比如 var a ），一边为数据区('1'  {} )，代码区与数据区的内容将会产生关联。
![内存区块](http://upload-images.jianshu.io/upload_images/7921365-c78f9e1f3e7314b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
我将重点研究的是数据区

* 声明变量后第一步都要进行变量提升
* 简单类型的值直接存储在栈内存中
* 数字用64位浮点数表示在栈内存中（凑够64位），字符是16位
* 复杂类型的值存储在堆内存中，堆内存有一个随机地址，这个随机地址将存储在栈内存中。
![数据区](http://upload-images.jianshu.io/upload_images/7921365-8f150ff9545eae60.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 如果 b = a，那么栈内存中a将覆盖到b上面。
* 如果 o2 = o ，那么原本存储栈内存的o2地址将变成o,共同指向堆内存的64位置,对其引用。要注意的是并不是o对应的对象复制给o2,而是改变了地址指向。
内存图很实际也很有用处。列几道题目来加深印象
```javascript
var a = 1
var b = a
b = 2
请问 a 显示是几？  
```
通过画内存图可以发现，b赋值为2并未影响到a，所以a仍然是1
![内存图1](http://upload-images.jianshu.io/upload_images/7921365-f680d8e41a708471.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
var a = {name: 'a'}
var b = a
b = {name: 'b'}
请问现在 a.name 是多少？
```
通过画内存图可以发现，a为对象，b同样指向了a这个对象，之后b重新被赋值了一个对象，并不改变a只是给b划出了另外一块堆内存用于存储数据。所以a.name = 'a'
![内存图2](http://upload-images.jianshu.io/upload_images/7921365-890d1f343b8d52cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
var a = {name: 'a'}
var b = a
b.name = 'b'
请问现在 a.name 是多少？
```
a与b同时指向对象{name: 'a'}，b.name = 'b'，导致共同指向的对象改变。a.name = b''
![内存3](http://upload-images.jianshu.io/upload_images/7921365-fa0e6f026e9b4d8c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```javascript
var a = {name: 'a'}
var b = a
b = null
请问现在 a 是什么？
```
a是一个对象，b=a，共同指向一个对象，b被赋值为简单类型null，栈内存中的b被重新赋值，并不影响栈内存的a所指向的堆内存的地址。所以，a = {name: 'a'}
![内存图4](http://upload-images.jianshu.io/upload_images/7921365-dd85aa887bb547fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
var a = {n: 1}
var b = a
a.x = a = {n: 2}
alert(a.x) ;
alert(b.x);
请问弹出值是什么？
```
说一下对应的逻辑，`a.x= a；a={n:2};可以看成先后两句语句，再结合内存图就一目了然了。（1）假设a为地址34，对应的堆内存数据就是{n: 1}，此时b = a，说明两者都被地址34所引用。（2）当a.x= a；时，地址34所对应的堆内存中新增属性x值为a 。（3）a = {n: 2}时，a的地址变更假设为54，对应的堆内存数据为{n: 2}。（4）此时(2)中x的值a变更为地址54。
结论：地址a已变更为54，所对应的堆内存数据中并无x这个key，所以alert(a.x)为undefined。地址b此时对应的是34地址，堆内存中有一个key为x值为地址54的对象哈希，所以alert(b.x) 为 对象
![image.png](http://upload-images.jianshu.io/upload_images/7921365-872090df9e28d470.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 垃圾回收
* 通过内存图，我们得知声明的变量对应的数据是存在引用关系的，如果数据未被引用就将形成垃圾堆砌在内存中，这是肯定不被接受的。所以如果一个对象没有被引用就将被回收。
![image.png](http://upload-images.jianshu.io/upload_images/7921365-583b6fd0cee2ba18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 内存泄漏
因为浏览器的某种bug（IE6）导致一些事件不能随单页面关闭而被回收，造成垃圾堆砌。
# 深拷贝与浅拷贝
* 简单来说赋值后并不影响其他变量是深拷贝
* 对于任意基本类型的简单赋值语句而言，都是深拷贝
![深拷贝](http://upload-images.jianshu.io/upload_images/7921365-bfacd2965258cfa3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 通过赋值会影响其他变量的是浅拷贝
* 对于复杂类型而言有意义
![浅拷贝](http://upload-images.jianshu.io/upload_images/7921365-c3e09876aad1fd03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
