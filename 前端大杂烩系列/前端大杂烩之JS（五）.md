#### 15. 举例说明一个匿名函数的典型用例  

&emsp;**最常见的用法**  

>  
    (function() { 
        alert('water'); 
    })();   

&emsp;**带参数**    

>  
    (function(o) { 
        alert(o); 
    })('water');   
    
&emsp;**链式调用**   

>  
    (function(o) { 
        alert(o); 
        return arguments.callee; 
    })('water')('down');   
    
#### 16. 指出JS的宿主对象和原生对象的区别，为什么扩展JS内置对象不是好的做法？有哪些内置对象和内置函数？  

&emsp;**原生对象**：也称为本地对象，独立于宿主环境的ECMAScript实现的对象。   

&emsp;**宿主对象**：ECMAScript官方未定义的对象都属于宿主对象。  

&emsp;**总结**：本地对象就是ECMAScript中定义好的对象，如String、Date等，内置对象是本地对象中比较特殊的一种，它不用实例化，包括Global和Math，宿主对象就是BOM、DOM和自己定义的对象。  

&emsp;**扩展JS内置对象会产生比全局变量更大的污染。**   

&emsp;**内置对象**  

&emsp;&emsp;包含：Global和Math。  
&emsp;&emsp;ECMAScript5中增添了JSON这个存在于全局的内置对象。  

&emsp;**内置函数**  

&emsp;&emsp;1.&emsp;常规函数  
&emsp;&emsp;2.&emsp;数组函数  
&emsp;&emsp;3.&emsp;日期函数  
&emsp;&emsp;4.&emsp;数学函数  
&emsp;&emsp;5.&emsp;字符串函数    

#### 17. document load和document DOMContentLoaded两个事件的区别  

&emsp;**DOM文档加载的步骤为**

- 解析HTML结构。  
- 加载外部脚本和样式表文件。  
- 解析并执行脚本代码。  
- DOM树构建完成。//DOMContentLoaded  
- 加载图片等外部文件。  
- 页面加载完毕。//load  

&emsp;1.当 onload 事件触发时，页面上所有的DOM，样式表，脚本，图片，flash都已经加载完成了。

&emsp;2.当 DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash。  

#### 18. === 和 == 

&emsp;**双等号==**： 

&emsp;（1）如果两个值类型相同，再进行三个等号(===)的比较。

&emsp;（2）如果两个值类型不同，也有可能相等，需根据以下规则进行类型转换在比较：

&emsp;&emsp;&emsp;1）如果一个是null，一个是undefined，那么相等。

&emsp;&emsp;&emsp;2）如果一个是字符串，一个是数值，把字符串转换成数值之后再进行比较。  

&emsp;**三等号===**：  

&emsp;（1）如果类型不同，就一定不相等。

&emsp;（2）如果两个都是数值，并且是同一个值，那么相等；如果其中至少一个是NaN，那么不相等。（判断一个值是否是NaN，只能使用isNaN( ) 来判断）

&emsp;（3）如果两个都是字符串，每个位置的字符都一样，那么相等，否则不相等。

&emsp;（4）如果两个值都是true，或是false，那么相等。

&emsp;（5）如果两个值都引用同一个对象或是函数，那么相等，否则不相等。

&emsp;（6）如果两个值都是null，或是undefined，那么相等。  

#### 19. 原生事件绑定（跨浏览器），dom0和dom2的区别？  

&emsp;**0级DOM**

&emsp;&emsp;分为2个：  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;一是在标签内写onclick事件

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;二是在JS写onlicke=function（）{}函数
　　　　  
&emsp;**2级DOM**  

&emsp;&emsp;只有一个：监听方法，原生有两个方法用来添加和移除事件处理程序：addEventListener()和removeEventListener()。

&emsp;**区别**：如果定义了两个dom事件，dom0级事件会覆盖，dom2不会覆盖，会依次执行，dom0和dom2可以共存，不互相覆盖，但是dom0之间依然会覆盖。