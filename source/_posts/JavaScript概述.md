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

# 使用：
方法一，写在页面上，用`<script>...</script>`包含起来，它将直接被浏览器执行；    
方法二，把JavaScript代码放到一个单独的`.js`文件，然后在HTML中通过`<script src="..." type="text/javascript"></script>`引入这个文件；
