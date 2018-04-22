#### 1. js的基本类型有哪些？引用类型有哪些？null和undefined的区别  

&emsp;**基本类型**：Number,String,Boolean,Null,undefined。指的就是保存在栈内存中的简单数据段。

&emsp;**引用类型**：Object,Array,Date,RegExp,Function。存储在堆（heap）中的对象，也就是说，存储在变量处的值是一个指针（point），指向存储对象的内存处。

&emsp;**null和undefined的区别**：

&emsp;&emsp;1、null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。Null表示“没有对象”，即该处不应该有值。典型的用法是：

&emsp;&emsp;（1）作为函数的参数，表示该函数的参数不是对象。

&emsp;&emsp;（2）作为对象原型链的终点。

&emsp;&emsp;2、当声明的变量还未被初始化时，变量的默认值为undefined，undefined表示“缺少值”，就是此处应该有一个值，但是还没有定义。

&emsp;&emsp;（1）  变量被声明了，但没有赋值时，就等于undefined。

&emsp;&emsp;（2）  调用函数时，应该提供的参数没有提供，该参数就等于undefined。

&emsp;&emsp;（3）  对象没有赋值的属性，该属性的值为undefined。

&emsp;&emsp;（4）  函数没有返回值时，默认返回undefined。  

#### 2. 如何判断一个变量是Array类型？如何判断一个变量是Number类型？  

&emsp;**判断一个变量是Array类型**

&emsp;&emsp;1、从原型入手，Array.prototype.isPrototypeOf(obj);  

&emsp;&emsp;&emsp;利用isPrototypeOf()方法，判定Array是不是在obj的原型链中，如果是，则返回true,否则false。  

&emsp;&emsp;2、也可以从构造函数入手，obj instanceof Array  

&emsp;&emsp;&emsp;typeof 和 instanceof 的区别是两者都可以用来判断变量，typeof会返回基本类型，可以用typeof a != 'undefined' 判断a变量存在。而instanceof只会返回一个布尔值。  

&emsp;&emsp;3、根据对象的class属性(类属性)，跨原型链调用toString()方法。

&emsp;&emsp;&emsp;js中提供了，调用对象原型中的toString方法， Object.prototype.toString.call(obj)；因为很多对象继承的toString（）方法被重写了，为了能够调用正确的toString（）版本，也就是最原始的版本。可以使用Function.call()的方法，其中call可以这么理解，相当于obj去借用这个Object.prototype.toString();  

&emsp;&emsp;4、Array.isArray()方法。  

&emsp;&emsp;&emsp;在MDN中就比较了isArray和instanceof的区别，当Array.isArray()不可用的使用，MDN做了如下的补丁，说明还是比较推荐使用前面讲的第三种方法 Object.prototype.toString.call(obj)。  

&emsp;**判断一个变量是Number类型**  

&emsp;&emsp;typeof()判断

&emsp;&emsp;&emsp;typeof(num)==="number")&&(num!==Infinity)&&!isNaN(num)  

#### 3. JS常见的dom操作api  

&emsp;**节点创建型api**

&emsp;&emsp;创建型api主要包括createElement，createTextNode，cloneNode和createDocumentFragment四个方法，需要注意下面几点：  

&emsp;&emsp;（1）它们创建的节点只是一个孤立的节点，要通过appendChild添加到文档中。  
&emsp;&emsp;（2）cloneNode要注意如果被复制的节点是否包含子节点以及事件绑定等问题。  
&emsp;&emsp;（3）使用createDocumentFragment来解决添加大量节点时的性能问题。  

&emsp;**页面修改型API**  

&emsp;&emsp;页面修改型api主要包括appendChild，insertBefore，removeChild，replaceChild，要注意几个特点：  
&emsp;&emsp;（1）不管是新增还是替换节点，如果新增或替换的节点是原本存在页面上的，则其原来位置的节点将被移除，也就是说同一个节点不能存在于页面的多个位置。  
&emsp;&emsp;（2）节点本身绑定的事件会不会消失，会一直保留着。  

&emsp;**节点查询型API**  

&emsp;&emsp;节点查询型API主要包括document.getElementById，document.getElementsByTagName，document.getElementsByName，document.getElementsByClassName，document.querySelector和document.querySelectorAll这六个方法。  

&emsp;**节点关系型api**   

&emsp;&emsp;（1）父关系型api  

&emsp;&emsp;parentNode：每个节点都有一个parentNode属性，它表示元素的父节点。Element的父节点可能是Element，Document或DocumentFragment。  
&emsp;&emsp;parentElement：返回元素的父元素节点，与parentNode的区别在于，其父节点必须是一个Element，如果不是，则返回null。  

&emsp;&emsp;（2）兄弟关系型api

&emsp;&emsp;previousSibling：节点的前一个节点，如果该节点是第一个节点，则为null。注意有可能拿到的节点是文本节点或注释节点，与预期的不符，要进行处理一下。  
&emsp;&emsp;previousElementSibling：返回前一个元素节点，前一个节点必须是Element，注意IE9以下浏览器不支持。  
&emsp;&emsp;nextSibling：节点的后一个节点，如果该节点是最后一个节点，则为null。注意有可能拿到的节点是文本节点，与预期的不符，要进行处理一下。  
&emsp;&emsp;nextElementSibling：返回后一个元素节点，后一个节点必须是Element，注意IE9以下浏览器不支持。  

&emsp;&emsp;（3）子关系型api  

&emsp;&emsp;childNodes：返回一个即时的NodeList，表示元素的子节点列表，子节点可能会包含文本节点，注释节点等。  
&emsp;&emsp;children：一个即时的HTMLCollection，子节点都是Element，IE9以下浏览器不支持。  
&emsp;&emsp;firstNode：第一个子节点。  
&emsp;&emsp;lastNode：最后一个子节点。  
&emsp;&emsp;hasChildNodes方法：可以用来判断是否包含子节点。  

&emsp;**元素属性型api**  

&emsp;&emsp;（1）setAttribute  

&emsp;&emsp;setAttribute：根据名称和值修改元素的特性。

&emsp;&emsp;（2）getAttribute

&emsp;&emsp;getAttribute返回指定的特性名相应的特性值，如果不存在，则返回null或空字符串。  

&emsp;**元素样式型api**  

&emsp;&emsp;（1）window.getComputedStyle

&emsp;&emsp;window.getComputedStyle是用来获取应用到元素后的样式，假设某个元素并未设置高度而是通过其内容将其高度撑开，这时候要获取它的高度就要用到getComputedStyle。  

&emsp;&emsp;（2）getBoundingClientRect

&emsp;&emsp;getBoundingClientRect用来返回元素的大小以及相对于浏览器可视窗口的位置。  

#### 4. 事件冒泡和事件捕获  

&emsp;&emsp;（1）捕获阶段（Capture Phase）

&emsp;&emsp;事件的第一个阶段是捕获阶段。事件从文档的根节点流向目标对象节点。途中经过各个层次的DOM节点，并在各节点上触发捕获事件，直到到达事件的目标节点。捕获阶段的主要任务是建立传播路径，在冒泡阶段，事件会通过这个路径回溯到文档跟节点。

&emsp;&emsp;（2）目标阶段（Target Phase）

&emsp;&emsp;当事件到达目标节点的，事件就进入了目标阶段。事件在目标节点上被触发，然后会逆向回流，直到传播至最外层的文档节点。

&emsp;&emsp;（3）冒泡阶段（Bubble Phase）

&emsp;&emsp;事件在目标元素上触发后，并不在这个元素上终止。它会随着DOM树一层层向上冒泡，回溯到根节点。
冒泡过程非常有用。它将我们从对特定元素的事件监听中释放出来，如果没有事件冒泡，我们需要监听很多不同的元素来确保捕获到想要的事件。
