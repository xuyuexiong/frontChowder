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

#### 17. transition和animation的区别

&emsp;&emsp;animation属性类似于transition，他们都是随着时间改变元素的属性值，其主要区别在于： 

&emsp;&emsp;transition需要触发一个事件才会随着时间改变其CSS属性；  

&emsp;&emsp;animation在不需要触发任何事件的情况下，也可以显式的随时间变化来改变元素CSS属性，达到一种动画的效果；

#### 18. sass less  

&emsp;&emsp;Less和Sass在语法上有些共性，比如下面这些：

> &emsp;&emsp;1、混入(Mixins)——class中的class；  
&emsp;&emsp;2、参数混入——可以传递参数的class，就像函数一样；  
&emsp;&emsp;3、嵌套规则——Class中嵌套class，从而减少重复的代码；  
&emsp;&emsp;4、运算——CSS中用上数学；  
&emsp;&emsp;5、颜色功能——可以编辑颜色；  
&emsp;&emsp;6、名字空间(namespace)——分组样式，从而可以被调用；  
&emsp;&emsp;7、作用域——局部修改样式；  
&emsp;&emsp;8、JavaScript 赋值——在CSS中使用JavaScript表达式赋值。  

&emsp;&emsp;Less和Sass的不同之处  

&emsp;&emsp;**1、Less环境较Sass简单**  

&emsp;&emsp;Sass的安装需要安装Ruby环境，Less基于JavaScript，是需要引入Less.js来处理代码输出css到浏览器，也可以在开发环节使用Less，然后编译成css文件，直接放在项目中，有less.app、SimpleLess、CodeKit.app这样的工具，也有在线编辑地址。  

&emsp;&emsp;**2、从功能出发，Sass较Less略强大一些**   

&emsp;&emsp;&emsp;①sass有变量和作用域。  

&emsp;&emsp;&emsp;②sass有函数的概念；  

&emsp;&emsp;&emsp;③进程控制；  

&emsp;&emsp;&emsp;④数据结构；  

&emsp;&emsp;**3、Less与Sass处理机制不一样**

&emsp;&emsp;前者是通过客户端处理的，后者是通过服务端处理，相比较之下前者解析会比后者慢一点。  

&emsp;&emsp;**引用链接**：https://www.cnblogs.com/roashley/p/7731865.html