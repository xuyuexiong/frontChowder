#### 1. 谈一谈Promise  

&emsp;&emsp;Promise是ES6中几个重要特性之一，这里不详细展开，只简单介绍一下Promise的几个用法和作用，想更深入的了解，可以去看其他的ES6文档。

&emsp;&emsp;Promise对象可以理解为执行的一次异步操作，只是它可以用链式的方式来编写代码，而不用像以往嵌套那样，一层一层的写回调函数。  

&emsp;**Promise对象的特点：**

&emsp;&emsp;1、对象的状态不受外界影响。  

&emsp;&emsp;&emsp;&emsp;Promise对象代表一个异步操作，有三种状态：  

&emsp;&emsp;&emsp;&emsp;——Pending（执行中）  

&emsp;&emsp;&emsp;&emsp;——Resolved（成功，又称Fulfilled）  

&emsp;&emsp;&emsp;&emsp;——Rejected（拒绝）  

&emsp;&emsp;其中Pending为初始状态，Resolved和Rejected为结束状态（结束状态表示Promise的生命周期已结束）。

&emsp;&emsp;Promise只有异步操作的结果可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。  

&emsp;&emsp;2、一旦状态改变，就不会再变，任何时候都可以得到这个结果。  

&emsp;&emsp;Promise对象的状态改变，只有两种可能：从Pending变为Resolved和从Pending变为Rejected。只要这两种情况发生，状态就不会再发生改变了。  

&emsp;**Promise对象的缺点：**  

&emsp;&emsp;1、无法中止Promise，只要新建了一个Promise对象，它就会立即执行，无法中途取消。

&emsp;&emsp;2、如果不设置Rejected函数，Promise内部抛出的错误，在外部无法接收。

&emsp;&emsp;3、当处于Pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。  

&emsp;**Promise对象的基本使用：**  

&emsp;&emsp;1、先new一个Promise对象，将Promise实例化；

&emsp;&emsp;2、实例化的Promise可以传两个参数，一个是成功的回调函数Resolve，一个是失败的回调函数Reject；

&emsp;&emsp;3、Promise实例生成以后，可以用then方法调用Resolve函数，catch方法调用Reject函数；  

>  
    var promise = function(isReady){
        return new Promise(function(resolve, reject){
            // do somthing, maybe async
            if (isReady){
              return resolve('hello world');
            } else {
              return reject('failure');
            }
        });
    }
    promise(true)
    .then(function(value){
        console.log('resolved');
        console.log(value);
        console.log(haha); //此处的haha未定义
    })
    .catch(function(error){
        console.log('rejected');
        console.log(error);
    });

#### 2. es6的继承和es5的继承有什么区别

&emsp;&emsp;不论是ES6也好，和ES5一样，本质上都是通过原型链来实现继承，只是ES6封装了更优雅简洁的api，修改了一些属性指向，规范了继承的操作，使得JS的继承更加高效。  

&emsp;**es6中的class**

>  
    class Super() {
        constructor(props = { name: 'eric' }) {
            this.name = props.name;
        }
        setName(name) {
            this.name = name;
        }
        getName() {
            return this.name;
        }
    }
    class Sub extends Super {
        constructor(props) {
            super(props = { sex: 'male' }); // 创建实例，继承父类属性和方法
            this.sex = props.sex;
        }
    }
    let sub1 = new Sub({
        name: 'eric',
        sex: 'male'
    })
    let sub2 = new Sub({
        name: 'eric',
        sex: 'female'
    })
    sub1.setName('ada');
    console.log(sub1.getName(),sub2.getName()) // ada,eric,属性没复用，各自实例都有自己的属性。
    console.log(sub1.getName === sub2.getName) // true; 复用了父类的方法
    console.log(Sub.prototype.sex) // undefined
    // 子类原型对象上没有父类构造函数中赋值的属性，不是组合式继承

#### 3. Promise封装ajax  

&emsp;ajax的简单实现  

>  
    // 简略实现ajax
    function ajax(url,type){
        return new Promise((resolve,reject) => {
            var XHR = new XHRHttpRequest();
            XHR.open(type,url,true);
            XHR.send();
            XHR.onreadystatechange = () => {
                if(XHR.readyState == 4) {
                    if(XHR.status == 200) {
                        try {
                            let response = JSON.parse(XHR.responseText);
                            resolve(response);
                        } catch(e) {
                            reject(e);
                        }
                    } else {
                        reject(new Error(XHR.statusText));
                    }
                }
            }
        });
    }  
    
#### 4. let const的优点  

&emsp;**Let 的优点**  

&emsp;&emsp;1、不存在变量提升，即变量不能再其声明之前使用;  

&emsp;&emsp;2、暂时性死区，在块级作用域内存在 let 命令 ，他所声明的变量就绑定到这个区域，不在受其他情况的影响。  

&emsp;&emsp;3、不能重复声明;  

&emsp;&emsp;4、块级作用域

&emsp;**const 的优点**  

&emsp;&emsp;1、一旦声明，其值就不能更改；

&emsp;&emsp;2、与let相似的一系类优点；  