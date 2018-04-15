#### 8. grid布局  
&emsp;&emsp;CSS Grid 布局由两个核心组成部分是 wrapper（父元素）和 items（子元素）。 wrapper 是实际的 grid(网格)，items 是 grid(网格) 内的内容。  

> 首先，你必须使用 display: grid 将容器元素定义为一个 grid(网格) 布局，使用 grid-template-columns 和 grid-template-rows 设置 列 和 行 的尺寸大小，然后通过 grid-column 和 grid-row 将其子元素放入这个 grid(网格) 中。与 flexbox 类似，网格项（grid items）的源顺序无关紧要。你的 CSS 可以以任何顺序放置它们，这使得使用 媒体查询（media queries）重新排列网格变得非常容易。定义整个页面的布局，然后完全重新排列布局以适应不同的屏幕宽度，这些都只需要几行 CSS ，想象一下就让人兴奋。Grid(网格) 布局是有史以来最强大的CSS模块之一。  

<br>  

&emsp;&emsp;在深入了解 Grid(网格) 的概念之前，理解术语是很重要的。由于这里涉及的术语在概念上都很相似，如果不先记住 Grid(网格) 规范定义的含义，很容易混淆它们。但是别担心，术语并不多。

&emsp;&emsp;**1. 网格容器(Grid Container)**

&emsp;&emsp;应用 display: grid 的元素。这是所有网格项（Grid Items）的直接父级元素。在这个例子中，container 就是 网格容器(Grid Container)。

    HTML 代码:
    <div class="container">
      <div class="item item-1"></div>
      <div class="item item-2"></div>
      <div class="item item-3"></div>
    </div>  
    
&emsp;&emsp;**2. 网格项(Grid Item)**

&emsp;&emsp;网格容器（Grid Container）的子元素（例如直接子元素）。这里 item 元素就是网格项(Grid Item)，但是 sub-item 不是。

    HTML 代码:
    <div class="container">
      <div class="item"></div> 
      <div class="item">
        <p class="sub-item"></p>
      </div>
      <div class="item"></div>
    </div>
    
&emsp;&emsp;**3. 网格线(Grid Line)**

&emsp;&emsp;构成网格结构的分界线。它们既可以是垂直的（“列网格线(column grid lines)”），也可以是水平的（“行网格线(row grid lines)”），并位于行或列的任一侧。



&emsp;&emsp;**4. 网格轨道(Grid Track)**

&emsp;&emsp;两条相邻网格线之间的空间。你可以把它们想象成网格的列或行。



&emsp;&emsp;**5. 网格单元格(Grid Cell)**

&emsp;&emsp;两个相邻的行和两个相邻的列网格线之间的空间。这是 Grid(网格) 系统的一个“单元”。



&emsp;&emsp;**6. 网格区域(Grid Area)**

&emsp;&emsp;4条网格线包围的总空间。一个 网格区域(Grid Area) 可以由任意数量的 网格单元格(Grid Cell) 组成。


&emsp;**引用链接**：http://www.css88.com/archives/8510

<br>

#### 9. table布局的作用  

&emsp;table布局有两个特性：

-  同行等高  
-  宽度自动调节  

&emsp;使用table布局，可以轻松解决等高布局的问题。  

&emsp;**缺点:**

&emsp;1、 标签结构多，复杂 
> 
    我们可以从表格的结构来看
    <table>  
        <tr>  
            <td>内容1</td> 
        </tr> 
    </table> 
>

&emsp;从上面表格的结构标签来看，标签的对数较多，在表格布局中，主要是用到表格的相互嵌套使用，这样就会造成代码的复杂度更高！  

&emsp;2、 表格布局，不利于搜索引擎抓取信息，直接影响到网站的排名

&emsp;**优点:**

&emsp;1、结构位置更简单 

&emsp;2、容易上手 

&emsp;3、 数据化的存放更合理。   

<br>

#### 9. 实现两栏布局有哪些方法？  

&emsp;**1. 双inline-block方案:**  

>  
    .wrapper-inline-block {
        box-sizing: content-box;
        font-size: 0;    // 消除空格的影响
    }
    .wrapper-inline-block .left,
    .wrapper-inline-block .right {
        display: inline-block;
        vertical-align: top;    // 顶端对齐
        font-size: 14px;
        box-sizing: border-box;
    }
    .wrapper-inline-block .right {
        width: calc(100% - 140px);
    }  
>  

&emsp;&emsp;**缺点:**

&emsp;&emsp;1. 需要知道左侧盒子的宽度，两个盒子的距离，还要设置各个元素的box-sizing。  
&emsp;&emsp;2. 需要消除空格字符的影响。  
&emsp;&emsp;3. 需要设置vertical-align: top满足顶端对齐。

&emsp;**2. 双float方案:**  

> 
    .wrapper-double-float {
        overflow: auto;        // 清除浮动
        box-sizing: content-box;
    }
    .wrapper-double-float .left,
    .wrapper-double-float .right {
        float: left;
        box-sizing: border-box;
    }
    .wrapper-double-float .right {
        width: calc(100% - 140px);
    }
>   

&emsp;&emsp;**缺点:**  

&emsp;&emsp;1. 需要知道左侧盒子的宽度，两个盒子的距离，还要设置各个元素的box-sizing。  
&emsp;&emsp;2. 父元素需要清除浮动。

&emsp;**3. float+margin-left方案:**  

>  
    .wrapper-float {
        overflow: hidden;        // 清除浮动
    }
    .wrapper-float .left {
        float: left;
    }
    .wrapper-float .right {
        margin-left: 150px;
    }  
> 

&emsp;&emsp;**缺点:**   

&emsp;&emsp;1. 需要清除浮动。

&emsp;&emsp;2. 需要计算右侧盒子的margin-left  。

&emsp;**4. absolute+margin-left方案:**  

>  
    .wrapper-absolute .left {
        position: absolute;
    }
    .wrapper-absolute .right {
        margin-left: 150px;
    }  
>  

&emsp;&emsp;**缺点:**   

&emsp;&emsp;1. 使用了绝对定位，若是用在某个div中，需要更改父容器的position。

&emsp;&emsp;2. 没有清除浮动的方法，若左侧盒子高于右侧盒子，就会超出父容器的高度。因此只能通过设置父容器的min-height来放置这种情况。   

&emsp;**5. float+BFC方法:**   

> 
    .wrapper-float-bfc {
        overflow: auto;
    }
    .wrapper-float-bfc .left {
        float: left;
        margin-right: 20px;
    }
    .wrapper-float-bfc .right {
        margin-left: 0;
        overflow: auto;
    }  
>

&emsp;&emsp;**缺点:**   

&emsp;&emsp;1. 父元素需要清除浮动。

&emsp;**6. flex方案:**  

>  
    .wrapper-flex {
        display: flex;
        align-items: flex-start;
    }
    .wrapper-flex .left {
        flex: 0 0 auto;
    }
    .wrapper-flex .right {
        flex: 1 1 auto;
    }  
>  

&emsp;&emsp;**需要注意的是，flex容器的一个默认属性值:align-items: stretch;。这个属性导致了列等高的效果。为了让两个盒子高度自动，需要设置: align-items: flex-start;**    

&emsp;**7. grid方案:**  

>  
    .wrapper-grid {
        display: grid;
        grid-template-columns: 120px 1fr;
        align-items: start;
    }
    .wrapper-grid .left,
    .wrapper-grid .right {
        box-sizing: border-box;
    }
    .wrapper-grid .left {
        grid-column: 1;
    }
    .wrapper-grid .right {
        grid-column: 2;
    }  
>  

&emsp;&emsp;**注意:**

&emsp;&emsp;**grid布局也有列等高的默认效果。需要设置: align-items: start;。**

&emsp;&emsp;**grid布局还有一个值得注意的小地方和flex不同:在使用margin-left的时候，grid布局默认是box-sizing设置的盒宽度之间的位置。而flex则是使用两个div的border或者padding外侧之间的距离。**

<br>

&emsp;&emsp;**引用链接：** https://segmentfault.com/a/1190000010698609
