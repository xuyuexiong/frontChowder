### 前端大杂烩之HTML  
#### 1. HTML5新特性。 
&emsp;&emsp;**（1）语义特性（Semantic）；**  
&emsp;&emsp;**（2）本地存储特性（OFFLINE & STORAGE）；**  
&emsp;&emsp;**（3）设备访问特性 (DEVICE ACCESS)；**  
&emsp;&emsp;**（4）连接特性（CONNECTIVITY）；**  
&emsp;&emsp;**（5）网页多媒体特性(MULTIMEDIA)；**  
&emsp;&emsp;**（6）三维、图形及特效特性（3D, Graphics & Effects）；**  
&emsp;&emsp;**（7）性能与集成特性（Performance & Integration）；**  

引用链接：http://blog.csdn.net/gane_cheng/article/details/52819118  

**语义特性**：HTML5中的内容标签相互独立，级别不同，搜索引擎可以快速识别各部分内容，这些标签在新闻类、博客类的网站很有用。  
如果浏览器不支持最新的标签，最多的解决方法是这样的。

>   
    <section class="section">
        <!-- content --> 
    </section> 
    
    .section 
    {
     color: blue;
    }
>  

**本地存储特性**：HTML5提供了网页储存的API，方便Web应用离线使用。HTML5离线储存包括，**应用程序缓存（App Cache）、本地存储（Local Storage）、索引数据库（Indexed DB）、文件接口（File API ）**。    

**设备访问特性**：大致包括地理位置API、媒体访问API、访问联系人及事件、设备方向。   

**连接特性**：HTML5更高效的连接方案，**Web Sockets 和 Server-Sent Events**。  

**网页多媒体特性**：HTML5原生支持音视频**Audio 和 Video**。   

**三维、图形及特效特性**：HTML5支持**SVG, Canvas, WebGL, 和 CSS3 3D**。  

**性能与集成特性**：HTML5性能与集成特性主要包括两个东西，**Web Workers 和 XMLHttpRequest 2**。   
<br>  

#### 2. 浏览器的标准模式和怪异模式。  
&emsp;&emsp;由于历史的原因，各个浏览器在对页面的渲染上存在差异，甚至同一浏览器在不同版本中，对页面的渲染也不同。在W3C标准出台以前，浏览器在对页面的渲染上没有统一规范，产生了差异(Quirks mode或者称为Compatibility Mode)；由于W3C标准的推出，浏览器渲染页面有了统一的标准(CSScompat或称为Strict mode也有叫做Standars mode)，这就是二者最简单的区别。   
<br> 
#### 3. xhtml和html的区别。 
- XHTML元素必须被正确地嵌套。
- XHTML 元素必须被关闭。
- 标签名必须用小写字母。
- XHTML 文档必须拥有根元素。   

<br>     

#### 4. 使用data-的好处   
&emsp;&emsp;HTML5之前，我们必须依赖于class和rel属性来存储需要在网站中使用的数据片段，这种做法有时会在网站的外观和实用性之间产生冲突。而HTML 5 Data属性的存在就能很好满足需要。  
&emsp;&emsp;HTML5为前端开发者提供自定义的属性，这些属性集可以通过对象的dataset属性获取，不支持该属性的浏览器可以通过 getAttribute方法获取。  
<br> 

#### 5. meta标签  
&emsp;&emsp;<meta> 标签提供关于HTML文档的元数据。它不会显示在页面上，但是对于机器是可读的。可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。 
<br>

#### 6. canvas  
> &emsp;&emsp;<canvas>是一个可以使用脚本(通常为JavaScript)来绘制图形的 HTML 元素.它可以用于绘制图表、制作图片构图或者制作简单的(以及不那么简单的)动画。 
>    

引用链接：https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial
<br>  

#### 7. HTML5废弃的标签  
> 
    以下的 HTML4.01元素在HTML5中已经被删除:
    <acronym>
    <applet>
    <basefont>
    <big>
    <center>
    <dir>
    <font>
    <frame> //框架类元素
    <frameset> //框架类元素
    <noframes> //框架类元素
    <strike>
    <tt>
>  


#### 8. css js放置位置和原因  
&emsp;&emsp;script标签最好放在</body>标签的前面，因为放在所有body中的标签后面就不会出现网页加载时出现空白的情况，可以持续的给用户提供视觉反馈，同时在有些情况下，会降低错误的发生。  
&emsp;&emsp;而css标签应该放在<head></head>标签之间，因为如果放在</body>标签的前面，那么当DOM树构建完成了，渲染树才构建，那么当渲染树构建完成，浏览器不得不再重新渲染整个页面，这样造成了资源的浪费。效率也不高。如果放在<head></head>之间，浏览器边构建边渲染，效率要高的多。  
<br>  
#### 9. 什么是渐进式渲染  
&emsp;&emsp;为了优化HTML渲染过程，让服务器渲染局部，客户端渲染局部的方法。 

引用链接：https://segmentfault.com/a/1190000006830779?utm_source=hao.caibaojian.com   
<br> 

#### 10. html模板语言  
&emsp;&emsp;html有打开效率高的先天优势，但也有一个先天缺陷-不支持动态语言，这也是html模板语言出现的原因，让网站即享受html高效，又享受内容的动态化；例如php模板，需要php解析后，再由apache输出；aspx需要专用dll解析后，由IIS输出；jsp需要虚拟机解析后，由tomcat输出；   
<br>  
#### 11. meta viewport原理  
&emsp;&emsp;手机浏览器是把页面放在一个虚拟的“窗口”（viewport）中，通常这个虚拟的“窗口”（viewport）比屏幕宽，这样就不用把每个网页挤到很小的窗口中（这样会破坏没有针对手机浏览器优化的网页的布局），用户可以通过平移和缩放来看网页的不同部分。移动版的 Safari 浏览器最新引进了 viewport 这个 meta tag，让网页开发者来控制 viewport 的大小和缩放，其他手机浏览器也基本支持。  
&emsp;&emsp;三种viewport：layout viewport、visual viewport、ideal viewport。  
&emsp;&emsp;移动设备默认的viewport是layout viewport，但在进行移动设备网站的开发时，需要的是ideal viewport。要得到ideal viewport，需要用到meta标签。 
> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">    
>
