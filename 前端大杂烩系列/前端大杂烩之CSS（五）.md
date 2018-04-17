#### 14. 移动端布局方案

&emsp;1.&emsp;单位（rem）；  

&emsp;2.&emsp;使用<meta>标签中的viewport解决适配问题；

&emsp;3.&emsp;使用弹性布局盒子布局；  

#### 15. 清除浮动的原理  

&emsp;&emsp;主要有一个概念，Block formatting contexts （块级格式化上下文），简称 BFC。   

>   &emsp;如何触发BFC呢？   
    <br>
    1. float 除了none以外的值 
    <br>  
    2. overflow 除了visible 以外的值（hidden，auto，scroll ） 
    <br>  
    3. display (table-cell，table-caption，inline-block)   
    <br>
    4. position（absolute，fixed）   
    <br>
    5. fieldset元素     

#### 16. overflow:hidden有什么缺点？  

&emsp;&emsp;**优点**：不存在结构和语义化问题，代码量极少。  

&emsp;&emsp;**缺点**：内容增多时候容易造成不会自动换行导致内容被隐藏掉，无法显示需要溢出的元素。