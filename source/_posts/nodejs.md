---
title: 【教程】Node.js
date: 2016-08-05
tags: [教程,JavaScript,Nodejs]
categories: Nodejs
---
# 一、Node.js创建第一个应用 #
Node.js应用的组成部分：
- 引入required模块；
- 创建服务器；
- 接收请求与响应请求；

# 二、NPM 使用介绍 #
npm是NodeJS的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景如下：
- 允许用户从NPM服务器下载别人编写的第三方包到本地使用；
- 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用；
- 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用；
<!-- more -->
# 三、Node.jsREPL（交互式解释器） #
Node自带了交互式解释器，可以执行以下任务：
- 读取：读取用户数据，解析输入了JavaScript数据结构并存储在内存中；
- 执行：执行输入的数据结构；
- 打印：输出结果；
- 循环：循环操作以上步骤知道用户两次按下ctrl+c或者直接按下ctrl+d按钮退出；

# 四、Node.js回调函数 #
Node.js异步编程的直接体现就是回调；异步编程依托于回调来实现，Node使用了大量的回调函数，Node所有的API都支持回调函数；

# 五、Node.js 事件循环 #
Node.js是单进程单线程应用程序，但是通过事件和回调支持并发，所以性能非常高；   
Node.js的每一个API都是异步的，并作为一个独立线程运行，使用异步函数调用，并处理并发；    
Node.js基本上所有事件机制都是用设计模式中观察者模式实现；    
Node.js单线程类似进入一个while（true）的事件循环，直到没有事件观察者退出，每个异步事件都生成一个事件观察者，如果有事件发生就调用该回调函数；

# 六、Node.js EventEmitter #
Node.js所有的异步I/O操作在完成时都会发送一个事件打牌事件列队；    
Node.js里面的许多对象都会分发事件：一个net.Server对象会在每次有新连接时分发一个事件，一个fs.readStream对象会在文件被打开的时候发出一个事件，所有这些产生事件的对象都是events.EventEmitter的实例；

# 七、Node.js Buffer(缓冲区) #
JavaScript语言 自身只有字符串数据类型，没有二进制数据类型，但是在处理像TCP流或文件流时，必须使用到二进制数据，因此在Node.js中定义了一个Buffer类，该类用来创建一个专门存放二进制数据的缓存区；

# 八、Node.js Stream(流) #
Stream是一个抽象接口，Node.js有四种流类型：Readable（可读操作）、Writable（可写操作）、Duplex（可读可写操作）、Transform（操作被写入数据，然后读出结果）；    
所有的Stream对象都是Emitter对象都是EventEmitter的实例，常用的事件有：data（当有数据可读时触发）、end（没有更多数据可读时触发）、error（在接收和写入过程中发生错误时触发）、finish（所有数据已被写入到底层系统时触发）；

# 九、Node.js模块系统 # 
模块是Node.js应用程序的基本组成部分，文件和模块是一一对应的，换言之，一个Node.js文件就是一个模块，这个文件可能是JavaScript代码、JSON或者编译过的C/C++扩展；

# 十、Node.js函数 #

# 十一、Node.js路由 #
我们要为路由提供请求的URL和其他需要的GET及POST参数，随后路由根据这些数据来执行相应的代码；我们需要查看HTTP请求，从中提取出来请求的URL一级GET/POST参数；    
我们需要的所有数据都会包含在request对象中，该对象作为onRequest()回调函数的第一个参数传递，为了解析这些数据，我们需要额外的Node.js模块，它们分别是url和querystring模块；

# 十二、Node.js全局对象 #
Node.js中的全局对象是global，所有全局变量（除了global本身以外）都是global对象的属性，我们可以直接访问到global的属性，而不需要在应用中包含它；
## 1. 全局对象和全局变量 ##
global最根本的作用是作为全局变量的宿主，满足一下条件的变量是全局变量：①在最外层定义的变量；②全局对象的属性；③隐式定义的变量（未定义直接赋值的变量）；    
当定义一个全局变量时，这个变量同时称为全局对象的属性，反之亦然；     
在Node.js中不可能在最外层定义变量，因为所有用户代码都属于当前模块，而模块本身不是最外层上下文；永远使用var定义变量以避免引入全局变量，因为全局变量会污染命名空间，提高代码的耦合风险；

# 十三、Node.js常用工具 #
util是一个Node.js核心模块，提供常用函数的集合，用于弥补核心JavaScript的功能过于精简的不足；

# 十四、文件系统 #
Node.js提供一组类似UNIX（POSIX）标准的文件操作API；

# 十五、GET/POST请求 #
由于GET请求直接被嵌入在路径中，URL是完整的请求路径，包含了?后面的部分，因此可以手动解析后面的内容作为GET请求的参数，Node.js中url模块中的parse函数提供了这个功能；    
POST请求的内容全部的都在请求体中，http.ServerRequest并没有一个属性内容为请求体，原因是等待请求体传输可能是一个耗时的工作；

# 十六、Node.js Web模块 #
目前最主流的三个Web服务器是Apache、Nginx、IIS；




