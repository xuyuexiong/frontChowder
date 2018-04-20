#### 19. 如何创建BFC？解决什么问题？  

&emsp;BFC（边距重叠解决方案）  
&emsp;&emsp;1、BFC的基本概念： 块级格式化上下文；  

&emsp;&emsp;2、BFC的原理：BFC的渲染规则  
&emsp;&emsp;&emsp;①：在BFC这个元素的垂直方向的边距会发生重叠。  
&emsp;&emsp;&emsp;②：BFC的区域不会与浮动元素的box重叠。  
&emsp;&emsp;&emsp;③：BFC在页面上是一个独立的容器，外面的元素不会影响里面的元素，里面的元素也不会影响外面的元素  
&emsp;&emsp;&emsp;④：计算BFC高度时，浮动元素也会参与计算  

&emsp;&emsp;3、如何创建BFC  
&emsp;&emsp;&emsp;①：float不为none。  
&emsp;&emsp;&emsp;②：position不为static或者relative。  
&emsp;&emsp;&emsp;③：display为inline-block或者是table相关的。  
&emsp;&emsp;&emsp;④：overflow不为visible。  

&emsp;&emsp;4、BFC的使用场景  
&emsp;&emsp;&emsp;①：解决垂直方向的边距重叠。  
&emsp;&emsp;&emsp;②：清除浮动。  
&emsp;&emsp;&emsp;③：不与浮动元素重叠。    

#### 20. CSS选择器的优先级是怎样的  

&emsp;**不同级别**

&emsp;&emsp;1.&emsp;在属性后面使用 !important 会覆盖页面内任何位置定义的元素样式。  
&emsp;&emsp;2.&emsp;作为style属性写在元素内的样式  
&emsp;&emsp;3.&emsp;id选择器  
&emsp;&emsp;4.&emsp;类选择器  
&emsp;&emsp;5.&emsp;标签选择器  
&emsp;&emsp;6.&emsp;通配符选择器  
&emsp;&emsp;7.浏览器自定义或继承&emsp;&emsp;  

&emsp;总结排序：!important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性

&emsp;**同一级别**

&emsp;&emsp;同一级别中后写的会覆盖先写的样式。  

#### 21. 雪碧图   

&emsp;雪碧图也叫CSS精灵， 是一项CSS图像合成技术  

&emsp;不使用雪碧图， 单纯调用小图片有以下优缺点：  

&emsp;优点：调用简单、维护方便；   
&emsp;缺点：请求文件过多、引发性能问题；  

&emsp;**雪碧图实现**  

&emsp;1： CSS Gaga  

&emsp;2：photoShop  

&emsp;3：gulp  

&emsp;4：webpack   

&emsp;除了 gulp 跟 webpack 外，还有国产前端部署的解决方案FIS3, 其对小图标也有一套部署配置流程。

#### 22.“::before”和“:after”中的双冒号和单冒号的区别  

&emsp;&emsp;伪元素由双冒号和伪元素名称组成。双冒号是在当前规范中引入的，用于区分伪类和伪元素。

&emsp;&emsp;伪类偏向于元素的动作行为，伪元素偏向于元素的属性。实际上 css3 为了区分两者，已经明确规定了伪类用一个冒号来表示，而伪元素则用两个冒号来表示。对于CSS2之前已有的伪元素，比如:before，单冒号和双冒号的写法::before作用是一样的。 