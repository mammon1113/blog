# JS的起源
* 1991年李爵士发明了万维网和HTTP协议
* 1992年李爵士的同事发明了CSS
* 1994年李爵士创立了万维网联盟也就是W3C
* 1994年底网景发布了Netscape（Navigator）浏览器，该浏览器自带脚本，由Branden Eich（JS之父）发明。最初为Mocha （看起来像JAVA）。逐步改名为-->LiveScript-->JavaScript
* JS早于Unicode与UTF-8发布的，所以JS的编码不是完整的Unicode。所以发步的JavaScript编码有问题。
* 1996年微软发明IE浏览器，并仿照JS发明了JScript，目的是抢占市场。网景的浏览器被打败了，该浏览器随后开源（firefox），随后IE5.5版本JS可以发请求。不得不说的是网景公司在开源后变像欧洲计算机制造商协会（ECMA）申报规范标准，并叫ECMAScript
* 2004年Gmail网页上可以用JS做程序，从此JS被认为是真正的编程语言。自此开始便诞生了前端（Front-and）。直到2010年左右中国开始真正的有了前端这个职业。
* 在这个过程中，使用ECMAScript3开发时，程序员们发现JS有一定的缺陷，没有模块化以及内置函数过少等相关问题暴露出来，毕竟这是JS之父10天时间搞出来的。所以ECMA开始升级到ECMAScript5。其中4.0版本因为跨越太大（升级功能太多导致浏览器不能快速跟上脚步，也有说法是众位浏览器大佬有不和），5.0版本吸取了教训，放慢了升级脚步，但是升级的脚步放的过慢了。此时有一个叫做Rails社区发布了CoffceScript，集所长提前推出了一些当前版本所没有的功能（例如类、箭头函数等），ECMA后发现的确不错，就吸取了CoffceScript的功能发布了6.0版本。这回升级的功能正好适合当下的需求。JS其实是集大家之所长的语言。JS之父曾说也曾对此说过一句话‘‘JS原创之处并非优秀，优秀之处并非原创’’。堪称经典！
* JS现在每年一更，ES7更新了2个特性，ES810个左右的特性。所以学习JS要温故而知新，不断更新新知识来满足高效开发成为一名优秀的程序员。
---
下面进入正题
# JS有哪些数据类型
JS有7种数据类型
1.Number（数值）
2.String（字符串）
3.Boolean（布尔值）
4.Symbol（符号）
5.undifend
6.null
7.object（对象）
所以JS并不是一切皆对象。其中数组和function并不是数据类型，这两种都属于对象的一种
# JS的表示方法
### 1.Number
Number又分为很多类
 十进制表示法：1、1.1、1.23e2等
 二进制表示法：0B1==1、0B10==2，都已0B开头
 八进制表示法：011==9、以0开头，所以用来表示电话号码时，要用字符串的数据类型来表示。
 十六进制表示法：0x11==17,以0x开头。
### 2.String
 例如·'你好'  `"你好"` `''`(空字符串)  `' '`(空格字符串)。单双引号皆可，但是在写入的时候最好统一。
 将特殊字符书写为字符串时可以转义，`'\''`即为转义，在前面加反引号即可
 多行字符串的写法最好的办法就是用`+`号换行。别的方法或多或少都会有些问题。
### 3.boolean
 多用于条件的判断，true/false,大部分的值都为true
 &&是与运算（条件均为真才是真）、 || 或运算（条件有一个是真的就可判断为真）
### 4.null、undefined
 null类型的值就是null，表示空对象
 undefined类型的值就是undefined，空非对象
区别:
它们表示都没有值。
如果一个变量未被赋值，也就是没定义值，就为undefined。
如果有一个对象object，现在暂时不想给值，就可以给null
如果一个非对象，现在暂时不想给值，就可以不定义（undefined）
### object对象(复杂类型)
* 除去object外的类型都是简单类型或基本类型，对象是复杂类型，是由简单类型组成的。
``` var age = 18```
``` var name = Xxc ```
``` var gender = 'male'
等同于
``` javascript 
var person = {
  'age': 18,
 'name':  Xxc,
'gender': 'male'
''：'mammon'
}
```
* key永远相当于字符串，引号可加可不加,但是如果key的首个字符是数字，或者key里有空格，则必须加引号。
* 读取时有两种方式，例如```person['name']```、符合标识符的情况下可以使用```person.name```,如果是前者，必须在中括号中加引号。
* 对象里面是可以有对象的。
* key可以是空字符串，```person[''] //'mammon'```
``` javascript 
delete person['name']
person['name'] // undefined
  'name' in person // undefined
```
delete后无key无value
区别于person['name'] = undefined
这样的话把undefined赋值给'name'，但是'name'这个key依旧存在
* forin循环
遍历一个哈希表中的key常用到for...in
``` javascript 
var person = {'name':'liu','age':18}
for(var key in person) { // key只是个变量名，用任何变量名都可以
console.log(key) // 'name'   'age'
console.log(person[key]) // 'liu'  18 此处不能书写为person.key 因为.key等价于person['key']
}
``` 
需要注意的是遍历出的key或值具备随机性。

# 关于typeof
![image.png](http://upload-images.jianshu.io/upload_images/7921365-63f0990dcc9184d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
只有两种返回值是比较特殊的，一个是函数一个是null。数组返回的仍然是object
函数本身是object，但是返回值为function.null返回值为object. 这两个要单独记忆

