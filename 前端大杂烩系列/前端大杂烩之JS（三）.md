#### 8. call，apply，bind  

&emsp;&emsp;在JavaScript 中，this的指向是动态变化的，很可能在写程序的过程中，无意中破坏掉this的指向，所以我们需要一种可以把this的含义固定的技术，于是就有了call，apply 和bind这三个方法，来改变函数体内部 this的指向，因为函数存在「定义时上下文」和「运行时上下文」以及「上下文是可以改变的」这样的概念。

&emsp;**call**  

>  
    var a = {
        user:"xyx",
        fn:function(e,ee){
            console.log(this.user); //xyx
            console.log(e+ee); //3
        }
    }
    var b = a.fn;
    b.call(a,1,2);  
    
&emsp;**apply**  

>  
    var a = {
        user:"xyx",
        fn:function(e,ee){
            console.log(this.user); //xyx
            console.log(e+ee); //520
        }
    }
    var b = a.fn;
    var arr = [500,20];
    b.apply(a,arr);  
    
&emsp;**bind**  

&emsp;bind方法和call、apply方法有些不同。

>  
    var a = {
        user:"xyx",
        fn:function(e,d,f){
            console.log(this.user); //xyx
            console.log(e,d,f); //10 1 2
        }
    }
    var b = a.fn;
    var c = b.bind(a,10);
    c(1,2);

&emsp;bind也可以有多个参数，并且参数可以执行的时候再次添加，但是要注意的是，参数是按照形参的顺序进行的。  

&emsp;**总结**：  

&emsp;&emsp;1.&emsp;apply 、 call 、bind 三者都是用来改变函数的this对象的指向的；  
&emsp;&emsp;2.&emsp;apply 、 call 、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文；  
&emsp;&emsp;3.&emsp;apply 、 call 、bind 三者都可以利用后续参数传参；  
&emsp;&emsp;4.&emsp;bind 是返回对应函数，便于稍后调用；apply 、call 则是立即调用 。  

#### 9. 显示原型和隐式原型，原型链是什么？为什么要有原型链  

&emsp;显式原型：prototype  
&emsp;隐式原型：\_\_proto__    

>  
    //以下是用于验证的伪代码
    var f = new F(); 
    //于是有
    f.__proto__ === F.prototype //true
    //又因为
    F.prototype === o;//true
    //所以
    f.__proto__ === o;

&emsp;**原型链**  

&emsp;&emsp;每个对象都有一个私有属性（称之为 [[Prototype]]），它指向它的原型对象（prototype）。该 prototype 对象又具有一个自己的原型对象 ，层层向上直到一个对象的原型为 null。根据定义，null 没有原型，并作为这个原型链中的最后一个环节。  
&emsp;&emsp;几乎所有 JavaScript中的对象都是位于原型链顶端的Object的实例。

&emsp;**为什么要有原型链**  

&emsp;&emsp;JS没有"子类"和"父类"的概念，也没有"类"（class）和"实例"（instance）的区分，全靠一种很奇特的"原型链"（prototype chain）模式，来实现继承。  

#### 10. 创建对象的多种方式  

>  
    // 第一种方式：字面量
    var o1 = {name: 'o1'}
    var o2 = new Object({name: 'o2'})
      // 第二种方式：构造函数
    var M = function (name) { this.name = name; }
    var o3 = new M('o3')
      // 第三种方式：Object.create
    var p = {name: 'p'}
    var o4 = Object.create(p)    
    
&emsp;**引用链接**：https://www.cnblogs.com/chengzp/p/prototype.html
    
#### 11. 实现继承的多种方式和优缺点  


