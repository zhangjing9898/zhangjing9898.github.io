---
layout: post
title: "H5 web workers（多线程）"
date: 2018-04-23
categories:
  - Juice
description: 
image: https://unsplash.it/2000/1200?image=36
image-sm: https://unsplash.it/2000/1200?image=36
---

#介绍
- web workers是HTML5提供的一个JavaScript多线程解决方案
- 我们可以将一些大计算量的代码交由web worker运行而不冻结用户界面
- 但是子线程完全受主线程控制，且不得操作dom。所以，这个新标准并没有改变JavaScript单线程的本质。

--------
###相关：
1.h5规范提供了js分线程的实现，取名为web workers
2.相关API
   - woker：构造函数，加载分线程执行的js文件
   - Woker.prototype.onmessage:用于接收另一个线程的回调函数
   - Woker.prototype.postMessage:向另一个线程发送消息
3. 不足
  * worker内代码不能操作DOM(更新UI)
  * 不能跨域加载JS
  * 不是每个浏览器都支持这个新特性
--------
#使用
- 创建在分线程执行的js文件
- 在主线程中的js中发消息并设置回调
```
	<input type="text" id="number" value="30">
		<button id="btn1">主线程计算fibonacci值</button>
		<button id="btn2">分线程计算fibonacci值</button>

		<script type="text/javascript">
			var worker = new Worker("./worker·2.js");
			document.getElementById("btn2").onclick = function() {
				var inputVal = document.getElementById("number").value;
				worker.postMessage(inputVal);
				worker.onmessage = function(event) {
					console.log(event.data);
				}
			}
		</script>
```
worker2.js:
```
var fibonacci =function(n) {
    return n <2 ? n : fibonacci(n -1) + fibonacci(n -2);
};

var onmessage = function(event) {
	console.log(event);
    var n = parseInt(event.data, 10);
    postMessage(fibonacci(n));
};
```
贴上相关API
分线程接收
```
var onmessage =function (event){ //不能用函数声明
    console.log('onMessage()22');
    var upper = event.data.toUpperCase();//通过event.data获得发送来的数据
    postMessage( upper );//将获取到的数据发送会主线程
}
```
在主线程设置
```
创建一个Worker对象并向它传递将在新线程中执行的脚本的URL
var worker = new Worker("worker.js");  
//接收worker传过来的数据函数
worker.onmessage = function (event) {     
    console.log(event.data);             
};
//向worker发送数据
worker.postMessage("hello world");    
```
相应图解：
![image.png](https://upload-images.jianshu.io/upload_images/3378252-5772770b4751206f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
