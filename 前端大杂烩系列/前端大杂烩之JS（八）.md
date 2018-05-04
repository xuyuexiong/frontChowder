#### 28. typeof 和 instanceof 区别，instanceof原理  

&emsp;**typeof**  

&emsp;&emsp;typeof方法返回一个字符串，来表示数据的类型，但是数组、正则、日期、对象的typeof返回值都是object。所以用typeof方法来判断引用数据类型，是有一定误差的。  

&emsp;**instanceof**  

&emsp;&emsp;instanceof用于判断某个变量是否是某个对象的实例，返回值为true或false，当typeof无法判断某个对象是否是数组或者某个变量是否是对象的实例时，常用instanceof方法来判断。  

&emsp;**instanceof原理**  

&emsp;&emsp;instanceof运算符主要是判断某个构造函数的prototype属性是否存在于另外一个要检测对象的原型链上。   

#### 29. js动画和css3动画比较  

&emsp;**CSS动画**

&emsp;&emsp;优点：   

&emsp;&emsp;1、浏览器可以对动画进行优化。

&emsp;&emsp;&emsp;&emsp;浏览器使用与 requestAnimationFrame类似的机制，requestAnimationFrame比起setTimeout，setInterval设置动画的优势主要是:   

&emsp;&emsp;&emsp;&emsp;（1）requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成,并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率,一般来说,这个频率为每秒60帧。  

&emsp;&emsp;&emsp;&emsp;（2）在隐藏或不可见的元素中requestAnimationFrame不会进行重绘或回流，这当然就意味着更少的的cpu，gpu和内存使用量。

&emsp;&emsp;2、强制使用硬件加速 （通过 GPU 来提高动画性能）。  

&emsp;&emsp;3、代码相对简单,性能调优方向固定。  

&emsp;&emsp;4、对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码。  

&emsp;&emsp;缺点：

&emsp;&emsp;&emsp;&emsp;1、 运行过程控制较弱,无法附加事件绑定回调函数。CSS动画只能暂停,不能在动画中寻找一个特定的时间点，不能在半路反转动画，不能变换时间尺度，不能在特定的位置添加回调函数或是绑定回放事件,无进度报告。  

&emsp;&emsp;&emsp;&emsp;2、代码冗长。想用 CSS 实现稍微复杂一点动画,最后CSS代码都会变得非常笨重。  

&emsp;**JS动画**  

&emsp;&emsp;优点：  

&emsp;&emsp;&emsp;&emsp;1、JavaScript动画控制能力很强, 可以在动画播放过程中对动画进行控制：开始、暂停、回放、终止、取消都是可以做到的。  

&emsp;&emsp;&emsp;&emsp;2、动画效果比css3动画丰富,有些动画效果，比如曲线运动,冲击闪烁,视差滚动效果，只有JavaScript动画才能完成。  

&emsp;&emsp;&emsp;&emsp;3、CSS3有兼容性问题，而JS大多时候没有兼容性问题。  

&emsp;&emsp;缺点：  

&emsp;&emsp;&emsp;&emsp;1、JavaScript在浏览器的主线程中运行，而主线程中还有其它需要运行的JavaScript脚本、样式计算、布局、绘制任务等,对其干扰导致线程可能出现阻塞，从而造成丢帧的情况。  

&emsp;&emsp;&emsp;&emsp;2、代码的复杂度高于CSS动画。  

**引用链接**：https://www.cnblogs.com/simba-lkj/p/6139066.html  

