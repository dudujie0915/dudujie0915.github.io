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
<!-- more -->
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
对象转换为布尔值：所以的对象(包括数组和函数)都转换为true，对于包装对象亦是如此；     
对象到字符串和对象到数字的转换时通过调用待转换对象的一个方法来完成的，有两种不同的方法来执行转换，此规则只适用于本地对象；宿主对象根据各自的算法可以转换成字符串和数字；     
两个转换方法，一个是toString()，它的作用是返回一个反应这个对象的字符串：       
- 默认的toString()方法并不会返回一个有趣的值；
- 数组类的toString()方法将每个数组元素转换为一个字符串，并在元素之间添加逗号后合并成结果字符串；
- 函数类的toString()方法返回这个函数的实现定义的表达方式，通常是将用户定义的函数转换为JavaScript源代码字符串；
- 日期类定义的toString()方法返回了一个可读的日期和时间字符串；
- RegExp类定义的toString()方法将RegExp对象转换为表示正则表达式直接量的字符串；      
另一个转换对象的函数是valueOf()，默认的valueOf()方法简单地返回对象本身；
- 数组、函数和正则表达式简单地继承了这个默认方法，调用这些类型的实例的valueOf()方法只是简单返回对象本身；
- 日期类定义的valueOf()方法会返回它的一个内部表示：1970年1月1日以来的毫秒数；     
JavaScript中对象到字符串的转换有如下步骤：
- 如果对象具有toString()方法，则调用这个方法；如果它返回一个原始值，JavaScript将这个值转换为字符串(如果本身不是字符串的话)，并返回这个字符串结果；
- 如果对象没有toString()方法，或者这个方法并不返回一个原始值，那么JavaScript会调用valueOf()方法；如果存在这个方法，则JavaScript调用它；如果它返回一个原始值，JavaScript将这个值转换为字符串(如果本身不是字符串的话)，并返回这个字符串结果；
- 否则，JavaScript无法从toString()或valueOf()获得一个原始值，因此这时它将抛出一个类型错误异常；     
JavaScript中对象到数字的转换有如下步骤：
- 如果对象具有valueOf()方法，后者返回一个原始值，则JavaScript将这个原始值转换为数字(如果有需要额话)并返回这个数字；
- 否则，如果对象具有toString()方法，后者返回一个原始值，则JavaScript将其转换并返回；
- 否则，JavaScript抛出一个类型错误异常；
对象转换为数字的细节解释了为什么空数组会转换为数字0以及为什么具有单个元素的数组同样会转换成一个数字；数组继承了默认的valueOf()方法，这个方法返回一个对象而不是一个原始值，因此，数组到数字的转换则调用toString()方法；空数组转换为空字符串，空字符串转换为数字0；含有一个元素的数组转换为字符串的结果和这个元素转换字符串的结果一样；如果数组只包含一个数字元素，这个数字转换为字符串，再转换回数字；

JavaScript中的"+"运算符可以进行数学加法和字符串连接操作；如果它的其中一个操作数是对象，则JavaScript将使用特殊的方法将对象转换为原始值，而不是使用其他算术运算符的方法执行对象到数字的转换；"=="相等运算符与此类似，如果将对象和一个原始值比较，则转换将会遵照对象到原始值的转换方式进行；"<"运算符以及其他关系运算符也会做对象到原始值的转换，但要除去日期对象的特殊情形：任何对象都会首先尝试调用valueOf()，然后调用toString()，不管得到的原始值是否直接使用，它都不会进一步被转换为数字或字符串；     
"+"、"=="、"!="和关系运算符是唯一执行这种特殊的字符串到原始值的转换方式的运算符;

"+"和"=="应用的对象到原始值得转换包含日期对象的一种特殊情形；日期类是JavaScript语言核心中唯一的预先定义类型，它定义了有意义的向字符串和数字类型的转换，对于所有非日期的对象来说，对象到原始值得转换基本上是对象到数字的转换(首先调用valueOf()),日期对象则使用对象到字符串的转换模式，然而这里的转换时通过valueOf或toString()返回的原始值将被直接使用，而不是被强制转换为数字或字符串；