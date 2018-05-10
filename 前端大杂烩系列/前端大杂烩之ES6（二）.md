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

#### 6. ES6和commonjs模块化规范区别  

&emsp;**es6模块化**  

&emsp;&emsp;1、export：可以输出多个，输出方式为 {}；  

&emsp;&emsp;2、export default ：只能输出一个，可以与export 同时输出，但是不建议这么做；  

&emsp;&emsp;3、解析阶段确定对外输出的接口，解析阶段生成接口；  

&emsp;&emsp;4、模块不是对象，加载的不是对象；  

&emsp;&emsp;5、可以单独加载其中的某个接口（方法）；  

&emsp;&emsp;6、静态分析，动态引用，输出的是值的引用，值改变，引用也改变，即原来模块中的值改变则该加载的值也改变；  

&emsp;&emsp;7、this 指向undefined；  

&emsp;**commonJS**  

&emsp;&emsp;1、module.exports =  ... ：      只能输出一个，且后面的会覆盖上面的；  

&emsp;&emsp;2、exports. ... ：可以输出多个；  

&emsp;&emsp;3、运行阶段确定接口，运行时才会加载模块；  

&emsp;&emsp;4、模块是对象，加载的是该对象；  

&emsp;&emsp;5、加载的是整个模块，即将所有的接口全部加载进来；  

&emsp;&emsp;6、输出是值的拷贝，即原来模块中的值改变不会影响已经加载的该值；  

&emsp;&emsp;7、this指向当前模块；    

#### 7.箭头函数的this和普通函数的this

&emsp;普通函数的this，哪里调用的this就指向哪里；

&emsp;ES6箭头函数的this，哪里定义的this就指向哪里；  

&emsp;箭头函数有两个方面的作用：更简短的函数并且不绑定this。  

&emsp;箭头函数本身没有this，它会直接绑定到它的父级作用域内的this，也就是定义它时的作用域内的this值。

