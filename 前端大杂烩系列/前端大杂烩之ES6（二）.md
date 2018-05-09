#### 5. es6的Generator是什么，async/await 实现原理    

&emsp;&emsp;从语法上来说，Generator函数就是一个状态机，封装了多个内部状态。  

&emsp;&emsp;Generator函数跟普通函数的写法有非常大的区别：  

&emsp;&emsp;一、function关键字与函数名之间有一个星号；  

&emsp;&emsp;二、函数体内部使用yield语句，定义不同的内部状态。  

>  
    function* test() {
        yield 'a';
        yield 'b';
        yield 'c';
        return 'ending';
    }
    
    var test1 = test();
    test1.next(); // 返回Object {value: "a", done: false}  
    
&emsp;&emsp;**Generator函数特点：**

&emsp;&emsp;1、test1并不会执行test函数，返回的也不是函数运行结果，而是一个指向内部状态的指针对象，也就是迭代器对象（Iterator Object）。

&emsp;&emsp;2、下一步，必须调用迭代器对象的next方法，使得指针移向下一个状态。也就是说，每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield语句（或return语句）为止。换言之，Generator函数是分段执行的，yield语句是暂停执行的标记，而next方法可以恢复执行。
