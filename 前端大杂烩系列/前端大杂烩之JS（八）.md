#### 28. typeof 和 instanceof 区别，instanceof原理  

&emsp;**typeof**  

&emsp;&emsp;typeof方法返回一个字符串，来表示数据的类型，但是数组、正则、日期、对象的typeof返回值都是object。所以用typeof方法来判断引用数据类型，是有一定误差的。  

&emsp;**instanceof**  

&emsp;&emsp;instanceof用于判断某个变量是否是某个对象的实例，返回值为true或false，当typeof无法判断某个对象是否是数组或者某个变量是否是对象的实例时，常用instanceof方法来判断。  

&emsp;**instanceof原理**  

&emsp;&emsp;instanceof运算符主要是判断某个构造函数的prototype属性是否存在于另外一个要检测对象的原型链上。   

#### 29. js动画和css3动画比较  

&emsp;**CSS动画**

&emsp;&emsp;优点：   

&emsp;&emsp;1、浏览器可以对动画进行优化。

&emsp;&emsp;&emsp;&emsp;浏览器使用与 requestAnimationFrame类似的机制，requestAnimationFrame比起setTimeout，setInterval设置动画的优势主要是:   

&emsp;&emsp;&emsp;&emsp;（1）requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成,并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率,一般来说,这个频率为每秒60帧。  

&emsp;&emsp;&emsp;&emsp;（2）在隐藏或不可见的元素中requestAnimationFrame不会进行重绘或回流，这当然就意味着更少的的cpu，gpu和内存使用量。

&emsp;&emsp;2、强制使用硬件加速 （通过 GPU 来提高动画性能）。  

&emsp;&emsp;3、代码相对简单,性能调优方向固定。  

&emsp;&emsp;4、对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码。  

&emsp;&emsp;缺点：

&emsp;&emsp;&emsp;&emsp;1、 运行过程控制较弱,无法附加事件绑定回调函数。CSS动画只能暂停,不能在动画中寻找一个特定的时间点，不能在半路反转动画，不能变换时间尺度，不能在特定的位置添加回调函数或是绑定回放事件,无进度报告。  

&emsp;&emsp;&emsp;&emsp;2、代码冗长。想用 CSS 实现稍微复杂一点动画,最后CSS代码都会变得非常笨重。  

&emsp;**JS动画**  

&emsp;&emsp;优点：  

&emsp;&emsp;&emsp;&emsp;1、JavaScript动画控制能力很强, 可以在动画播放过程中对动画进行控制：开始、暂停、回放、终止、取消都是可以做到的。  

&emsp;&emsp;&emsp;&emsp;2、动画效果比css3动画丰富,有些动画效果，比如曲线运动,冲击闪烁,视差滚动效果，只有JavaScript动画才能完成。  

&emsp;&emsp;&emsp;&emsp;3、CSS3有兼容性问题，而JS大多时候没有兼容性问题。  

&emsp;&emsp;缺点：  

&emsp;&emsp;&emsp;&emsp;1、JavaScript在浏览器的主线程中运行，而主线程中还有其它需要运行的JavaScript脚本、样式计算、布局、绘制任务等,对其干扰导致线程可能出现阻塞，从而造成丢帧的情况。  

&emsp;&emsp;&emsp;&emsp;2、代码的复杂度高于CSS动画。  

**引用链接**：https://www.cnblogs.com/simba-lkj/p/6139066.html    

#### 30. js处理异常  

&emsp;&emsp;由于Javascript 引擎是单线程的，因此一旦遇到异常，Javascript 引擎通常会停止执行，阻塞后续代码并抛出一个异常信息，因此对于可预见的异常，我们应该捕捉并正确展示给用户或开发者。  

&emsp;**Error对象**  

&emsp;&emsp;throw 和 Promise.reject() 可以抛出字符串类型的异常，也可以抛出一个 Error 对象类型的异常。一个 Error 对象类型的异常不仅包含一个异常信息，同时也包含一个追溯栈，可以很容易通过追溯栈找到代码出错的行数。所以推荐抛出 Error 对象类型的异常，而不是字符串类型的异常。  

&emsp;**Try / Catch**  

&emsp;&emsp;try/catch 主要用于捕捉异常。try/catch 语句包含了一个 try 块, 和至少有一个 catch 块或者一个 finally 块，下面是三种形式的 try 声明:  

&emsp;&emsp;try...catch  
&emsp;&emsp;try...finally  
&emsp;&emsp;try...catch...finally  

&emsp;&emsp;try 块中放入可能会产生异常的语句或函数

&emsp;&emsp;catch 块中包含要执行的语句，当 try 块中抛出异常时，catch 块会捕捉到这个异常信息，并执行 catch 块中的代码，如果在 try 块中没有异常抛出，这 catch 块将会跳过。

&emsp;&emsp;finally 块在 try 块和 catch 块之后执行。无论是否有异常抛出或着是否被捕获它总是执行。当在 finally 块中抛出异常信息时会覆盖掉 try 块中的异常信息。  

&emsp;**Throw**  

&emsp;&emsp;throw 语句用来抛出一个用户自定义的异常。当前函数的执行将被停止（throw 之后的语句将不会执行），并且控制将被传递到调用堆栈中的第一个 catch 块。如果调用者函数中没有 catch 块，程序将会终止。  

>  
    try {
        console.log('before throw error');
        throw new Error('throw error');
        console.log('after throw error');
    } catch (err) {
        console.log(err.message);
    }
    
    // before throw error
    // throw error  
    
&emsp;**window.onerror**  

&emsp;&emsp;通过在 window.onerror 上定义一个事件监听函数，程序中其他代码产生的未被捕获的异常往往就会被 window.onerror 上面注册的监听函数捕获到。并且同时捕获到一些关于异常的信息。  
>  
    window.onerror = function (message, source, lineno, colno, error) { }
    //message：异常信息（字符串）
    //source：发生异常的脚本URL（字符串）
    //lineno：发生异常的行号（数字）
    //colno：发生异常的列号（数字）
    //error：Error对象（对象）  
    
&emsp;**引用链接**：https://segmentfault.com/a/1190000011481099 

#### 31. 什么是函数柯里化  

&emsp;柯里化又称部分求值，字面意思就是不会立刻求值，而是到了需要的时候再去求值。听起来跟bind的作用是一样的，其实bind也可以采用这种思想来实现。  

&emsp;如果要实现这样一个加法函数：
>  
    add(1,2,3)(1)(2)(3)(4,5,6)(7,8)() === 42  
    
&emsp;&emsp;实现的原理主要是：

&emsp;&emsp;1、闭包保存args变量，存储之前的参数；    

&emsp;&emsp;2、新建一个_add函数，参数的长度为0，就执行加法，否则，存储参数到args，然后返回函数自身（可以选择匿名函数，返回arguments.callee即可，意思相同，见代码中注释掉的部分，但是在严格模式下不能使用，所以还是使用方法一比较稳妥）。  

>  
    // add 函数柯里化
    function add(){
        //建立args,利用闭包特性，不断保存arguments
        var args = [].slice.call(arguments);
           //方法一，新建_add函数实现柯里化
        var _add = function(){
            if(arguments.length === 0){
                //参数为空，对args执行加法
                return args.reduce(function(a,b){return a+b});
            }else {
                //否则，保存参数到args，返回一个函数
                [].push.apply(args,arguments);
                return _add;
            }
        }
        //返回_add函数
        return _add;
        
        // //方法二，使用arguments.callee实现柯里化
        // return function () {
      //       if (arguments.length === 0) {
      //           return args.reduce(function(a,b){return a+b});
      //       }
      //       Array.prototype.push.apply(args, arguments);
      //       return arguments.callee;
      //   }
    }
    console.log(add(1,2,3)(1)(2)(3)(4,5,6)(7,8)());//42  
    
&emsp;**柯里化有3个常见作用：**  

&emsp;&emsp;1. 参数复用；  
&emsp;&emsp;2. 提前返回；  
&emsp;&emsp;3. 延迟计算/运行。  

&emsp;**引用链接**：https://www.jianshu.com/p/f88a5175e7a2