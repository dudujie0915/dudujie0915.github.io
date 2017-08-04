---
title: 【笔记】核心语法之类型转换
date: 2017-07-28
tags: [笔记,教程,JavaScript]
categories: JavaScript
---
JavaScript中的取值类型非常灵活，我们可以提供任意类型值，JavaScript将根据需要自行转换类型；意外的转换类型如下：     

| 值                     | 转换为字符串   | 数字        | 布尔值   | 对象                   |
| :---------------------- | :------------- | :---------- | :-------- | :--------------------  |
| undefind               | "undefined"   | NaN        | false    | throws TypeError      |
| null                   | "null"        | 0          | false    | throws TypeError      |
| true                   | "true"        | 1          |          | new Boolean(true)     |
| false                  | "false"       | 0          | false    | new Boolean(false)    |
| ""(空字符串)            |               | 0          | false    | new String("")        |
| "1.2"(非空，数字)       |               | 1.2        | true     | new String("true")    |
| "one"(非空，非数字)     |               | NaN        | true     | new String("one")     |
| 0                      | "0"           |            | false    | new Number(0)         |
| -0                     | "0"           |            | false    | new Number(-0)        |
| NaN                    | "NaN"         |            | false    | new Number(NaN)       |
| Infinity               | "Infinity"    |            | true     | new Number(Infinity)  |
| -Infinity              | "-Infinity"   |            | true     | new Number(-Infinity) |
| 1(无穷大，非零)         | "1"           |            | true     | new Number(1)         |
| {}(任意对象)            | 参考第三节     | 参考第三节 | true     |                       |
| {}(任意数组)            | ""            | 0         | true     |                       |
| \[9\](1个数字元素)        | "9"           | 9         | true     |                       |
| \['a'\](其他数组)         | 使用join()方法 | NaN      | true     |                       |
| function(){}(任意函数)  | 参考第三节     | NaN      | true     | &nbsp;                |

原始值到原始值的转换：     
- 转换为布尔值：[布尔值](/2017/07/26/JS核心语法之类型简介/)；     
- 转换为字符串：表中明确定义；     
- 转换为数字：以数字表示的字符串可直接转换为数字，也允许在开始和结尾处带空格；在开始和结尾处的任意非空格字符都不会被当成数字直接量的一部分，进而造成字符串转换为数字的结果为NaN；true转换为1，false、空字符串""转换为0；

原始值转换为对象：
通过调用String()、Number()或Boolean()构造函数，转换为它们各自的[包装对象](/2017/07/26/JS核心语法之类型简介/)；     
null和underfined属于例外，当将它们用在期望是一个对象的地方都会造成一个类型错误异常，而不会执行正常的转换；     

对象到原始值，看第三节；

# 转换和相等性
JavaScript中类型灵活变化，"=="相等运算符也随相等的含义灵活多变；    
```
下面的比较结果均是true
null == underfined
"0" == 0
0 == false
"0" == false
```
一个值转换为另一个值并不意味着两个值相等，如在期望使用布尔值的地方使用了underfined，它将会转换为false，但不能表明underfined == false；     
JavaScript运算符和语句期望使用多样化的数据类型，并可以相互转换；

# 显示类型转换
做显式类型转换最简单的方法就是使用Boolean()、Number()、String()或Object()函数；     
除了null或underfined之外的任何值都具有toString()方法，这个方法的执行结果通常和String()方法的返回结果一致；     
JavaScript的某些运算符会做隐式的类型转换，如"+"运算符的一个操作数是字符串，他将会把另一个操作符转换为字符串；一元"+"运算符将其操作数转换为数字；一元"!"运算符将其操作数转换为布尔值并取反；
```
x + ""  //等价于String(x)
+x      //等价于Number(x)，也可写成x-0
!!x     //等价于Boolean(x)
```
JavaScript中提供了专门的函数和方法用来做更精确的数字到字符串和字符串到数字的转换；      
Number类定义的toString()方法可以接收表示转换基数的可选参数，如果不指定此参数，转换规则将是基于十进制；亦可以将数字转换为其他进制数；
```
var n = 17;
binary_string = n.toString(2);   //转换为"10001"
```
Number类定义的toFixed()根据小数点后的指定位数将数字转换为字符串，它从不用指数记数法；toExponential()使用指数记数法将数字转换为指数形式的字符串，其中小数点前只有一位，小数点后的位数由参数指定；toPrecision()根据指定的有效数字位数将数字转换成字符串，如果有效数字的位数少于数字整数部分的位数，则转换成指数形式；三个方法都会适当地进行四舍五入或填充0；
```
var n = 123456.789;
n.toFixed(0);  //"123457"
n.toFixed(2);  //"123456.79"
n.toFixed(5);  //"123456.78900"
n.toExponential(1);  //"1.2e+5"
n.toExponential(3);  //"1.235e+5"
n.toPrecision(4);  //"1.235e+5"
n.toPrecision(7);  //"123456.8"
n.toPrecision(10);  //"123456.7890"
```
通过Number()转换函数传入一个字符串，它会试图将其转换为一个整数或浮点数直接量，这个方法只能基于十进制数进行转换，并且不能出现非法的尾随字符；     
parseInt()只解析整数，而parseFloat()则可以解析整数和浮点数，如果字符串前缀是"0x"或者"0X"，parseInt()将其解释为十六进制数；它们两个都会跳过任意数量的前导空格，尽可能解析更多数值字符，并忽略后面的内容；如果第一个非空字符是非法的数字直接量，将返回NaN;
```
parseInt("3 d")  // => 3
parseFloat("3.14 d")  // => 3.14
parseInt("-12.3")  // => -12
parseInt("0xff")  // => 255
parseInt("0Xff")  // => 255
parseInt("-0XFF")  // => -255
parseFloat(".1")  // => 0.1
parseInt("0.1")  // => 0
parseInt(".1")  // => NaN
parseFloat("$72.1")  // => NaN
```
parseInt()可以接收第二个可选参数，这个参数指定数字转换的基数，合法的取值范围是2~36；
```
parseInt("11",2)  // => 3(1*2+1)
parseInt("zz",36)  // => 1295(35*36+35)
parseInt("077",10)  // => 77(7*10+7)
```

# 对象转换为原始值
