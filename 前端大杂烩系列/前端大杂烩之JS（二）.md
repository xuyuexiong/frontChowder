#### 5. 事件委托（手写例子），事件冒泡和捕获，如何阻止冒泡？如何阻止默认事件？  


&emsp;**事件委托**

>   
    //事件冒泡
    elem.addEventListener(type,function(){},false);
    
    //事件捕获
    elem.addEventListener(type,function(){},true);
>   

&emsp;**阻止冒泡**

>  
    div.onClick = function() {
        console.log('a');
        e.stopPropagation();
    }  
    
&emsp;**阻止默认事件**  

>  
    if(window.event){ 
        //IE中阻止函数器默认动作的方式  
        window.event.returnValue = false;  
    } 
    else{ 
        //阻止默认浏览器动作(W3C)  
        e.preventDefault(); 
    }    
    
#### 6. 对闭包的理解？什么时候构成闭包？闭包的实现方法？闭包的优缺点？  

&emsp;**什么是闭包：**  

&emsp;&emsp;闭包就是能够读取其他函数内部变量的函数。  
&emsp;&emsp;由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。
所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。  

&emsp;**什么时候构成闭包**  

&emsp;&emsp;闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。  

&emsp;**闭包的实现方法**   

> 
    var name = "The Window";
    var object = {
        name : "My Object",
        getNameFunc : function(){
            var that = this;
            return function(){
                return that.name;
            };
        }
    };
    alert(object.getNameFunc()());   
    　
&emsp;**闭包的缺点**  

&emsp;&emsp;1.&emsp;由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。  

&emsp;&emsp;2.&emsp;闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（PublicMethod），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。  

&emsp;**引用链接**：http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html
<br>

#### 7. this有哪些使用场景？跟C,Java中的this有什么区别？如何改变this的值？  

&emsp;**Java中的this**

&emsp;&emsp;在 Java 等面向对象的语言中，this 关键字的含义是明确且具体的，即指代当前对象。一般在编译期确定下来，或称为编译期绑定。

&emsp;**this的使用场景**  

&emsp;&emsp;1. 作为对象方法调用  

&emsp;&emsp;在 JavaScript中，函数也是对象，因此函数可以作为一个对象的属性，此时该函数被称为该对象的方法，在使用这种调用方式时，this 被自然绑定到该对象。  
>  
    var point = { 
        x : 0, 
        y : 0, 
        moveTo : function(x, y) { 
            this.x = this.x + x; 
            this.y = this.y + y; 
        } 
    }; 
    point.moveTo(1, 1)//this 绑定到当前对象，即 point 对象  
    
&emsp;&emsp;2. 作为函数调用  

&emsp;&emsp;函数也可以直接被调用，此时 this绑定到全局对象。在浏览器中，window 就是该全局对象。比如下面的例子：函数被调用时，this被绑定到全局对象，接下来执行赋值语句，相当于隐式的声明了一个全局变量，这显然不是调用者希望的。  

>  
    function makeNoSense(x) { 
        this.x = x; 
    } 
    makeNoSense(5); 
    x;// x 已经成为一个值为 5 的全局变量    

&emsp;&emsp;对于内部函数，即声明在另外一个函数体内的函数，这种绑定到全局对象的方式会产生另外一个问题。我们仍然以前面提到的 point对象为例，这次我们希望在 moveTo 方法内定义两个函数，分别将 x，y 坐标进行平移。结果可能出乎大家意料，不仅 point 对象没有移动，反而多出两个全局变量 x，y。  

>  
    var point = { 
        x : 0, 
        y : 0, 
        moveTo : function(x, y) { 
            // 内部函数
            var moveX = function(x) { 
                this.x = x;//this 绑定到了哪里？
            }; 
            // 内部函数
            var moveY = function(y) { 
                this.y = y;//this 绑定到了哪里？
            }; 
            moveX(x); 
            moveY(y); 
        } 
    }; 
    point.moveTo(1, 1); 
    point.x; //==>0 
    point.y; //==>0 
    x; //==>1 
    y; //==>1  
    
&emsp;&emsp;这属于 JavaScript 的设计缺陷，正确的设计方式是内部函数的 this 应该绑定到其外层函数对应的对象上，为了规避这一设计缺陷，聪明的 JavaScript程序员想出了变量替代的方法，约定俗成，该变量一般被命名为 that。  

>  
    var point = { 
        x : 0, 
        y : 0, 
        moveTo : function(x, y) { 
            var that = this; 
            // 内部函数
            var moveX = function(x) { 
                that.x = x; 
            }; 
            // 内部函数
            var moveY = function(y) { 
                that.y = y; 
            } 
            moveX(x); 
            moveY(y); 
        } 
    }; 
    point.moveTo(1, 1); 
    point.x; //==>1 
    point.y; //==>1
    
&emsp;&emsp;3. 作为构造函数调用  

&emsp;&emsp;JavaScript支持面向对象式编程，与主流的面向对象式编程语言不同，JavaScript 并没有类（class）的概念，而是使用基于原型（prototype）的继承方式。相应的，JavaScript 中的构造函数也很特殊，如果不使用 new调用，则和普通函数一样。作为又一项约定俗成的准则，构造函数以大写字母开头，提醒调用者使用正确的方式调用。如果调用正确，this 绑定到新创建的对象上。  

&emsp;**如何改变this的值**

&emsp;&emsp;**使用 apply 或 call 调用**  

&emsp;&emsp;在 JavaScript 中函数也是对象，对象则有方法，apply 和 call 就是函数对象的方法。这两个方法异常强大，他们允许切换函数执行的上下文环境（context），即 this 绑定的对象。很多 JavaScript中的技巧以及类库都用到了该方法。让我们看一个具体的例子：  

>  
    function Point(x, y){ 
        this.x = x; 
        this.y = y; 
        this.moveTo = function(x, y){ 
            this.x = x; 
            this.y = y; 
        } 
    } 
    var p1 = new Point(0, 0); 
    var p2 = {x: 0, y: 0}; 
    p1.moveTo(1, 1); 
    p1.moveTo.apply(p2, [10, 10]);  
    
&emsp;&emsp;在上面的例子中，我们使用构造函数生成了一个对象 p1，该对象同时具有 moveTo 方法；使用对象字面量创建了另一个对象 p2，我们看到使用 apply 可以将 p1 的方法应用到 p2 上，这时候 this 也被绑定到对象 p2 上。另一个方法 call 也具备同样功能，不同的是最后的参数不是作为一个数组统一传入，而是分开传入的。