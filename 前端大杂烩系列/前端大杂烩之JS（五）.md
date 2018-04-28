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