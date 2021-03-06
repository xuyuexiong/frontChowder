#### 24. setTimeout和promise的执行顺序  

&emsp;一个浏览器环境（unit of related similar-origin browsing contexts.）只能有一个事件循环（Event loop），而一个事件循环有多个任务队列（Task queue），每个任务都有一个任务源（Task source）。不同的任务队列，有不同的优先级。  

&emsp;用setImmediate和process.nextTick进行测试，优先级如下：

&emsp;&emsp;process.nextTick > promise.then > setTimeout > setImmediate  

#### 25. js的垃圾回收机制  

&emsp;为了防止内存泄漏，js与java一样，有一套自己的垃圾回收机制，并且在开发过程中，无需考虑内存分配的问题，因为js会根据一定的规则，自动回收无用的变量，释放其占用的内存。因为这个过程占用许多资源，所以垃圾回收机制是按照固定的时间周期性的执行。  

&emsp;js中，变量有其生命周期，其中全局变量的生命周期，直到浏览器卸载页面后才会结束，而局部变量，只在函数执行的过程中存在，垃圾回收机制会将函数结束后的局部变量清理，这仅仅是垃圾回收的一种情况，因为在闭包中，看似函数结束了，实则没有，垃圾回收器必须判断变量是否有用，以下是常见的两种方法：  

>&emsp;&emsp;**标记清除（mark and sweep）**  
<br>
&emsp;&emsp;这是JavaScript最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。  
<br>
&emsp;&emsp;垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了，因为环境中的变量已经无法访问到这些变量了，然后垃圾回收器相会这些带有标记的变量机器所占空间。  
<br>
&emsp;&emsp;**引用计数(reference counting)**  
<br>
&emsp;&emsp;在低版本IE中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。  
<br>
&emsp;&emsp;看起来也不错的方式，为什么很少有浏览器采用，还会带来内存泄露问题呢？主要是因为这种方式没办法解决循环引用问题。比如对象A有一个属性指向对象B，而对象B也有有一个属性指向对象A，这样相互引用   
<br>
&emsp;&emsp;function test(){  
&emsp;&emsp;&emsp;&emsp;var a={};  
&emsp;&emsp;&emsp;&emsp;var b={};  
&emsp;&emsp;&emsp;&emsp;a.prop=b;  
&emsp;&emsp;&emsp;&emsp;b.prop=a;  
&emsp;&emsp;}  
<br>
&emsp;&emsp;这样a和b的引用次数都是2，即使在test()执行完成后，两个对象都已经离开环境，在标记清除的策略下是没有问题的，离开环境的就被清除，但是在引用计数策略下不行，因为这两个对象的引用次数仍然是2，不会变成0，所以其占用空间不会被清理，如果这个函数被多次调用，这样就会不断地有空间不会被回收，造成内存泄露。  
<br>
&emsp;&emsp;**解决办法**  
<br>
&emsp;&emsp;手动解除循环引用  

&emsp;**引用链接**：https://www.cnblogs.com/dolphinX/p/3348468.html  

#### 26. DOM事件中target和currentTarget的区别  

&emsp;**target**：触发事件的某个具体对象，只会出现在事件流的目标阶段（谁触发谁命中，所以肯定是目标阶段）。  

&emsp;**currentTarget**：绑定事件的对象，恒等于this，可能出现在事件流的任意一个阶段中。  

&emsp;&emsp;通常情况下target和currentTarget是一致的，我们只要使用target即可，但有一种情况必须区分这三者的关系，那就是在父子嵌套的关系中，父元素绑定了事件，单击了子元素（根据事件流，在不阻止事件流的前提下他会传递至父元素，导致父元素的事件处理函数执行），这时候currentTarget指向的是父元素，因为他是绑定事件的对象，而target指向了子元素，因为他是触发事件的那个具体对象。  

#### 27. 内存泄漏的原因和场景   

&emsp;**原因**

&emsp;&emsp;当两个对象相互引用时，构成了循环引用，垃圾回收机制使用标记清除的方式，循环引用能被正常清除，但如果是引用计数的方式，垃圾回收器可能不能正确识别循环引用，这个时候DOM 对象和 JavaScript 对象均不能被销毁，造成了内存泄漏。  

&emsp;**场景**  

&emsp;1、给DOM对象添加的属性是一个对象的引用。  

>  
    var obj = {};   
    document.getElementById('id1').property = obj;  //如果DOM不被消除，则obj会一直存在，造成内存泄漏    
    
&emsp;2、DOM对象与JS对象相互引用。

>  
    function obj(element) {   
        this.elementReference = element; // 为obj(js)对象的属性绑定element(DOM)对象  
        element.property = this;//为element(DOM)对象的属性绑定obj(js)对象  
    }   
    new obj(document.getElementById('id1'));  

&emsp;3、给DOM对象用attachEvent绑定事件。  

>  
    function click() {}   
    element.attachEvent("onclick", click);   
    
&emsp;4、从外到内执行appendChild。这时即使调用removeChild也无法释放。  

>  
    var parentDiv = document.createElement("div");   
    var childDiv = document.createElement("div");   
    document.body.appendChild(parentDiv);   
    parentDiv.appendChild(childDiv);     
    
&emsp;5、反复重写同一个属性会造成内存大量占用(但关闭IE后内存会被释放)。  
  
