#### 11. css dpi 和 ppi 
&emsp;1.  dpi：(dot per inch)每英寸多少点，该值越高，则图片越细腻，用于打印；  

&emsp;&emsp;DPI是Dots Per Inch（每英寸所打印的点数）的缩写，是打印机、鼠标等设备分辨率的单位。这是衡量打印机打印精度的主要参数之一，一般来说，该值越大，表明打印机的打印精度越高。     

&emsp;&emsp;**注意**：DPI是手机图片输出的一个衡量标准，一般用于图片打印时调节参数。针对特定的图像而言，图像的像素数是固定的，所以，打印分辨率和打印尺寸便呈现反比的关系。

&emsp;2.  ppi: (pixel per inch)每英寸像素数，该值越高，则屏幕越细腻，用于计算机和电视屏幕上每英寸显示的像素点的数量；  

&emsp;&emsp;PPI(像素密度)是指屏幕上的像素密度，其计算方法为： 
ppi= 屏幕对角线上的像素点数/对角线长度 = √ （屏幕横向像素点^2 + 屏幕纵向像素点^2）/对角线长度；   

#### 12. attribute和property的区别  

- property是DOM中的属性，是JavaScript里的对象；
- attribute是HTML标签上的特性，它的值只能够是字符串；    

&emsp;&emsp;常用的Attribute，例如id、class、title等，已经被作为Property附加到DOM对象上，可以和Property一样取值和赋值。但是自定义的Attribute，就不会有这样的特殊优待，例如：

        <div id="div1" class="divClass" title="divTitle" title1="divTitle1">100</div>  
&emsp;&emsp;这个div里面的“title1”就不会变成Property。

&emsp;1.&emsp;property能够从attribute中得到同步；  

&emsp;2.&emsp;attribute不会同步property上的值；  

&emsp;3.&emsp;attribute和property之间的数据绑定是单向的，attribute->property；  

&emsp;4.&emsp;更改property和attribute上的任意值，都会将更新反映到HTML页面中；   

#### 13. 流式布局如何实现，响应式布局如何实现   

&emsp;**流式布局（Liquid Layout）**  

&emsp;&emsp;流式布局（Liquid）的特点（也叫"Fluid") 是页面元素的宽度按照屏幕分辨率进行适配调整，但整体布局不变。代表作栅栏系统（网格系统）。

&emsp;&emsp;网页中主要的划分区域的尺寸使用百分数（搭配min-*、max-*属性使用），例如，设置网页主体的宽度为80%，min-width为960px。图片也作类似处理（width:100%, max-width一般设定为图片本身的尺寸，防止被拉伸而失真）。   

&emsp;&emsp;**1. 布局特点**

&emsp;&emsp;屏幕分辨率变化时，页面里元素的大小会变化而但布局不变。【这就导致如果屏幕太大或者太小都会导致元素无法正常显示。   

&emsp;&emsp;**2. 设计方法**

&emsp;&emsp;使用%百分比定义宽度，高度大都是用px来固定住，可以根据可视区域 (viewport) 和父元素的实时尺寸进行调整，尽可能的适应各种分辨率。往往配合 max-width/min-width 等属性控制尺寸流动范围以免过大或者过小影响阅读。  

&emsp;&emsp;这种布局方式在Web前端开发的早期历史上，用来应对不同尺寸的PC屏幕（那时屏幕尺寸的差异不会太大），在当今的移动端开发也是常用布局方式，但缺点明显：主要的问题是如果屏幕尺度跨度太大，那么在相对其原始设计而言过小或过大的屏幕上不能正常显示。因为宽度使用%百分比定义，但是高度和文字大小等大都是用px来固定，所以在大屏幕的手机下显示效果会变成有些页面元素宽度被拉的很长，但是高度、文字大小还是和原来一样（即，这些东西无法变得“流式”），显示非常不协调  

&emsp;**响应式布局（Responsive Layout）**   

&emsp;&emsp;随着CSS3出现了媒体查询技术，又出现了响应式设计的概念。响应式设计的目标是确保一个页面在所有终端上（各种尺寸的PC、手机、手表、冰箱的Web浏览器等等）都能显示出令人满意的效果，对CSS编写者而言，在实现上不拘泥于具体手法，但通常是糅合了流式布局+弹性布局，再搭配媒体查询技术使用。——分别为不同的屏幕分辨率定义布局，同时，在每个布局中，应用流式布局的理念，即页面元素宽度随着窗口调整而自动适配。即：创建多个流体式布局，分别对应一个屏幕分辨率范围。可以把响应式布局看作是流式布局和自适应布局设计理念的融合。  

&emsp;&emsp;**1. 布局特点**

&emsp;&emsp;每个屏幕分辨率下面会有一个布局样式，即元素位置和大小都会变。

&emsp;&emsp;**2. 设计方法**

&emsp;&emsp;媒体查询+流式布局。通常使用 @media 媒体查询 和网格系统 (Grid System) 配合相对布局单位进行布局，实际上就是综合响应式、流动等上述技术通过 CSS 给单一网页不同设备返回不同样式的技术统称。

&emsp;&emsp;**优点**：适应pc和移动端，如果足够耐心，效果完美。

&emsp;&emsp;**缺点**：（1）媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。（2）要匹配足够多的屏幕大小，工作量不小，设计也需要多个版本。