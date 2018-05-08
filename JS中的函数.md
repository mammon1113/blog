# 函数的声明
1.具名函数
```javascript
 function x(a,b){
     return a+b
 }
 x.name // 'x'   name为'x'
```
2.匿名函数
```javascript
var x
 x = function (a,b){
     return a+b
 }
 x.name // 'x'  name为'x'
```
3.具名函数赋值
```javascript
var x
 x = function y(a,b){ return a+b }
console.log(y) // undefined
 x.name // 'y'   name为'y'
```
4.window.Function
```javascript
 var f = new Function('x','y','return x+y')
 f.name //    "anonymous"
```
5.箭头函数
```javascript
var f = (a,b)=>{ return a+b } 
var sum = (x,y) => x+y  //表达式如果只有一句可以省略{}
var n2 = n => n*n  //参数如果只有一个可以省略()
```
总结：函数声明的5种方式中，1、2、5用的较多，箭头函数为新的声明方式，比较简洁。对于函数声明方式的不同name属性值，有几个特殊的需要特殊记忆。
# 函数的调用
介绍一下阮一峰说过的函数定义:''函数就是一段可以反复调用的代码块，函数还能接受输入的参数，不同的参数会返回不同的值。''
所以你可以声明一个函数，便能反复的调用这个函数来满足自己的需求。
```javcascript 
function 求三角形面积(h,w){
    var n = h*w
    var m = n/2
    return m   
}

求三角形面积(5,5) //  这是第一种调用方式
求三角形面积.call(undefined,5,5) //这是第二种调用方式
```
调用函数的时候最好使用call()方法来调用，这样可以理解到函数的本质。
这里面的call()方法可以执行对象的函数体。
```javcascript 
var f = {}
f.params = ['x','y']  //假设将参数存到params里。
f.fbody = 'console.log(1)' //假设将函数体存到fbody里。
f.call = function(){ 
   eval(f.body)
}     //  eval方法可以执行函数体
f.call()  // 1
```
如下图
![call()](http://upload-images.jianshu.io/upload_images/7921365-a9b53ba07ff9130e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# this与arguments
刚刚已经简单的介绍了.call()调用函数的方法，其中.call需要接受可选的几个参数，不论是多少个参数，简单（并不严谨）来说，第一个参数就是this，第二个之后的就是arguments。
比如```f.call(asThis, input1,input2)```
其中 asThis 会被当做 this，[input1,input2] 会被当做arguments。
```javascript
 f = function(){
    'use strict'  //严格模式
    console.log(this)
    console.log(arguments)
}
f.call(undefined,1,2)  
// undefined  
// [1,2]         
```
该示例中打印出来的arguments是一个伪数组，即该对象的__proto__所指向的共有函数并不是Array.prototype而是object.prototype。或者说该对象所指向的共有属性中无Array.prototype却以数组的形式显示出来的，即是伪数组。
这篇文章中重点并不探讨this的用法，但是js的this从根上来说并不如java那么重要，发明者最初的初衷只是为了js看起来像java而已。
写到这里可以初步下个结论
1.call的第一个参数可以被this得到
2.call的后面的参数可以被arguments得到。
# call stack
每进入一个函数之前会把这函数的位置记入到stack里面，每次return的时候就会回到stack上面的那个位置继续记入stack。
![调用堆栈](http://upload-images.jianshu.io/upload_images/7921365-21f574bd42a5a974.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![代码示意图](http://upload-images.jianshu.io/upload_images/7921365-f0dbacb9a2dd81b7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```javascript
var sum = function(n){
    if(n==1){
    return n
  }else{
   return n+sum.call(n-1)
  }
}
sum.call(5)   //15
sum.call(3)   //6
sum.call(20250)  // 205041375 
sum.call(30000) // 根据电脑和当前运行环境的不同，最大可调用的堆栈也不同。如果大于某个阈值，就会溢出导致报错（stack overflow）
```
# 函数的作用域
![作用域范围](http://upload-images.jianshu.io/upload_images/7921365-469cf9d8fa639e32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
从图中可以看出作用域的包裹范围。
![作用域树](http://upload-images.jianshu.io/upload_images/7921365-cc3c132faa82c2c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```javascript
var a = 1
function f1(){
    alert(a) // 是多少
    var a = 2
}
a   // 1         //外层作用域变量声明为1
f1.call()       // undefined 因为在作用域中var a会提升
a // 1          // 变量声明只在内部作用域有效
f1.call()      //undefined  同样的，变量相当于重新提升，a还是没定义值。
```

```javascript
var a = 1
function f1(){
    alert(a) // 是多少
    a = 2
}
a       // 1           外层`var a = 1`此时a为1
f1.call()    // 1   js代码是按顺序执行的，也会按顺序去找声明的变量，发现没有会去外层作用域中寻找。在内层函数作用域中，没有声明，外层的作用域声明了 a =1，所以此时a被赋值为1 
a           // 2   `f1.call()`此时已执行完毕，a被赋值为2（与上一例子不同的是，这里并未被重新声明）
f1.call()  // 2    此时a已经是被赋值为2了，所以输出值也是2
```

```javascript
var a = 1
function f1(){
    var a = 2
    f2.call()
}
function f2(){
    console.log(a) // 是多少   1
}
f1.call()             //     1
console.log(a)   //   1
```

```javascript
var liTags = document.querySelectorAll('li')
for(var i = 0; i<liTags.length; i++){
    liTags[i].onclick = function(){
        console.log(i) // 点击第3个 li 时，打印 2 还是打印 6？答案是6
    }
}
```
以上几个示例了解清楚后，作用域也就很清晰了。
# 闭包
```javascript
var a = 1
function(){
    console.log(a) //2
}
```
结论：如果一个函数，使用了它范围外的变量，那么（这个函数+这个变量）就叫做闭包。