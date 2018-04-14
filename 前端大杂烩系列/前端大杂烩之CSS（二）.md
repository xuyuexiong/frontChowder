#### 5. position和display。  
&emsp;&emsp;**（1）display属性的值与作用；**   

&emsp;none

    1）表示该元素不会显示，并且该元素的空间也不存在，可理解为已删除；

    2）visibility：hidden只是将元素隐藏，但不会改变页面布局，但也不会触发该元素已经绑定的事件；

    3)opacity：0，将元素隐藏，不会改变页面布局，但会触发该元素绑定的事件。

&emsp;inline

    1）内联元素，与其他元素在一行；

    2）不可设置宽高；

    3）margin-top与margin-bottom无效，但margin-left与margin-right有效；

    4）padding-left与padding-right同样有效，但是padding-top与padding-bottom不会影响元素高度，会影        响背景高度；

    5）常见的有<a>、<span>、<br>、<i>、<em>、<strong>。

&emsp;block

    块级元素，常见的有<div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>

&emsp;inline-block

    1)行内块元素，即是内联元素，又可设置宽高以及行高及顶和底边距；

    2)常见的有<img>、<input>。   

&emsp;&emsp;**（2）position属性的值和作用；**   

&emsp;static 

    默认值，元素出现在正常的文档流中，不会受left、top、right、bottom的影响。

&emsp;relative 

    相对定位，相对自身位置定位，可通过设置left、top、right、bottom的值来设置位置；

    并且它原本所占的空间不变，即不会影响其他元素布局；

    经常被用来作绝对元素的容器块。

&emsp;absolute 

    绝对定位，相对于最近的除static定位以外的元素定位，若没有，则相对于html定位；

    脱离了文档流，不占据文档空间；

    若设置absolute，但没有设置top、left等值，其位置不变；

    若设置absolute，会影响未定义宽度的块级元素，使其变为包裹元素内容的宽度。

&emsp;fixed 

    固定定位 相对于浏览器窗口定位，脱离文档流，不会随页面滚动而变化。


#### 6. 浮动元素引起的问题和解决办法？绝对定位和相对定位，元素浮动后的display值。 

**（1）浮动元素引起的问题；** 
1.  由于浮动元素已脱离文档流，所以父元素无法被撑开，影响与父级元素同级的元素。  

2.  与浮动元素同级的非浮动元素（内联元素）会跟随其后，也是由于浮动元素脱离文档流，不占据s文档流中额位置。  
3. 如果该浮动元素不是同级第一个浮动的元素，则它之前的元素也应该浮动，否则容易影响页面的结构显示。  


**（2）解决方法；**   
1.  使用css样式中的clear：both可以用来解决上述问题中的2、3。
2.  给父元素添加clearfix样式，可以解决问题1，代码如下：

> 
    .clearfix:after{
        content: ".";       
        display: block;  
        height: 0;  
        clear: both;  
        visibility: hidden;
    }  
    
    .clearfix{
        display: inline-block; 
    } /* for IE/Mac */    
> 

3.  设置overflow为hidden或者auto。  

**（3）元素浮动后的display值；**  

&emsp;&emsp;元素设置了浮动后，无论是行内元素还是块元素，其display值会被重置为block。   

<br>  

#### 7. link和@import引入css的区别  

&emsp;&emsp;**（1）link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事务；@import属于CSS范畴，只能加载CSS；**    
&emsp;&emsp;**（2）link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载；**  
&emsp;&emsp;**（3）link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持；**  
&emsp;&emsp;**（4）link支持使用Javascript控制DOM去改变样式；而@import不支持；**    

<br>


