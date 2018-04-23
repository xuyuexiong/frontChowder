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