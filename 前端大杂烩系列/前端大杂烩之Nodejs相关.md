#### 1. nodeJs概要  

&emsp;&emsp;nodeJS之所以能在后端运行，得归功于V8引擎，通过对高性能V8引擎的封装，并通过一系列优化的API类库，使其能够在后端运行。  

&emsp;&emsp;nodeJs有两大特点：

&emsp;&emsp;1、基于事件驱动；

&emsp;&emsp;2、无阻塞；  

&emsp;&emsp;nodeJs其本质就是JavaScript，所以基于事件驱动不难理解。能做到无阻塞，是nodeJs通过大量的回调函数来达到这一目的。  

#### 2. Express和koa的区别  

&emsp;&emsp;Express主要基于Connect中间件，并且自身封装了路由、视图处理等功能。  

&emsp;&emsp;Koa是Express原班人马基于ES6新特性重新开发的框架，主要基于co中间件，框架自身不包含任何中间件，很多功能需要借助第三方中间件解决，但是由于其基于ES6 generator特性的异步流程控制，解决了"callback hell"和麻烦的错误处理问题。  

&emsp;&emsp;**异步流程控制**  

&emsp;&emsp;&emsp;&emsp;Express 采用 callback 来处理异步；  

&emsp;&emsp;&emsp;&emsp;Koa v1 采用 generator，Koa v2 采用 async/await。    

&emsp;&emsp;**错误处理**  

&emsp;&emsp;&emsp;&emsp;Express使用callback捕获异常，对于深层次的异常捕获不了；  

&emsp;&emsp;&emsp;&emsp;Koa使用try catch，能更好地解决异常捕获。  

&emsp;&emsp;**总结**  

&emsp;&emsp;&emsp;&emsp;Express  

&emsp;&emsp;&emsp;&emsp;优点：线性逻辑，通过中间件形式把业务逻辑细分、简化，一个请求进来经过一系列中间件处理后再响应给用户，清晰明了。  

&emsp;&emsp;&emsp;&emsp;缺点：基于 callback 组合业务逻辑，业务逻辑复杂时嵌套过多，异常捕获困难。  

&emsp;&emsp;&emsp;&emsp;Koa  

&emsp;&emsp;&emsp;&emsp;优点：首先，借助 co 和 generator，很好地解决了异步流程控制和异常捕获问题。其次，Koa 把 Express 中内置的 router、view 等功能都移除了，使得框架本身更轻量。  

&emsp;&emsp;&emsp;&emsp;缺点：社区相对较小  

#### 3. NodeJs适合做什么样的业务  

&emsp;&emsp;**为什么用Node**  

&emsp;&emsp;&emsp;&emsp;1、天然的事件驱动可以用于处理并发；  

&emsp;&emsp;&emsp;&emsp;2、降低前后端协作成本，提高开发效率；  

&emsp;&emsp;&emsp;&emsp;3、职责分明，前端的问题前端er自己负责，自己解决；  

&emsp;&emsp;&emsp;&emsp;4、前后端同构，前端解决方案同步到Server-side；   

&emsp;&emsp;**什么业务场景使用Node**  

&emsp;&emsp;&emsp;&emsp;1、页面需求大，从样式到性能都一直迭代；  

&emsp;&emsp;&emsp;&emsp;2、后端接口丰富，页面数据资源方多；  

&emsp;&emsp;&emsp;&emsp;3、纯渲染，对安全性要求不高，无计算能力；  

&emsp;&emsp;**Nodejs不适合的领域**  

&emsp;&emsp;&emsp;&emsp;1、计算密集型应用，让Javascript和C去拼计算性能，估计是不可能赢的；  

&emsp;&emsp;&emsp;&emsp;2、内存控制，让Javascript和Java比较复杂数据类型定义，也是很困难的。因为Javascript的面向对象是基于JSON的，而Java是直接使用内存结构。所以，通过JSON序列化和反序列的过程控制内存，Javascript就已经输了；  

&emsp;&emsp;&emsp;&emsp;3、大内存的应用，由于V8引擎有内存设计的限制，32位环境中最大堆是1G，64位环境中最大堆也不到2G，如果要一次读入10G数据，对于Nodejs来说也无法实现；  

&emsp;&emsp;&emsp;&emsp;4、静态服务器，虽然Nodejs的优势在IO密集集应用，但是和Nginx的处理静态资源还是有很大的差距；  

&emsp;&emsp;&emsp;&emsp;5、不需要异步的应用：比如系统管理，自行化脚本等，还是Python更顺手，Nodejs的异步调用可能会给编程带来一些麻烦；  

#### 4. NodeJs是如何实现高并发的？  

&emsp;&emsp;NodeJs是单线程且支持高并发的脚本语言。可为什么单线程的NodeJs可以支持高并发呢？  

&emsp;&emsp;I/O密集型处理是NodeJs的强项，因为NodeJs的I/O请求都是异步的（如：sql查询请求、文件流操作操作请求、http请求...）  

&emsp;&emsp;I/O操作是由NodeJs的工作线程去执行的（NodeJs底层的libuv是多线程的线程池用来并行io操作），且主线程是不需要等待结果返回的，只要发出指令马上就可以去做其他的事情。  

#### 5. NodeJs的event loop原理  

&emsp;&emsp;**Node.js的运行机制如下**  

&emsp;&emsp;&emsp;&emsp;1、V8引擎解析JavaScript脚本。

&emsp;&emsp;&emsp;&emsp;2、解析后的代码，调用Node API。

&emsp;&emsp;&emsp;&emsp;3、libuv库负责Node API的执行。它将不同的任务分配给不同的线程，形成一个Event Loop（事件循环），以异步的方式将任务的执行结果返回给V8引擎。

&emsp;&emsp;&emsp;&emsp;4、V8引擎再将结果返回给用户。  

&emsp;&emsp;**event loop的事件处理机制如果运作的**  

&emsp;&emsp;&emsp;&emsp;事件循环分为几个阶段，每个阶段都是按照先进先出的规则执行回调函数。按顺序执行每个阶段的回调函数队列，直至队列为空或是该阶段执行的回调函数达到该阶段所允许一次执行回调函数的最大限制后，才会将操作权移交给下一阶段。    

&emsp;&emsp;**每个阶段的简单概要**  

&emsp;&emsp;&emsp;&emsp;1、timers：执行setTimeout()和setInterval()预先设定的回调函数。  

&emsp;&emsp;&emsp;&emsp;2、I/O callbacks：大部分执行都是timers阶段或是setImmediate()预先设定的并且出现异常的回调函数事件。  

&emsp;&emsp;&emsp;&emsp;3、idle, prepare：NodeJs内部函数调用。  

&emsp;&emsp;&emsp;&emsp;4、poll：检索新的I/O事件，NodeJs将在适当的时候阻塞。  

&emsp;&emsp;&emsp;&emsp;5、check：setImmediate() 函数会在这个阶段执行。  

&emsp;&emsp;&emsp;&emsp;6、close callbacks：执行一些诸如关闭事件的回调函数，如socket.on('close', ...) 。
