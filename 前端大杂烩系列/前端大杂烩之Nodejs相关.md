#### 1. nodeJs概要  

&emsp;&emsp;nodeJS之所以能在后端运行，得归功于V8引擎，通过对高性能V8引擎的封装，并通过一系列优化的API类库，使其能够在后端运行。  

&emsp;&emsp;nodeJs有两大特点：

&emsp;&emsp;1、基于事件驱动；

&emsp;&emsp;2、无阻塞；  

&emsp;&emsp;nodeJs其本质就是JavaScript，所以基于事件驱动不难理解。能做到无阻塞，是nodeJs通过大量的回调函数来达到这一目的。