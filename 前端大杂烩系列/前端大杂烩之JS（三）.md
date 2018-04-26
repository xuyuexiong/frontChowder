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

&emsp;**(1)原型继承**  

>  
    let Super = functioin(name) {
        this.name = name;
        this.setName = (newName) => {
            this.name = name;
        };
        this.getName = () => {
            return this.name;
        }
    }
    let Sub = function(sex) {
        this.sex = sex;
    }
    Sub.prototype = new Super('eric');  //通过改变原型对象实现继承
    let sub1 = new Sub('male')
        sub2 = new Sub('female');
    sub1.setName('ada');
    // 这里必须通过setName方法来修改继承来的name属性。
    // 如果通过sub1.name== 'ada',就打不到目的，因为此时sub1对象上没有name属性，
    // 这样等于为该对象添加了新的属性，而不是修改继承而来的name属性。
    console.log(sub2.name); // ada,可见此sub2的name也会被修改掉
    console.log(sub1.getName === sub2.getName) // true,复用了方法  
    
&emsp;&emsp;**优点**：父类的方法(getName)得到了复用。

&emsp;&emsp;**缺点**：同理父类的属性(name)也是复用，即子类实例没有自己的属性。  

<br>

&emsp;**(2)构造函数实现继承**  

>  
    let Super = function(name) {
        this.name = name;
        this.getName = () => {
            return this.name;
        }
    }
    let Sub = function(sex,name) {
        Super.call(this,name); // 调用父类方法为子类实例添加属性
        this.sex = sex;
    }
    let sub1 = new Sub('male','eric'),
        sub2 = new Sub('female','eric');
    sub1.name = 'ada';
    console.log(sub2.name); // eric,实例的属性没有相互影响
    console.log(sub1.getName === sub2.getName); // false,可见方法没有复用  
    
&emsp;&emsp;**优点**：子类的每个实例都有自己的属性（name），不会相互影响。

&emsp;&emsp;**缺点**：但是继承父类方法的时候就不需要这种特性，没有实现父类方法的复用。  

<br>  

&emsp;**(3)组合式继承**  

>  
    let Super = function(name) {
        this.name = name;
    }
    Super.prototype = {
        constructor: Super, // 保持构造函数和原型对象的完整性
        getName() {
            return this.name;
        }
    }
    let Sub = function(sex) {
        Super.call(this,'eric'); //继承父类属性
        this.sex = sex;
    }
    Sub.prototype = new Super('eric'); //继承父类方法
    Sub.prototype.constructor = Sub;
    let sub1 = new Sub('male'),
        sub2 = new Sub('female');
    // 可以按上述两种方法验证，复用了父类的方法，实例没有复用，达到目的  
    
&emsp;&emsp;**优点**：继承了上述两种方式的优点，摒弃了缺点，复用了方法，子类又有各自的属性。

&emsp;&emsp;**缺点**：因为父类构造函数被执行了两次，子类的原型对象(Sub.prototype)中也有一份父类的实例属性，而且这些属性会被子类实例(sub1,sub2)的属性覆盖掉，也存在内存浪费。

<br>  

&emsp;**(4)寄生组合式继承**  

>  
    let Super = function(name) {
        this.name = name;
    }
    Super.prototype = {
        constructor: Super,
        getName() {
            return this.name;
        }
    }
    let Sub = function(sex,name) {
        Super.call(this,name);
        this.sex = sex;
    }
    // 组合继承的缺点就是在继承父类方法的时候调用了父类构造函数，从而造成内存浪费，
    // 现在只要解决了这个问题就完美了。那在复用父类方法的时候，
    // 使用Object.create方法也可以达到目的，没有调用父类构造函数，问题解决。
    Sub.prototype = Object.create(Super.prototype);
    Sub.prototype.constructor = Sub;  
    
&emsp;**(5)es6中的class**   

>  
    class Super() {
        constructor(props = { name: 'eric' }) {
            this.name = props.name;
        }
        setName(name) {
            this.name = name;
        }
        getName() {
            return this.name;
        }
    }
    class Sub extends Super {
        constructor(props) {
            super(props = { sex: 'male' }); // 创建实例，继承父类属性和方法
            this.sex = props.sex;
        }
    }
    let sub1 = new Sub({
        name: 'eric',
        sex: 'male'
    })
    let sub2 = new Sub({
        name: 'eric',
        sex: 'female'
    })
    sub1.setName('ada');
    console.log(sub1.getName(),sub2.getName()) // ada,eric,属性没复用，各自实例都有自己的属性。
    console.log(sub1.getName === sub2.getName) // true; 复用了父类的方法
    console.log(Sub.prototype.sex) // undefined
    // 子类原型对象上没有父类构造函数中赋值的属性，不是组合式继承  
    
<br>  

&emsp;**引用链接**：https://segmentfault.com/a/1190000009955064