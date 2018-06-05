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