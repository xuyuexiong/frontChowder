#### 12. new一个对象具体做了什么？ 

&emsp;使用关键字new创建新实例对象经过了以下几步：

&emsp;1、创建一个新对象，如：var person = {};

&emsp;2、新对象的_proto_属性指向构造函数的原型对象。

&emsp;3、将构造函数的作用域赋值给新对象。（也所以this对象指向新对象）

&emsp;4、执行构造函数内部的代码，将属性添加给person中的this对象。

&emsp;5、返回新对象person。 

>  
    var person = {};  
    person._proto_ = Person.prototype; //引用构造函数的原型对象  
    Person.call(person); //将构造函数的作用域给person,即：this值指向person  

<br>

#### 13. 手写Ajax，XMLHttpRequest

<br>

&emsp;**手写AJAX的步骤**  

&emsp;&emsp;1.&emsp;创建XMLHttpRequest对象  

&emsp;&emsp;2.&emsp;指定响应函数  

&emsp;&emsp;3.&emsp;打开连接（指定请求）  

&emsp;&emsp;4.&emsp;发送请求  

&emsp;&emsp;5.&emsp;创建响应函数   

<br>

&emsp;**W3C版参考代码**  

>  
    var xmlhttp=null;//声明一个变量，用来实例化XMLHttpRequest对象
    if (window.XMLHttpRequest){
        xmlhttp=new XMLHttpRequest();// 新版本的浏览器可以直接创建XMLHttpRequest对象
    }
      
    else if (window.ActiveXObject){
        xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");// IE5或IE6没有XMLHttpRequest对象，而是用的ActiveXObject对象
    }
      
      
    if (xmlhttp!=null){
        xmlhttp.onreadystatechange=state_Change;//指定响应函数为state_Change
        xmlhttp.open("GET","/example/xdom/note.xml",true);//指定请求，这里要访问在/example/xdom路径下的note.xml文件，true代表的使用的是异步请求
        xmlhttp.send(null);//发送请求
    } 
    else{
        alert("Your browser does not support XMLHTTP.");
    }
    
    //创建具体的响应函数state_Change
    function state_Change(){
        if (xmlhttp.readyState==4){
            if (xmlhttp.status==200){
                // 这里应该是函数具体的逻辑
            }
            else{
                alert("Problem retrieving XML data");
            }
        }
    }  

<br>

&emsp;**MDN版参考代码**  

>  
    <!--html部分，创建一个按钮控件-->
    <span id="ajaxButton" style="cursor: pointer; text-decoration: underline">
      Make a request
    </span>
    
    
    <script type="text/javascript">
    (function() {
      var httpRequest;//声明一个变量，用来实例化XMLHttpRequest对象
      document.getElementById("ajaxButton").onclick = function() { makeRequest('test.html'); }; //这里将AJAX操作封装在makeRequest函数中，函数的参数为要请求的url，即根目录下的test.html文件。
     
      function makeRequest(url) {
        httpRequest = new XMLHttpRequest();//创建XMLHttpRequest对象
        if (!httpRequest) {
          alert('Giving up :( Cannot create an XMLHTTP instance');
          return false;
        }
        
        httpRequest.onreadystatechange = alertContents;//指定响应函数为alertContents
        
        httpRequest.open('GET', url); //指定请求，方法为GET，url为上面的test.html
       
        httpRequest.send();//发送请求
        
      }
      
      
    //创建响应函数alertContents
      function alertContents() {
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
          if (httpRequest.status === 200) {
            alert(httpRequest.responseText);
          } else {
            alert('There was a problem with the request.');
          }
        }
      }
    })();//这是一个立即执行函数
    </script>  
    
&emsp;**引用链接**：https://segmentfault.com/a/1190000008097712  

<br>

#### 14. 变量提升/函数声明提升  

&emsp;&emsp;JS引擎在读取JS代码时会进行两个步骤，第一个步骤是解释，第二个步骤是执行。   
&emsp;&emsp;解释就是先扫描所有的JS代码，然后把所有声明提升到顶端；执行就是执行解释后的代码。  

&emsp;**例子1**：

>  
    console.log(a);//输出结果 undefined
    var a=10;
    
&emsp;&emsp;原因： 变量提升（把变量声明提升到当前执行环境的最顶端）。  

&emsp;&emsp;上段代码相当于：  

>  
    var a; 
    console.log(a);//由于未赋值 所以输出undefined 
    a=10;  
    
&emsp;**例子2**：  

>  
    foo();
    function foo(){
        console.log("aaa");//输出aaa
    }  
    
&emsp;&emsp;原理：函数声明提升（函数声明提升直接把整个函数提到执行环境的最顶端）。  

&emsp;&emsp;上段代码相当于：    

>  
    function foo(){
        console.log("aaa");
    }
    foo();  
    
&emsp;**例子3**：  

&emsp;&emsp;变量提升只提升函数名，而函数提升会提升整个函数体。注意：函数提升在变量提升上面。  

>  
    foo();// foo is not a function
    var foo = function(){
        console.log("aaa");
    }  
    
&emsp;&emsp;原因：还是进行了变量提升  

&emsp;&emsp;上段代码相当于：   

>  
    var foo;
    console.log(foo);  //undefined
    foo(); //foo is not a function
    foo = function(){
        console.log("aaa");
    }  
    
&emsp;**例子4**： 

>  
    console.log(foo); //f foo(){console.log(10);}
    var foo=10;
    console.log(foo); //10
    function foo(){
        console.log(10); 
    }
    console.log(foo); //10  
    
&emsp;&emsp;相当于：  

>  
    function foo(){
        console.log(10);
    }
    var foo;
    console.log(foo);
    foo=10;
    console.log(foo);
    console.log(foo);  
    
&emsp;&emsp;注意： 函数提升在变量提升上面，第一个console.log(foo);为什么会输出函数题呢，原因在于 var foo。并未有赋值只是声明，因此他会调用上面的值。  

&emsp;&emsp;**总结：函数提升在变量提升之上。**