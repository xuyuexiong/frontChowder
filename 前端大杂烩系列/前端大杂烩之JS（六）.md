#### 20. 图片滚动懒加载  

&emsp;**懒加载的意义（为什么要使用懒加载）**  

&emsp;&emsp;对于图片过多的页面，为了加速页面加载速度，很多时候我们需要将页面内未出现在可视区域内的图片先不做加载， 等到滚动到可视区域后再去加载。这样对于页面加载性能上会有很大的提升，也提高了用户体验。  

&emsp;**原理**  

&emsp;&emsp;图片滚动懒加载的原理非常简单：基于\<img>标签，在初次加载时，不把图片url放在src属性中，而是自定义一个属性，例如data-src。然后检测"scroll"，"resize"等窗体事件，判断图片是否进入了可视范围。如果进入，则将data-src的字段替换到src，此时浏览器会自动去加载对应图片资源。

&emsp;**实现**  

>  
    //原生JS方式
    var num = document.getElementsByTagName('img').length;
    var img = document.getElementsByTagName("img");
    var n = 0; //存储图片加载到的位置，避免每次都从第一张图片开始遍历
    lazyload(); //页面载入完毕加载可是区域内的图片
    window.onscroll = lazyload;
    function lazyload() { //监听页面滚动事件
        var seeHeight = document.documentElement.clientHeight; //可见区域高度
        var scrollTop = document.documentElement.scrollTop || document.body.scrollTop; //滚动条距离顶部高度
        for (var i = n; i < num; i++) {
            if (img[i].offsetTop < seeHeight + scrollTop) {
                if (img[i].getAttribute("src") == "default.jpg") {
                    img[i].src = img[i].getAttribute("data-src");
                }
                n = i + 1;
            }
        }
    }  
    
    //jQuery方式  
    var n = 0,
        imgNum = $("img").length,
        img = $('img');
    lazyload();
    $(window).scroll(lazyload);
    function lazyload(event) {
        for (var i = n; i < imgNum; i++) {
            if (img.eq(i).offset().top < parseInt($(window).height()) + parseInt($(window).scrollTop())) {
                if (img.eq(i).attr("src") == "default.jpg") {
                    var src = img.eq(i).attr("data-src");
                    img.eq(i).attr("src", src);
                    n = i + 1;
                }
            }
        }
    }   
    
&emsp;**节流函数进行性能优化**  

&emsp;&emsp;如果直接将函数绑定在scroll事件上，当页面滚动时，函数会被高频触发，这非常影响浏览器的性能。  

&emsp;&emsp;节流函数：只允许一个函数在N秒内执行一次。下面是一个简单的节流函数：  

>  
    // 简单的节流函数
    //fun 要执行的函数
    //delay 延迟
    //time  在time时间内必须执行一次
    function throttle(fun, delay, time) {
        var timeout,
            startTime = new Date();
        return function() {
            var context = this,
                args = arguments,
                curTime = new Date();
            clearTimeout(timeout);
            // 如果达到了规定的触发时间间隔，触发 handler
            if (curTime - startTime >= time) {
                fun.apply(context, args);
                startTime = curTime;
                // 没达到触发间隔，重新设定定时器
            } else {
                timeout = setTimeout(fun, delay);
            }
        };
    };
    // 实际想绑定在 scroll 事件上的 handler
    function lazyload(event) {}
    // 采用了节流函数
    window.addEventListener('scroll',throttle(lazyload,500,1000));  
    
&emsp;&emsp;**引用链接**：https://zhuanlan.zhihu.com/p/24057749?refer=dreawer  

#### 21. 深拷贝  

&emsp;JS中数据类型分为基本数据类型和引用数据类型，当我们需要拷贝一个变量时，引用数据类型的拷贝，只是复制了一个指针的指向，内存中并没有开辟一块新的内存空间，所以，如果需要对一个引用数据类型的变量进行拷贝，我们需要用深拷贝的方式来实现。  

&emsp;通常有下面两种方法实现深拷贝：

&emsp;&emsp;1.&emsp;迭代递归法  

&emsp;&emsp;2.&emsp;序列化反序列化法  

<br>

&emsp;**迭代递归法**  

&emsp;&emsp;这是最常规的方法，思想很简单：就是对对象进行迭代操作，对它的每个值进行递归深拷贝。（只能拷贝arr 和 obj 类型的变量）

&emsp;&emsp;**for...in 法**
>  
    // 迭代递归法：深拷贝对象与数组
    function deepClone(obj) {
        if (!isObject(obj)) {
            throw new Error('obj 不是一个对象！')
        }
    
        let isArray = Array.isArray(obj)
        let cloneObj = isArray ? [] : {}
        for (let key in obj) {
            cloneObj[key] = isObject(obj[key]) ? deepClone(obj[key]) : obj[key]
        }
    
        return cloneObj
    }  
    
&emsp;&emsp;**Reflect 法**  
>  
    // 代理法
    function deepClone(obj) {
        if (!isObject(obj)) {
            throw new Error('obj 不是一个对象！')
        }
    
        let isArray = Array.isArray(obj)
        let cloneObj = isArray ? [...obj] : { ...obj }
        Reflect.ownKeys(cloneObj).forEach(key => {
            cloneObj[key] = isObject(obj[key]) ? deepClone(obj[key]) : obj[key]
        })
    
        return cloneObj
    }

&emsp;**序列化反序列化法**  

&emsp;&emsp;也只能深拷贝对象和数组。

>  
    // 序列化反序列化法
    function deepClone(obj) {
        return JSON.parse(JSON.stringify(obj))
    }