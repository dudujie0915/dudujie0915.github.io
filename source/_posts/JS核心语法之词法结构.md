---
title: 【笔记】核心语法之词法结构
date: 2017-07-24
tags: [笔记,教程,JavaScript]
categories: JavaScript
---
JavaScript的词法结构包括字符集、注释、直接量、标识符和保留字、可选的分号五部分组成。

# 字符集
JavaScript程序是用Unicode字符集编成的。Unicode是ASCII和Latin-1的超集，并支持几乎所有的语言。
## 区分大小写
JavaScript是区分大小写的语言
## 空格、换行符和格式控制器
JavaScript会忽略程序中的标识之间的空格；多少情况下，也会忽略换行符；因此可以采用整齐、一致的缩进来形成统一的编码风格，提高代码可读性。    
标识为空格的字符：普通的空格符(\u0020)、水平制表符(\u0009)、垂直制表符(\u000B)、换页符(\u000C)、不中断空白(\u00A0)、字节序标记(\uFEFF)、在Unicode中所有Zs类别的字符；    
标识为行结束符：换行符(\u000A)、回车符(\u000D)、行分隔符(\u2028)、段分隔符(\u2029)；回车符加换行符组成一个单行结束符；    
Unicode格式控制字符(Cf类)：如从右至左书写标记(\u200F)、从左到右书写标记(\u200E)，可以用在注释、字符串直接量、正则表达式直接量中，不能用在标识符(如变量名)中；有个例外，零宽连接符(\u200D)和零宽非连接符(\uFEFF)可以出现在标识符中，但是不能作为标识符的首字符；
<!-- more -->
## Unicode转义序列
使用6个ASCII字符来表示任意16位Unicode内码；Unicode转义序列均以\u为前缀，其后跟随4个十六进制，此写法可用在字符串直接量、正则表达式直接量、标识符中(关键字除外)和注释(不会解析)中;
## 标准化
Unicode允许使用多种方法对同一个字符进行编码。比如复杂的字符可能用两个字符来表示；

# 注释
两种注释方式
```
//单行注释

/*
 多行注释
*/

//由于历史上JavaScript兼容HTML代码的注释，所以
<!-- 
xxx 
-->
也被视为单行注释
注：-->只有放在行首，才会被当成注释，否则是一个运算符
```

# 直接量
直接量就是程序中直接使用的数值量，比如整数、小数、字符串、布尔值、正则表达式直接量(用做模式匹配)、null，更加复杂的表达方式，可以写成数值或对象直接量；

# 标识符和保留字
## 标识符
标识符就是一个名字，用来对变量和函数进行命名(此两种最常见)，或用在某些循环语句中的跳转位置的标记；   
命名规则：
- 标识符区分大小写；
- 必须以字母、下划线(_)、或美元符($)开始；
- 后续字符可以是字母、数字、下划线或美元符； 
- 中文是合法标识符；   
出于可移植性和易用性的考虑，通常只用ASCII字母和数字来书写标识符；JavaScript允许标识符中出现Unicode字符全集中的字母和数字；

## 保留字
保留字(即关键字)不能用做标识符。    
保留字有：  
```  
break  case  catch  continue  debugger  default    
delete  do  else  false  finally  for    
function  if  in  instanceof  new  null    
return  switch  this  throw  true  try    
typeof  var  void while  with  
```
ES5保留的关键字：
```
class  const  enum  export  extends  import  super
```
普通模式合法，严格模式下是保留字：
```
implements  interface  let  package  private  protected    
public  static  yield
```
下面的标识符在严格模式下并不完全是保留字，但是不能用做变量名、函数名或参数名：
```
arguments  eval
```
JavaScript预定义的全局变量和函数，应避免把他们的名字用做变量名和函数名：    
```
arguments  Array  Boolean  Date  decodeURI  decodeURIComponent
encodeURI  encodeURIComponent  Error  eval  EvalError  Function
Infinity  isFinite  isNaN JSON  Math  NaN
Number  Object  parseFloat  parseInt  RangError  ReferenceError
RegExp  String  SyntaxError  TypeError  undefined  URIError
```
每一种特定的JavaScript运行环境(客户端、服务器端等)都有自己的一个全局属性列表；

# 可选的分号
JavaScript使用分号(;)将语句分割开；   
如果语句各自独占一行，通常可以省略语句直间的分号(程序结尾或右花括号"}"之前的分号也可省略)；    
建议使用分号来明确标记语句的结束；   
JavaScript并不是在所以换行处都填补分号，只有在缺少了分号无法正常解析代码的时候才会填补分号；   
如果一条语句以"("或"["(此两种比较常见)、"/"或"+"或"-"(此三种不常见)开始，它极有可能和前一条语句合在一起解析；在语句前加上一个分号，可以有效的防止错误；    
如果当前语句和下一行无法合并解析，JavaScript则在第一行后填补分号，但有两个例外：一个是涉及到return、break和countinue语句的场景中，如果这三个关键词后紧跟着换号，JavaScript会在换行处填补分号；二是在涉及"++"和"--"运算符(它们既可以作为表达式的前缀，也可以当做表达式的后缀)的时候，如果将其用做后缀表达式，它和表达式应当在同一行，否则行尾将填补分号，同时"++"或"--"会作为下一行的前缀操作符并与之一起解析；
