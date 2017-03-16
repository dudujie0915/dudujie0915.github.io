---
title: 【教程】JavaScript权威指南第六版
date: 2016-06-13
tags: [教程,JavaScript]
categories: JavaScript
---
# JavaScript权威指南第六版 #
## 一、JavaScript概述 ##
JavaScript是一门高端的、动态的、弱类型的编程语言，非常适合面向对象和函数式的编程风格；  
内置API，基于浏览器的API----“客户端JavaScript”
### 1. JavaScript语言核心 ###
```javascript
//单行注释
变量是表示值的一个符号名称，通过var关键字声明（例 var x;）,值可以通过等号赋值给变量（例 x=0;）  
JavaScript支持多挣数据类型：
数字（例 x=1;）;
整数和实数公用一种数据类型----浮点型（例 x=0.01;）;
字符串类型----由双引号或者单引号包含（例 x="hello"; x='hello';）;
布尔值（例 x=true; x=false;）;
null（是一个特殊的值，意思是“空”）;
underfined（和null类似）;

对象----最重要的类型，对象是名/值对的集合，或字符串到值映射的集合
var book={
    topic:"javascript"，//属性:值
    fat:true
}
通过"."或"[]"来访问对象属性
book.topoc          // =>"javascript"
book["fat"]           // =>true
book.author = "Flanagan";             // 通过赋值创建一个新属性
book.contents = {};            // {}是一个空对象，他没有属性              

数组----以数字为索引的列表
var primes = [2,3,5,7];          //有4个值的数值，由"["和"]"划定界限
primes[0]          // => 2  获取数组中的第一个元素（索引为0）
primes.length          // =>4  数组元素的个数
primes[primes.length -1]      // =>7  数组的最后一个元素
primes[4] = 9;          //通过赋值来添加新元素
primes[4] = 11;             //通过赋值来改变已有的元素
var empty = [];           // []是空数组，它具有0个元素
empty.length            // =>0

数组和对象中都可以包含另一个数组或对象：
var points = [                  //具有两个元素的数字
    {x:0,y:0},                      //每个元素都有一个对象
    {x:1,y:1}
]
var data ={                                     //一个包含两个属性的对象
    trial1:[[1,2],[3,4]],                 //每一个属性都是数组
    trial2:[[2,3],[4,5]]                  //数组的元素也是数组
}
```

