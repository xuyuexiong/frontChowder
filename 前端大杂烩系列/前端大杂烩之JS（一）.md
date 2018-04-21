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

  
