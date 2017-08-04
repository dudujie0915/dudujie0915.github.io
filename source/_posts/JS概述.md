---
title: 【笔记】JavaScript概述
date: 2017-07-21
tags: [笔记,教程,JavaScript]
categories: JavaScript
---
# 组成部分：
1. 核心部分：基本的语法构造、标准库
2. 宿主环境：浏览器、服务器（Node项目）    

基本的语法构造：数据类型（数值、字符串、对象、数组、函数）、操作符、控制结构、语句、数据类型转换、错误处理机制、变成风格     
标准库：一系列具有各种功能的对象，如Array、Data、Math、Object、Boolean、包装对象、Number、String、RegExp、JSON、console、属性描述对象    
浏览器：
  - 浏览器控制类：操作浏览器
  - DOM类：操作网页的各种元素
  - Web类：实现互联网的各种功能

服务器：提供各种操作系统的API，如文件操作API、网络通信API

# 是什么？
1. JavaScript 是一种轻量级的脚本语言；
2. JavaScript 是一种嵌入式（embedded）语言；
3. 从语法角度看，JavaScript语言是一种“对象模型”语言；
4. JavaScript是一门高端的、动态的、弱类型的编程语言，非常适合面向对象和函数式的编程风格；
5. JavaScript是一种集健壮性、高效性和通用性为一身的编程语言；
<!-- more -->
> - ECMAScript 是在宿主环境中执行计算，处理对象的面向对象编程语言。   
> - 脚本语言 是一种用于操作，自定义，自动化现有系统设施的编程语言。    
> - WEB 浏览器为引入客户端计算能力而提供 ECMAScript 宿主环境，例如，它提供的对象有：windows，menus，pop-ups，dialog boxes，text areas，anchors，frames，history，cookies 及输入 / 输出等等。
> - WEB 服务器为了服务端的计算则提供了一个完全不一样的宿主环境，包括的对象有：requests，clients，files 以及数据锁定和分享的机制。
> - ECMAScript 是基于对象的：基本语言和宿主设施都由对象提供，ECMAScript 程序是一组可通信的对象。ECMAScript 对象 (objects) 是 属性 (properties) 的集合，每个属性有零个或多个 特性 (attributes)，它确定怎样使用此属性。属性是持有其他 对象 (objects)， 原始值 (primitive values)， 函数 (functions) 的容器。原始值是以下内置类型之一的成员：Undefined，Null，Boolean，Number，String；对象是剩下的内置类型 Object 的成员；函数是可调用对象 (callable object)。方法 (method) 是通过属性与对象关联的函数。
> - ECMAScript 定义一组内置对象 (built-in objects)，勾勒出 ECMAScript 实体的定义。这些内置对象包括 全局对象 (global object) ，Object 对象 ，Function 对象 ，Array 对象 ，String 对象 ，Boolean 对象 ，Number 对象 ，Math 对象 ，Date 对象 ，RegExp 对象 ，JSON 对象，和 Error 对象： Error ，EvalError ，RangeError ，ReferenceError ，SyntaxError ，TypeError ，URIError 。
> - ECMAScript 中还定义一组内置运算符 (operators)。ECMAScript 运算符包括 一元运算符 ，乘法运算符 ，加法运算符 ，按位移位运算符 ，关系运算符 ，相等运算符 ，二进制位运算符 ，二进制逻辑运算符 ，赋值运算符 ，逗号运算符。
> - ECMAScript对象可以通过各种方式创建，包括字面符号，或通过 构造器 创建对象然后运行代码初始化其全部或部分属性值，为这些属性分配初始值。每个构造器是一个拥有名为“prototype”的属性的函数。此属性用于实现 基于原型的继承 和 共享属性 。构造器通过 new 表达式创建对象,不使用 new 调用一个构造器的结果，依赖构造器本身。
> - 每个由构造器创建的对象，都有一个隐式引用 ( 叫做对象的原型 ) 链接到构造器的“prototype”属性值。再者，原型可能有一个非空 (non-null) 隐式引用链接到它自己的原型，以此类推，这叫做 原型链 。当向对象的一个属性提出引用，引用会指向原型链中包含此属性名的第一个对象的此属性。换句话说，首先检查直接提及的对象的同名属性，如果对象包含同名的属性，引用即指向此属性，如果该对象不包含同名的属性，则下一步检查对象的原型；以此类推。
> - 一般情况下基于类的面向对象语言的实例拥有状态，类拥有方法，并且只能继承结构和行为。在 ECMAScript 中，对象拥有状态和方法，并且结构，行为，状态全都可继承。
> - ECMAScript 的严格变体通常被称为语言的 严格模式 (strict mode)。严格模式选择使用的 ECMAScript 严格模式的语法和语义，明确地适用于个别 ECMAScript 代码单元级别。由于严格模式适用于选择的语法代码单元级别，严格模式仅在这个代码单元内施加有局部效果的限制。严格模式不限制或修改任何必须运行在多个代码单元的 ECMAScript 语义层面。一个 ECMAScript 程序可由严格模式和非严格模式的代码单元组成。在这种情况下，严格的模式只适用于严格模式代码单元内实际执行的代码。

> - JavaScript ( JS ) 是一种轻量级解释型的，或是JIT编译型的程序设计语言，有着 头等函数 (First-class Function) 的编程语言。虽然它是作为开发web页面的脚本语言而出名的，但是在很多非浏览器环境中也使用JavaScript，例如 node.js 和 Apache CouchDB。JS是一种基于原型、多范式的动态脚本语言，并且支持面向对象、命令式和声明式（如：函数式编程）编程风格

# 为什么学习？
1. 操控浏览器的能力
2. 广泛的使用领域
 - 浏览器的平台化
 - Node
 - 数据库操作（NoSQL） 
 - 跨移动平台
 - 内嵌脚本语言
 - 跨平台的桌面应用程序
3. 易学性
 - 学习环境无处不在
 - 简单性
 - 与主流语言的相似性
 虽然核心语法不难，但是 JavaScript 的复杂性体现在另外两个方面。
 首先，它涉及大量的外部 API。
 其次，JavaScript 语言有一些设计缺陷。
4. 强大的性能
 - 灵活的语法，表达力强 
 - 支持编译运行
 - 事件驱动和非阻塞式设计
5. 开放性
6. 社区支持和就业机会

# 使用(浏览器)：
方法一，写在页面上，用`<script>...</script>`包含起来，它将直接被浏览器执行；    
方法二，把JavaScript代码放到一个单独的`.js`文件，然后在HTML中通过`<script src="..." type="text/javascript"></script>`引入这个文件；
