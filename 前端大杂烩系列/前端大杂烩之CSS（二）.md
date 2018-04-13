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

