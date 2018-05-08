# Array的基本用法
1. window.Array 全局对象（也是函数）
2. var a = Array(3) // {length:3} 每个值都是undefined
但是值并没有存上，只存了一个`length:3`。但是生成的数组依旧有对应的方法，例如push。主要是因为`__proto__`指向了Array的共有属性。
![内存图](http://upload-images.jianshu.io/upload_images/7921365-6903015714679f92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3.var a =  Array(3,3) // [3,3] 
所以，当一个参数的时候，第一个参数是长度。当大于1个参数的时候，第一参数是第一项。
![JS具有不一致性](http://upload-images.jianshu.io/upload_images/7921365-953e84cbd4db3bb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* new Array(3) 跟不加 new 一样的效果
* new Array(3,3,) 跟不加 new 一样的效果
结论：对于Object（包含Array/function）来说加不加 new 结果一样。但是对于简单类型来说，加new才能生成对象。
window.Function 全局对象（也是函数）
`Function('x','y','return x+y')`
`new Function('x','y','return x+y')`
结论：加不加 new 结果依旧一样
# 函数的声明方法
1.具名函数
```javascript
function x(a,b){
    return a+b
}
```
简单地说，function是声明，地位等同于var，相当于声明一个x的函数，参数为a与b，大括号里面的是这个函数具体的运算内容。
2.匿名函数
```javascript
var f = function (a,b){
    return a+b
}
```
其实区别并不是很大，但是具名函数在内存中是一步到位的，声明函数。在匿名函数里面，内存是先声明f，在开辟一个区域用来存放一个函数，在赋值给已经声明过的f。
```javascript
var f 
f= function (a,b){
    return a+b
}
```
今天不讨论函数，重点讨论数组。
# 什么是数组
数组的本质究竟是什么呢？
直接下一个定义来确定数组
人类理解：数组就是数据的有序集合
JS理解：数据就是原型链中有 Array.prototype 的对象
对于数组来说，当声明一个对象为数组的时候，这个对象的`__proto__`指向的共有属性是Array的共有属性，也就是`Array.prototype`这个对象。所以当你声明一个数组的时候，你可以调用数组中的多个API，例如`push`等等。但是如果你声明一个Object对象的时候，这个对象的`__proto__`所指向的共用属性并不是`Array.prototype`，而是根共用属性`Object.prototype`，Object并不指向`Array.prototype`这个对象，所以不能调用`push`等方法。下图描绘的很清楚。
![数组内存图](http://upload-images.jianshu.io/upload_images/7921365-495fdfd9f1b0cf8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```javascript
var a ={
 '0':1,
 '1':2,
 '2':3,
 'length':3
}
a.xxx= 'ooo'
console.log(a) 
```
将会打印出结果
```javascript
0:1
1:2
2:3
length:3
xxx:"ooo"
__proto__:Object
```
```javascript
0:1
1:2
2:3
length:3
xxx:"ooo"
__proto__:Object
```
我们遍历这个对象
```javascript
for(let i=0;i<a.length;i++){
  console.log(i)
}
// 0
// 1
// 2
```
这回用for...in遍历
```javascript
for(var key in a){
 console.log(key)
}
// 0
// 1
// 2
// length
// xxx
```
可以得到5个Key。
结论：所以，可以发现，数组和对象并没有什么本质区别，只是因为我们遍历的方式不同（for循环故意不访问非数组的下标），导致结果不一样。只不过在访问a的时候是按照顺序访问的所以才感觉是数组，实际上还是对象，只不过它是一个拥有特殊原型链的对象。
# 伪数组
结论：原型链中没有 Array.prototype
这样的对象就是伪数组。
# 数组的API
## 1.forEach
这个API可以遍历数组后取得value与key
```javascript
var a = ['a','b','c','d']
a.forEach( function(value,key){
    console.log(value)
    console.log(key)
} )
```
我对这个API的个人理解就好像是，执行forEach方法后，会遍历数组，传的参数为函数（函数本身没有对应值），当运行的那一刻，此时forEach方法中带的参数会等同自己传的那个函数（目的是得到遍历的值与Key），系统会传递给我对应的( function(value,key)的值（此时函数拿到对应的值）。好像很难解释，但是看图会理解的更清晰。
![推导](http://upload-images.jianshu.io/upload_images/7921365-e3550278241e21c7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

forEach可以通过this获取到数组a
![forEach原理](http://upload-images.jianshu.io/upload_images/7921365-d107c6eed52d9eac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 2. sort()
sort()可以排序数组，通过快排算法排列顺序。该API接受一个函数，必须接受2个参数。
```javascript
var a = [18,20,7,3,1]
a.sort( function(x,y){return x-y}) //[1,3,7,18,20]
a.sort( function(x,y){return y-x}) //[20,18,7,3,1]
```
x-y为负值是从小到大，用的时候一试就知晓了。
![sort()](http://upload-images.jianshu.io/upload_images/7921365-4932ed8aaea36e2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 3. join()
该API可以使数组中添加需要的内容并使其变为字符串
```javascript
var a = ['a','b','c']
a.join(',') // "a,b,c"
```
![ join()](http://upload-images.jianshu.io/upload_images/7921365-32fa04c9b45aab9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
之前谈到了 数字+''会转为字符串类型
数组+空字符串也可以转变为字符串类型，等同于join()方法
## 4. concat()
通过数组中的concat()方法可以将两个数组值连接起来，可生成一个新数组。不改变原数组的值。
```javascript
var a = [1,2,3,4]
var b = [5,6,7,8]
var c = a.concat(b)
console.log(c) // [1,2,3,4,5,6,7,8] 
console.log(a) // [1,2,3,4]
console.log(b) // [5,6,7,8]
```
![concat()](http://upload-images.jianshu.io/upload_images/7921365-833fca70c53a8ad7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
需要注意的是，concat()可以连接一个空数组
```javascript
var a = [1,2,3,4]
var b =  a.concat([])   // b为一个新数组
console.log(b) // [1,2,3,4]
a === b // false   
// 在内存中新生成一个数组，b所对应的并不是原数组a的引用，改变a的值将不影响b
```
![可以结合内存图进行对比](http://upload-images.jianshu.io/upload_images/7921365-110fe24aea344765.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 5. map()
与forEach类似，可以遍历数组，但是map的返回值可以用来计算。
```javascript
var a = [1,2,3,4]
// undefined
a.map( function(x,y){return x*2})
// [2, 4, 6, 8]
a
// [1, 2, 3, 4]
```
## 6. filter()
这个方法很像map，同样也是遍历后取值，但是语法是用来判断条件的，用于筛选符合条件的值进行输出。
![filter基本语法](http://upload-images.jianshu.io/upload_images/7921365-04d25e6ec608f8d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
还有几种筛选方法
```javascript
var a = [1,2,3,4]
// undefined
a.filter( function(x,y){return x%2 === 0})   // 当value的值的余数是0时输出
// [2, 4,]
```
## 6. reduce()
这个API用于求和，直接上例子
```javascript
var a = [1,2]
a.reduce( function(sum,n){return sum+n},0) // 3 
// 这个函数必须接受2个参数。0代表sum初始值，n代表数组中的值。
a.reduce( function(sum,n){return sum},0) // 0 
// sum+第一次n 得到求和的值存储到sum中，进行下一次sum+n(这里的n代表数组中的值，每一次的n的取值就是数组里面的每一项的值)
a.reduce( function(sum,n){return n},0) // 2
// 可以看到此时n的最后一次被赋值为2
// sum = sum+n
```
![原理图](http://upload-images.jianshu.io/upload_images/7921365-e3a974b89143fba0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![原理图2](http://upload-images.jianshu.io/upload_images/7921365-0a9b701c9a145191.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 7.用reduce表示map或filter
```javascript
var a = [1,2,3]
a.reduce(function(arr,n){  // arr此时初始值为空数组
      arr.push(n*2)  // 将每一项成员*2后push给空数组
      return arr   //    [2,4,6] 输出这个数组
},[])
```
```javascript
var a = [1,2,3]
a.reduce(function(arr,n){  // arr此时初始值为空数组
      if(n % 2 === 0){  // 如果n的余数为0
         arr.push(n)     //  将n的值push给arr这个空数组里
      }
      return arr   //    [2]
},[])  
```
![代码示意图](http://upload-images.jianshu.io/upload_images/7921365-556109aca9d6f854.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
