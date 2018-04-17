#### 1. 盒模型，box-sizing
&emsp;&emsp;CSS中的盒模型一般分为标准W3C盒模型和IE盒模型。在标准盒模型中，width 和 height 指的是内容区域的宽度和高度。而在IE盒模型中，内容区域的宽度和高度还包括了边框、内边距。  
&emsp;&emsp;在CSS3中新增加了box-sizing属性，能够事先定义盒模型的尺寸解析方式。border-box重新定义CSS2.1中盒模型组成的模式，让元素维持IE传统的盒模型（IE6以下版本和IE6-7怪异模式）。   
#### 2. CSS3新特性  
&emsp;&emsp;**（1）CSS3选择器；**  

&emsp;&emsp;**（2）CSS3 边框；**  

&emsp;用CSS3，你可以创建圆角边框，添加阴影框，并作为边界的形象而不使用设计程序  
&emsp;&emsp;**（3）CSS3 背景；** 

&emsp;CSS3中包含几个新的背景属性，提供更大背景元素控制。  
&emsp;&emsp;**（4）CSS3 渐变；**  

&emsp;CSS3 定义了两种类型的渐变(线性渐变-向下/向上/向左/向右/对角方向、径向渐变-由它们的中心定义）  
&emsp;&emsp;**（5）CSS3 文本效果；**  

&emsp;&emsp;**（6）CSS3 字体；**  

&emsp;使用CSS3，可以使用喜欢的任何字体。当要使用字体文件时，只需简单的将字体文件包含在网站中，它会自动下载给需要的用户。您所选择的字体在新的CSS3版本有关于@font-face规则描述。您"自己的"的字体是在 CSS3 @font-face 规则中定义的。  
&emsp;&emsp;**（7）CSS3 转换和变形；** 

&emsp;&emsp;**（8）CSS3 过渡；** 

&emsp;&emsp;**（9）CSS3 动画；**  

&emsp;要创建CSS3动画，你需要了解@keyframes规则。@keyframes规则是创建动画。 @keyframes规则内指定一个CSS样式和动画将逐步从目前的样式更改为新的样式。  
&emsp;&emsp;**（10）CSS3 多列；**  

&emsp;&emsp;**（11）CSS3 盒模型；**  

&emsp;在 CSS3 中, 增加了一些新的用户界面特性来调整元素尺寸，框尺寸和外边框，resize属性指定一个元素是否应该由用户去调整大小。box-sizing属性允许您以确切的方式定义适应某个区域的具体内容。outline-offset属性对轮廓进行偏移，并在超出边框边缘的位置绘制轮廓。  
&emsp;&emsp;**（12）CSS3 多媒体查询；**  

<br> 

#### 3. 伪类，伪元素 
&emsp;&emsp;**CSS 引入伪类和伪元素的概念是为了实现基于文档树之外的信息的格式化**  
- 伪类：用于向某些选择器添加特殊的效果  
- 伪元素：用于将特殊的效果添加到某些选择器   

<br>  

#### 4.CSS实现隐藏页面的方式  
&emsp;&emsp;**（1）Opacity**  

&emsp;&emsp;opacity 属性的意思是设置一个元素的透明度。它不是为改变元素的边界框（bounding box）而设计的。这意味着将 opacity 设为 0 只能从视觉上隐藏元素。而元素本身依然占据它自己的位置并对网页的布局起作用。它也将响应用户交互。 
> 
    .hide {
        opacity: 0;
    }  
>  

&emsp;&emsp;**（2）Visibility**  

&emsp;&emsp;第二个要说的属性是 visibility。将它的值设为 hidden 将隐藏我们的元素。如同 opacity 属性，被隐藏的元素依然会对我们的网页布局起作用。与 opacity 唯一不同的是它不会响应任何用户交互。此外，元素在读屏软件中也会被隐藏。

&emsp;&emsp;这个属性也能够实现动画效果，只要它的初始和结束状态不一样。这确保了 visibility 状态切换之间的过渡动画可以是时间平滑的（事实上可以用这一点来用 hidden 实现元素的）。  
> 
    .hide {
        visibility: hidden;
    }  
>  

&emsp;&emsp;**（3）Display**  

&emsp;&emsp;display 属性依照词义真正隐藏元素。将 display 属性设为 none 确保元素不可见并且连盒模型也不生成。使用这个属性，被隐藏的元素不占据任何空间。不仅如此，一旦 display 设为 none 任何对该元素直接打用户交互操作都不可能生效。此外，读屏软件也不会读到元素的内容。这种方式产生的效果就像元素完全不存在。

&emsp;&emsp;任何这个元素的子孙元素也会被同时隐藏。为这个属性添加过渡动画是无效的，它的任何不同状态值之间的切换总是会立即生效。

&emsp;&emsp;不过请注意，通过 DOM 依然可以访问到这个元素。因此你可以通过 DOM 来操作它，就像操作其他的元素。 
> 
    .hide {
        display: none;
    }  
>   

&emsp;&emsp;**（4）Position**   

&emsp;&emsp;假设有一个元素你想要与它交互，但是你又不想让它影响你的网页布局，没有合适的属性可以处理这种情况（opacity 和 visibility 影响布局， display 不影响布局但又无法直接交互）。在这种情况下，你只能考虑将元素移出可视区域。这个办法既不会影响布局，有能让元素保持可以操作。下面是采用这种办法的 CSS：

> 
    .hide {
       position: absolute;
       top: -9999px;
       left: -9999px;
    } 
>  

&emsp;&emsp;**（5）Clip-path**   

&emsp;&emsp;隐藏元素的另一种方法是通过剪裁它们来实现。这可以通过 clip 属性来实现，但是这个属性被废弃了，换成一个更好的属性叫做 clip-path。

&emsp;&emsp;记住，clip-path 属性还没有被IE或Edge完全支持。如果要在你的 clip-path 中使用外部的 SVG 文件，浏览器支持度还要更低。使用 clip-path 属性来隐藏元素的代码看起来如下：

> 
    .hide {
      clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);
    } 
>   


&emsp;&emsp;引用链接：https://blog.csdn.net/xtzz92/article/details/51967601