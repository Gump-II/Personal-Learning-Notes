---
layout: post
title: 前端面试问题及详解-JavaScript
tags: [前端后台]
---

# JavaScript部分
 
## 1.谈谈闭包

**使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。**

**三特性**
- 1.函数内嵌套函数；
- 2.函数内部可以引用外部的参数和变量；
- 3.参数和变量不会被垃圾回收机制回收；

```
//li节点的onclick事件都能正确的弹出当前被点击的li索引
<ul id="testUL">
<li> index = 0</li>
<li> index = 1</li>
<li> index = 2</li>
<li> index = 3</li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName("li");
    for(i = 0;i<nodes.length;i+= 1){
        nodes[i].onclick = (function(i){
                    return function() {
                        console.log(i);
                    } //不用闭包的话，值每次都是4
                })(i);
    }
</script>

```
- 执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在.
- 使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源
- 因为say667()的内部函数的执行需要依赖say667()中的变量
- 这是对闭包作用的非常直白的描述
```
function say667() {
    // Local variable that ends up within closure
    var num = 666;
    var sayAlert = function() {
        alert(num);
    }
    num++;
    return sayAlert;
}

    var sayAlert = say667();
    sayAlert()//执行结果应该弹出的667
```
## 2.谈谈cookie

**2.1 cookie虽然在持久保存客户端数据提供了方便，分担了服务器存储的负担，但还是有很多局限性的。**
- 1.特定域名下IE6只能生成20个cookie；
- 2.每个cookie大小限制在`4K`

**2.2 使用cookie方法**

- 1.控制`cookie`和`session`对象的大小；
- 2.加密技术，减少`cookie`被破解的可能性；
- 3.不在cookie中存放私密信息；
- 4.控制cookie的声明周期，让有有效时间；
- 5.为了防止重复提交表单，在服务器上有计数器；

## 3.谈谈浏览器本地存储

**3.1 js提供了`sessionStorage`和`globalStorage`。在HTML5中的web storage提供了`localStorage`来取代`globalStorage`**

- 1.`sessionStorage`用于本地存储数据,同一个页面中才能访问随之销毁。因此不是一种持久化的本地存储，仅仅是会话级别的存储。
- 2.`localStorage`用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

**3.2 web storage和cookie的区别**

- 1.`cookie`大小受限，`web storage`更大容量存储；
- 2.每当请求一个新页面，`cookie`都会发送过去，浪费了带宽；
- 3.`cookie`不可跨域调用；
- 4.`cookie`的作用是与服务器交互，作为`HTTP`一部分，而`web storage`为本地存储而生；

**3.3 session和cookie的区别**

- 1.`cookie`放在客户端浏览器，`session`放在服务器上；
- 2.`cookie`安全性没有`session`高；
- 3.`session`会保留在服务器一段时间，访问增多，占用服务器性能，则合理使用`cookie`；
- 4.登陆重信息放在`session`,其它信息可放在`cookie`;

## 4.请描述一下 cookies，sessionStorage 和 localStorage 的区别？

- 1.cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。
- 2.cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。
- 3.sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
- 
**存储大小：**
- 1.cookie数据大小不能超过4k。
- 2.sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

**有期时间：**
- 1.localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
- 2.sessionStorage  数据在当前浏览器窗口关闭后自动删除。
- 3.cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

## 5.数据类型

- 1.逻辑对象无初始值或者其值为 0、-0、null、""、false、undefined 或者 NaN，其对象的值为 false
- 2.其他1：regExp正则，test()查找字符串，exec()返回字符串，compile()改变regExp中的匹配参数。
- 3.其他2：window表示浏览器窗口，screen表示屏幕。
- 4.其他3：警告alert();确认框confirm();提示框prompt()

## 6.介绍js的基本数据类型。

- 1.Undefined、Null、Boolean、Number、String、
- 2.ECMAScript 2015 新增:Symbol(创建后独一无二且不可变的数据类型 )

## 7.介绍js有哪些内置对象？

- Object 是 JavaScript 中所有对象的父对象
- 数据封装类对象：Object、Array、Boolean、Number 和 String
- 其他对象：Function、Arguments、Math、Date、RegExp、Error

参考：[http://www.ibm.com/developerworks/cn/web/wa-objectsinjs-v1b/index.html](http://www.ibm.com/developerworks/cn/web/wa-objectsinjs-v1b/index.html)

## 8.说几条写JavaScript的基本规范？

- 1.不要在同一行声明多个变量。
- 2.请使用 ===/!==来比较true/false或者数值
- 3.使用对象字面量替代new Array这种形式
- 4.不要使用全局函数。
- 5.Switch语句必须带有default分支
- 6.函数不应该有时候有返回值，有时候没有返回值。
- 7.For循环必须使用大括号
- 8.If语句必须使用大括号
- 9.for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染。

## 9.JavaScript原型，原型链 ? 有什么特点？

**每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。**

- 关系：instance.constructor.prototype = instance.__proto__

**特点：**
- JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。
- 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
```
Func.prototype.name = "Sean";
Func.prototype.getInfo = function() {
    return this.name;
}
var person = new Func();//现在可以参考var person = Object.create(oldObject);
console.log(person.getInfo());//它拥有了Func的属性和方法
//"Sean"
console.log(Func.prototype);
// Func { name="Sean", getInfo=function()}
```
## 10.JavaScript有几种类型的值？，你能画一下他们的内存图吗？

- 1.栈：原始数据类型（Undefined，Null，Boolean，Number、String）
- 2.堆：引用数据类型（对象、数组和函数）

**两种类型的区别是：存储位置不同**
	
- 1.原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
- 2.引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体

![Stated Clearly Image](http://www.w3school.com.cn/i/ct_js_value.gif)

## 11.如何将字符串转化为数字，例如'12.3b'?

* parseFloat('12.3b');
* 正则表达式'12.3b'.match(/(\d)+(\.)?(\d)+/g)[0] * 1, 但是这个不太靠谱，提供一种思路而已。

## 12.如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』?

```
function commafy(num){
    return num && num
        .toString()
        .replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
            return $2 + ',';
        });
}
```
## 13.如何实现数组的随机排序？	
**方法一：**

```
var arr = [1,2,3,4,5,6,7,8,9,10];
function randSort1(arr){
    for(var i = 0,len = arr.length;i < len; i++ ){
        var rand = parseInt(Math.random()*len);
        var temp = arr[rand];
        arr[rand] = arr[i];
        arr[i] = temp;
    }
    return arr;
}
console.log(randSort1(arr));
```

**方法二：**

```
var arr = [1,2,3,4,5,6,7,8,9,10];
function randSort2(arr){
    var mixedArray = [];
    while(arr.length > 0){
        var randomIndex = parseInt(Math.random()*arr.length);
        mixedArray.push(arr[randomIndex]);
        arr.splice(randomIndex, 1);
    }
    return mixedArray;
}
console.log(randSort2(arr));
```

**方法三：**

```
var arr = [1,2,3,4,5,6,7,8,9,10];
arr.sort(function(){
    return Math.random() - 0.5;
})
console.log(arr);
```

## 14.Javascript如何实现继承？

- 1、构造继承
- 2、原型继承
- 3、实例继承
- 4、拷贝继承

**原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。**
```
function Parent(){
    this.name = 'wang';
}

function Child(){
    this.age = 28;
}
Child.prototype = new Parent();//继承了Parent，通过原型

var demo = new Child();
alert(demo.age);
alert(demo.name);//得到被继承的属性
```

## 15.JavaScript继承的几种实现方式？
**参考：**
- 构造函数的继承[http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)
- 非构造函数的继承[http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)


## 16.javascript创建对象的几种方式？

**javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。**

**1、对象字面量的方式**

```
person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};
```

**2、用function来模拟无参的构造函数**

```
function Person(){}
    var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class
    person.name="Mark";
    person.age="25";
    person.work=function(){
    alert(person.name+" hello...");
}
person.work();
```
**3、用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）**

```
function Pet(name,age,hobby){
    this.name=name;//this作用域：当前对象
    this.age=age;
    this.hobby=hobby;
    this.eat=function(){
        alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
    }
}
var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
maidou.eat();//调用eat方法
```

**4、用工厂方式来创建（内置对象）**

```
var wcDog =new Object();
wcDog.name="旺财";
wcDog.age=3;
wcDog.work=function(){
alert("我是"+wcDog.name+",汪汪汪......");
}
wcDog.work();
```

**5、用原型方式来创建**

```
function Dog(){

}
Dog.prototype.name="旺财";
Dog.prototype.eat=function(){
alert(this.name+"是个吃货");
}
var wangcai =new Dog();
wangcai.eat();

```

**6、用混合方式来创建**

```
function Car(name,price){
    this.name=name;
    this.price=price;
}
Car.prototype.sell=function(){
    alert("我是"+this.name+"，我现在卖"+this.price+"万元");
}
var camry =new Car("凯美瑞",27);
camry.sell();
```
## 17.Javascript作用链域?

- 全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。
- 当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，至全局函数，这种组织形式就是作用域链。

## 18.eval是做什么的？

- 它的功能是把对应的字符串解析成JS代码并运行；
- 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。
- 由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval('('+ str +')');

## 19.什么是window对象? 什么是document对象?

- window对象是指浏览器打开的窗口。
- document对象是Documentd对象（HTML 文档对象）的一个只读引用，window对象的一个属性。

## 20.null，undefined 的区别？

- 1.null 表示一个对象是“没有值”的值，也就是值为“空”；
- 2.undefined 	表示一个变量声明了没有初始化(赋值)；
- 3.undefined不是一个有效的JSON，而null是；
- 4.undefined的类型(typeof)是undefined；
- 5.null的类型(typeof)是object；
- 6.Javascript将未赋值的变量默认值设为undefined；
- 7.Javascript从来不会将变量设为null。它是用来让程序员表明某个用var声明的变量时没有值的。

```
typeof undefined
    //"undefined"
    undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined；
    例如变量被声明了，但没有赋值时，就等于undefined

typeof null
    //"object"
    null : 是一个对象(空对象, 没有任何属性和方法)；
    例如作为函数的参数，表示该函数的参数不是对象；

注意：
    在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined
    null == undefined // true
    null === undefined // false

再来一个例子：

    null
    Q：有张三这个人么？
    A：有！
    Q：张三有房子么？
    A：没有！

    undefined
    Q：有张三这个人么？
    A：有！
    Q: 张三有多少岁？
    A: 不知道（没有被告诉）
```

## 21.["1", "2", "3"].map(parseInt) 答案是多少？

- parseInt() 函数能解析一个字符串，并返回一个整数，需要两个参数 (val, radix)，
- 其中 radix 表示要解析的数字的基数。【该值介于 2 ~ 36 之间，并且字符串中的数字不能大于radix才能正确返回数字结果值】;
- 但此处 map 传了 3 个 (element, index, array),我们重写parseInt函数测试一下是否符合上面的规则。

```
function parseInt(str, radix) {
    return str+'-'+radix;
};
var a=["1", "2", "3"];
a.map(parseInt);  // ["1-0", "2-1", "3-2"] 不能大于radix
```
- 因为二进制里面，没有数字3,导致出现超范围的radix赋值和不合法的进制解析，才会返回NaN
- 所以["1", "2", "3"].map(parseInt) 答案也就是：[1, NaN, NaN]

详细解析：[http://blog.csdn.net/justjavac/article/details/19473199](http://blog.csdn.net/justjavac/article/details/19473199)

## 22.事件是？IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

- 1.我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
- 2.事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
- 3.ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）

**参考阅读：undefined与null的区别[http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)**


## 23.javascript 代码中的"use strict";是什么意思 ? 使用它区别是什么？

**use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行**

- 使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
- 默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
- 全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
- 消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;

- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript标准化做铺垫。


## 24.如何判断一个对象是否属于某个类？

**使用instanceof （待完善）**

```
if(a instanceof Person){
    alert('yes');
}
```
## 25.new操作符具体干了什么呢?

- 1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
- 2、属性和方法被加入到 this 引用的对象中。
- 3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。
```
var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
```
## 26.Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？

   **hasOwnProperty**

    - javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。

    **使用方法：**

    - object.hasOwnProperty(proName)
    - 其中参数object是必选项。一个对象的实例。 
    - proName是必选项。一个属性名称的字符串值。

    如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。

## 27.js延迟加载的方式有哪些？

defer和async、动态创建DOM方式（用得最多）、按需异步载入js


## 28.Ajax 是什么? 如何创建一个Ajax？

ajax的全称：`Asynchronous Javascript And XML`。
异步传输+js+xml。
所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。

- (1)创建XMLHttpRequest对象,也就是创建一个异步调用对象
- (2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
- (3)设置响应HTTP请求状态变化的函数
- (4)发送HTTP请求
- (5)获取异步调用返回的数据
- (6)使用JavaScript和DOM实现局部刷新

## 29.Ajax 解决浏览器缓存问题？

- 1、在ajax发送请求前加上 anyAjaxObj.setRequestHeader("If-Modified-Since","0")。
- 2、在ajax发送请求前加上 anyAjaxObj.setRequestHeader("Cache-Control","no-cache")。
- 3、在URL后面加上一个随机数： "fresh=" + Math.random();。
- 4、在URL后面加上时间戳："nowtime=" + new Date().getTime();。
- 5、如果是使用jQuery，直接这样就可以了 $.ajaxSetup({cache:false})。这样页面的所有ajax都会执行这条语句就是不需要保存缓存记录。

## 30.同步和异步的区别?

- 1.同步的概念应该是来自于OS中关于同步的概念:不同进程为协同完成某项工作而在先后次序上调整(通过阻塞,唤醒等方式).同步强调的是顺序性.谁先谁后.异步则不存在这种顺序性.
- 2.同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。
- 3.异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。


## 31.异步加载JS的方式有哪些？

- (1) defer，只支持IE
- (2) async：
- (3) 创建script，插入到DOM中，加载完毕后callBack

## 32.documen.write和 innerHTML的区别

- 1.document.write只能重绘整个页面
- 2.innerHTML可以重绘页面的一部分

## 33.DOM操作——怎样添加、移除、移动、复制、创建和查找节点?

- （1）创建新节点

>   -  createDocumentFragment()    //创建一个DOM片段
>   - createElement()   //创建一个具体的元素
>   - createTextNode()   //创建一个文本节点

- （2）添加、移除、替换、插入
 
>  -  appendChild()
>  -  removeChild()
>  -  replaceChild()
>  -  insertBefore() //在已有的子节点前插入一个新的子节点

- （3）查找

>  -  getElementsByTagName()    //通过标签名称
>  -  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
>  -  getElementById()    //通过元素Id，唯一性

## 34..call() 和 .apply() 的区别？


- 例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);

**注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。**
```
function add(a,b)
{
    alert(a+b);
}

function sub(a,b)
{
    alert(a-b);
}

add.call(sub,3,1);
```
## 35.jquery.extend 与 jquery.fn.extend的区别？

* jquery.extend 为jquery类添加类方法，可以理解为添加静态方法
* jquery.fn.extend:源码中jquery.fn = jquery.prototype，所以对jquery.fn的扩展，就是为jquery类添加成员函数
* 使用：
jquery.extend扩展，需要通过jquery类来调用，而jquery.fn.extend扩展，所有jquery实例都可以直接调用。

## 36.Jquery与jQuery UI 有啥区别？

*  jQuery是一个js库，主要提供的功能是选择器，属性修改和事件绑定等等。
* jQuery UI则是在jQuery的基础上，利用jQuery的扩展性，设计的插件。 提供了一些常用的界面元素，诸如对话框、拖动行为、改变大小行为等等

## 37.那些操作会造成内存泄漏？

- 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
- 垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

- setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
- 闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

## 38.JQuery一个对象可以同时绑定多个事件，这是如何实现的？

* 多个事件同一个函数：

> $("div").on("click mouseover", function(){});

* 多个事件不同函数

```
$("div").on({
    click: function(){},
    mouseover: function(){}
});
```
## 39.Webpack热更新实现原理?

- 1.Webpack编译期，为需要热更新的 entry 注入热更新代码(EventSource通信)
- 2.页面首次打开后，服务端与客户端通过 EventSource 建立通信渠道，把下一次的 hash 返回前端
- 3.客户端获取到hash，这个hash将作为下一次请求服务端 hot-update.js 和 hot-update.json的hash
- 4.修改页面代码后，Webpack 监听到文件修改后，开始编译，编译完成后，发送 build 消息给客户端
- 5.客户端获取到hash，成功后客户端构造hot-update.js script链接，然后插入主文档
- 6.hot-update.js 插入成功后，执行hotAPI 的 createRecord 和 reload方法，获取到 Vue 组件的 render方法，重新render 组件， 继而实现 UI 无刷新更新。


