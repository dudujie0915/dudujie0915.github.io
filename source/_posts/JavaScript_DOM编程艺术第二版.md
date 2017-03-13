---
title: 【教程】JavaScript_DOM编程艺术第二版
date: 2016-08-05
tags: [教程,JavaScript,DOM]
categories: JavaScript
---
# 一、JavaScript简史
## 1. 起源
## 2. DOM
 DOM是一套对文档的内容进行抽象和概念化的方法；
## 3. 浏览器战争
 ### 3.1 DHTML  
DHTML的含义是：
- 利用HTML把网页标记为各种元素；
- 利用css设置元素样式和他们的位置；
- 利用JavaScript实时地操控页面和改变样式；
### 3.2 浏览器之间的冲突
不同的浏览器之间不同的实现方式，在早期的Nerscape和IE之间出现（现在IE低版本也是这个问题），这促使标准的出现；
<!-- more -->
## 4. 制定标准
W3C组织发起，Netscape、微软和其他一些浏览器制造商联合制定，影响深远；
- 浏览器以外的考虑
- 浏览器战争的结局
- 崭新的起点
# 二、JavaScript语法
## 1. 准备工作
程序设计语言分为解释型和编译型两大类，Java或C++等语言需要一个编译器，编译器是一种程序，能够把用Java等高级语言编写出来的源代码翻译成直接在计算机上执行的文件；解释型应用程序只需要解释器，对于JavaScript语言，在互联网环境下，Web浏览器负责完成有关的解释和执行工作；
## 2.语法
### 2.1 语句
语句用";"区分
```
多行语句
first statement;
second statement;

单行语句
first statement;  second statement;
```
### 2.2 注释
```
//单行注释
<!--单行注释，HTML风格，没有闭合标签，只能用于单行注释，容易混淆，最好不要用

/*多行
  注释*/

```
### 2.3 变量
- 变量和赋值，变量可以不用提前声明，但是建议提前声明，用“var”完成声明；
- 不必单独声明每个变量，可以一条语句一次声明多个变量；
- 可以把声明变量和对该变量赋值一次完成； 
- 在JavaScript中，变量和其他语法元素的名字都是区分字母大小写的；
- JavaScript变量名中不允许包含空格或标点符号（美元符号“$”例外）；
- JavaScript变量名允许包含字母、数字、美元符和下划线（但是第一个字符不允许是数字）；
```javascript
//赋值
mood = "happy";
age = 33；

//声明
var mood;
var age;

//一条语句一次声明多个变量
var mood,age;

//把声明变量和对该变量赋值一次完成
var mood ="happy";
var age =33;
或者
var mood ="happy",age=33;

//下面的语句是对两个不同的变量进行赋值
var mood = "happy";
MOOD = "sad";
Mood = 23;

//命名方法一：
var my_mood = "happy";
//命名方法二（驼峰格式）：
var myMod = "happy";
```
 ### 2.4 数据类型
有些语言要求在声明变量的同事必须声明变量的数据类型，这种做法称为类型声明（typing）；  
必须明确类型声明的语言称为强类型（strongly typed）语言；JavaScript不需要进行类型声明，是一种弱类型（weakly typed）语言，这意味可以在任何阶段改变变量 的数据类型；  
- 字符串、数值和布尔值都是标量（scalar）；
- 字符串：有0个或多个字符构成，字符包括（但不限于）字母 、数字、标点符号和空格。字符串必须包在引号里，单引号或者双引号都可以；
- 数值：可以是任意位的小数（浮点数），整数，可以是负数（早有关数值前面加一个减号“-”），可以是负浮点数；
- 布尔值：布尔（boolean）类型，只有两个可选值--true和false；
- 数组：  
	1. 指用一个变量表示一个值的集合，集合中的每个值都是这个数组的一个元素（element） ；  
	2. 在JavaScript中，数组可以用关键字Array声明，声明数组的同时可以指定数组初始元素个数，也就是数组的长度（length）；  
	3. 向数组添加元素的操作称为填充，填充数组时，不仅需要给出新元素的值，还需要给出新元素在数组中的存放位置，这个位置就是这个元素的下      标，数组里一个元素一个下标；用0作为第一个下标；可以在声明数组的同时对他进行填充；数组元素可以是字符串、布尔值、一组数值，也可以是三者的混合，还可以是变量，数组元素的值可以是另外一个数组的元素，数组可以包含其他数组，数组中的任何一个元素都给可以把一个数组作为它的值；  
	4. 关联数组：如果在填充数组是只给出了元素的值，这个数组就是传统数组，它的各个元素的下标将自动创建和刷新；可以通过在填充数组的时候为每个新元素明确地给出下标来改变这种默认的行为，下标不必局限于整数数字，这样的数组叫关联数组；
- 对象：对象使用一个名字表示一组值，对象的每个值都是对象的一个属性；创建对象使用Object关键字，使用点好来获取属性，属性值可以是任何JavaScript值，包括其他对象；
```javascript
//字符串
//下面两个完全一样
var mood = "happy";
var mood = 'happy';
//单双引号的表示
var mood ="don't ask";
var mood = 'don\'t ask'; //字符转义
var height = "about 5'10\" tall"; //字符转义

//数值
var tem = 33;
var tem = 20.33;
var tem = -33;
var tem = -20.33;

//布尔值
var sleeping = true;
var sleeping = false;
var sleeping = "true"; //这个是字符串类型

//数组
var beatles = Array(4); //数组的长度为4
var beatles = Array（）; //未给出元素个数
//数据填充
array[index] = element;
beatles[0] = "John"; //用0作为第一个下标
//声明和填充beatles数组的全过程:
var beatles = Array(4);
beatles[0] = "John";
beatles[1] = "Paul";
beatles[2] = "George";
beatles[3] = "Ringo";
//简单的方法声明和填充beatles数组:
var beatles = Array("John","Paul","George","Ringo");
//简写形式
var beatles = ["John","Paul","George","Ringo"];
//数组存放数值
var year = [1940,1955,1963,1994];
//数组存放混合数据类型
var lennon = ["John",1940,false];
//数组元素可以是变量
var name ="John";
beatles[0] = name;
//数组元素的值可以是另一个数组的元素
var name = ["Ringo","John","George","Paul"];
beatles[1] = name[3];
//数组可以包含其他数组
var lennon =  ["John",1940,false];
var beatles = [];
beatles[0] = lennon;
//关联数组
var lennon = Array();
lennon["name"] = "John";
lennon["year"] = 1940;
lennon["living"] = false;

//创建对象
var lennon = Object();
lennon.name = "John";
lennon.year = 1940;
lennon.living = false;
//创建对象的简洁语法--花括号语法：
var lennon = {name:"John",year:1940,living:false};
```
## 3. 操作
### 算数操作符
加（+）减（-）乘（*）除（/）;
```javascript
//变量可以包含操作
var tatal = (1+4)*5
//可以对变量进行操作
var temp_fahrenheit = 95;
var temp_celsius = (temp_fahrenheit - 32) / 1.8;
//常用操作缩写
year = year + 1;可以缩写为year++;
year = year - 1;可以缩写为year--;
//加号（+）即可以用于数值，也可以用用于字符串
//把多个字符串收尾相连在一起的操作叫做拼接
var message = "I am grrling" + "happy";
//可以通过变量完成拼接
var mood = "happy";
var message = "I am feeling" + mood;
//可以把数值和字符串拼接在一起，此时，数值自动转换为字符串
var year = 2005;
var message = "The year is" + year;
//比较字符串和数值
alert("10"+20);//返回字符串“1020”
alert(10+20);//返回数值30
//快捷操作符+=，它一次完成“加法和赋值”（“或拼接和赋值”）
var year = 2010;
var message == "The year is";
message += year; 等同于 message = message + year;
```
## 4. 条件语句 ##
最常见的条件语句是if语句  
```
if(condition){值为true时执行;}else{值为false时执行;}
iff(condition) 值为true时执行; 
```
条件放在if后面的圆括号里，条件的求值结果永远是一个布尔值，即只能是true或false；  
花括号本事并不是必不可少的，如果if语句中花括号部分值包含这一条语句，那么它就可以不使用花括号，而且这条语句的内容可以写在同一行上；它可以提高脚本的可读性，推荐使用；
### 4.1 比较操作符 ###
大于(>)、小于(<)、大于等于(>=)、小于等于(<=)、等于(==)、不等于(!=)、全等于(===)，严格不相等(!==) 
单个等号(=)是用于完成赋值操作的；
```javascript
var a = false;
var b = " ";
if(a == b){alert();}//求值结果为true
if(a === b){alert();}//求值结果为false
```
### 4.2 逻辑操作符 ###
逻辑与（&&）、逻辑或（||）、逻辑非（!）  
JavaScript允许把条件语句的操作组合在一起；  
逻辑操作符的操作对象是布尔值，每个逻辑操作数返回一个布尔值true或false；  
逻辑与只有在所有的操作数都是true时才会是true；  
逻辑或只要有一个操作数为true时就是true，只有当所有的操作数为false时才为false；  
逻辑非只能用于单个逻辑操作数，其结果是把那个逻辑操作数返回的布尔值取反；
## 5. 循环语句 ##
循环语句可以让我们反复的执行同一段代码；
### 5.1 while循环 ###
while循环：与if语句唯一的区别就是：只要给定条件的求值结果是true，包括在花括号里的代码就将反复地执行下去；  
while循环的花括号部分所包含的语句有可能不被执行，因为对循环控制条件的求值发生在每次循环开始之前，所有如果循环控制条件的首次求值结果是false，那么代码将一次也不会被执行；
```javascript
//实例
var count = 1;
while(count < 11){
    alert(count);
    count++;
}
```
do...while循环：在循环语句的代码至少执行一次；
```javascript
//实例
var count = 1;
do{
    alert(count);
    count++;
}while(count<1);
```
### 5.2 for循环 ###
用for循环来重复执行一些代码的好处是循环控制结构更加清晰
```javascript
//实例
var beatles = Array("John","Paul","George","Ringo");
for（var count = 0; count < beatles.length; count++）{
    alert(beatles[count]);
}
```
## 6. 函数 ##
函数就是一组允许在你的代码里随时调用的语句，事实上，每个函数实际上是一个短小的脚本;  
应该先对函数做出定义再调用它们；  
```javascript
//实例
function shout(){
    var beatles = Array("John","Paul","George","Ringo");
    for(var count = 0; count < beatles.length; count++){
        alert(beatles[count]);
    }
}
shout();

```
JavaScript提供了许多内置函数，比如alert；  
在定义函数时，可以为它声明任意多个参数，只要用逗号分割开来就行；在函数内部，可以像使用普通变量那样使用它的任何一个参数；
```javascript
//实例
function multily(num1,num2){
    var total = num1 * num2;
    alert(total);
}
multily(10,2);
```
函数的真正价值体现在，我们可以把它们当做一种数据类型来使用，这意味着可以把一个函数的调用结果赋给一个变量：
```javascript
//实例
function convertToCelsius(temp){
    var result = temp - 32;
    result = result / 1.8;
    return result;
}
var temp_fahrenheit = 95;
var temp_celsius = convertToCelsius(temp_fahrenheit);
alert(temp_celsius);
```
**在命名变量时，用下划线分隔各个单词；在命名函数时，从第二个单词开始把每个单词的第一个字母变成大写形式（驼峰命名法）；在命名css的名称时，用“-”分隔单词（非强制，但是好习惯，自己的风格，并且符合规范）**
### 6.1 变量的作用域 ###
变量既可以是全局的，也可以是局部的；  
全局变量：可以在脚本的任意位置被引用，全局变量的作用域是整个脚本；  
局部变量：只存在声明它的那个函数的内部，在那个函数的外部是无法引用它的，局部变量的作用域仅限于某个特定的函数；  
可以用var关键字明确地为函数变量设定作用域；如果某个函数中使用了var，那么变量就将被视为一个局部变量，它只存在于这个函数的上下文中；反之，如果没有使用var，那么变量就将被视为一个全局变量，如果脚本里已经存在一个与之同名的全局变量，这个函数就会改变那个全局变量的值；  
**函数在行为方面应该像一个自给自足的脚本，在定义一个函数时，一定要 把它内部的变量全部都明确地声明为局部变量；如果总是在函数里使用var关键字来定义变量，就能避免任何形式的二义性隐患；**
## 7. 对象 ##
对象是自包含的数据集合，包含在对象里面的数据可以通过两种形式访问----属性（property）和方法（method）； 
- 属性是隶属于每个特定的对象的变量；
- 方法是只有某个特定对象才能调用的函数；  
对象就是由一些属性和方法组合在一起而构成的一个数据实体；  
在JavaScript里，属性和方法都使用“点”语法来访问；
```
Object.property
object.method()
```
### 7.1 内建对象 ###
JavaScript提供了一系列预先定义好的对象，这些可以拿来就用的对象称为内建对象；  
数组是一种内建对象，当我们用new关键字去初始化一个数组时，其实就是在创建一个Array对象的新实例`var beatles = new Array();`当需要了解某个数组有多少个元素时，利用Array对象的length属性来获取这一信息`beatles.length;`  
Math对象（处理数值）、Date对象（处理日期值）
### 7.2 宿主对象 ###
可以在JavaScript脚本中使用一些已经 预先定义好的其他对象，在web应用中，是有浏览器提供的；由浏览器提供的预先定义对象称为宿主对象；  
宿主对象包括Form、Image、Element、document等；
# 三、 DOM #
5个常用的DOM方法：getElementById、getElementsByIagName、getElementsByClassName、getAttribute、setAttribute  
## 1. 文档：DOM中的“D” ##
document（文档）
## 2. 对象：DOM中的“Ｏ” ##
JavaScript中对象分三类：
- 用户定义对象：由程序员自行创建的对象；
- 内建对象：内建在JavaScript语言里的对象；
- 宿主对象：有浏览器提供的对象；  
最基础的对象是window对象，window对象对应这浏览器窗口本身，这个对象的属性和方法通常称为BOM（浏览器对象模型，或者称为Window Object Model--窗口对象模型），BOM对象提供了window.open和window.blur等方法；
## 3. 模型：DOM中的“M” ##
“M”代表着“Model”（模型），也可以说它代表着“Map”（地图）；  
## 4. 节点 ##
元素节点、文本节点、属性节点
### 4.1 元素节点 ###
就是指html、head、body、ul、li、div等元素（页面的结构），
### 4.2 文本节点 ###
文本节点就是指文本内容；  
在HTML文档里，文本节点总是被包含在元素节点内部，但并非所有的元素节点都包含有文本节点，比如ul节点包含li节点；
### 4.3 属性节点 ###
属性节点用来对元素做出更具体的描述，例如所有的元素都有一个title属性，在DOM中title="*"是一个属性节点；  
因为属性节点总是放在起始标签里，所以属性节点总是被包含在元素节点中；  
并非所有的元素都包含属性，但是所有的属性都被元素包含；
### 4.4 CSS ###
css的语法，继承，class属性，id属性
### 4.5 获取元素 ###
有3种DOM方法可以获取元素节点，分别是通过元素的ID、通过标签名称和通过类名字来获取；
1. **getElementById：**返回一个与那个有着给定id属性值的元素节点对应的对象，它是document对象特有的函数
```javascript
document.getElementById(id)
//实例
document.getElementById("purchases")
```
2. **getElementsByTagName：**返回一个对象数组，每个对象分别对应着文档里有着给定标签的一个元素
```javascript
element.getElementsByTagName(tag)
//实例
document.getElementsByTagName("li")
//获取每个元素的对象
for(var i=0; i<document.getElementsByTagName("li").length; i++){
    alert(typeof document.getElementsByTagName("li")[i]);
}
//变量替换
var items = document.getElementsByTagName("li")；
for(var i=0; i<items.length; i++){
    alert(typeof items[i]);
}
//返回文档总共元素节点
alert(document.getElementsByTagName("*").length);
```
即使整个文档里标签只有一个，getElementsByTagName也返回一个数组，此时数组的长度为1；
3. **getElementsByClassName：**HTML5支持，低版本浏览器需要做兼容性处理，
```javascript
document.getElementsByClassName(class)
//实例
document.getElementsByClassName("sale")
//可以查找带有多个类名的方法,类名的先后顺序不重要，只要元素中的class属性中，有这两个类名就能匹配该元素
alert(document.getElementsByClassName("important sale").length);
//实例--判断id下面有多少个class元素
var shopping = document.getElementById("purchases");
var sales = shopping.getElementsByClassName("sale");
alert(sales.length);
```
**重要，getElementsByClassName的兼容性写法(此方法不适用于多个类名)：**
```javascript
function getElementsByClassName(node,classname){
    if(node.getElementsByClassName){
        //使用现有方法
        return node.getElementsByClassName(classname);
    }else{
        var results = new Array();
        var elems =node.getElementsByTagName("*");
        for(var i=0; i<elems.length;i++){
            if(elems[i].className.indexOf(classname) != -1){
                results[results.length] = elems[i];
            }
        }
        return results;
    }
}
```
### 4.6 盘点知识点 ###
- 一份文档就是一棵节点树；
- 节点分为不同的类型：元素节点、属性节点和文本节点等；
- getElementById将返回一个对象，该对象对应着文档里的一个特定的元素节点；
- getElementsByTagName和getElementsByClassName将返回一个对象数组，它们分别对应着文档里的一组特定的元素节点；
- 每个节点都是一个对象；
## 5. 获取和设置属性 ##
获取属性getAttribute,改变属性节点的值setAttribute
### 5.1 getAttribute ###
getAttribute是一个函数，只有一个参数----查询的属性名字`object.getAttribute(attribute)`,它只能通过元素节点对象调用
```javascript
var paras = document.getElementsByTagName("p");
for(var i=0; i<paras.length; i++){
    var title_text = paras[i].gatAttribute("title");
    if(title_text) alert(title_text);//简写形式
}
//解释：如果p标签上没有title属性，则会返回null值，通过if语句判断是否有值，只有当有值的时候才执行alert，if(title_text != null){alert(title_text);}是上面的语句的完整写法；
```
### 5.2 setAttribute ###
语法`object.setAttribute(attribute,value)`
如果元素上原先没有需要赋值的属性，那么setAttribute会先创建这个属性，然后设置它的值；如果setAttribute用在一个本身就有这个属性的元素节点上，这个属性的值就会被覆盖掉；
```javascript
var paras = document.getElementsByTagName("p");
for(var i=0; i<paras.length; I++){
    var title_text = paras[i].getAttribute("title");
    if(title_text){
        paras[i].setAttribute("title","新的标题");
        alert(paras[i].getAttribute("title"));
    }
}
```
## 6. 小结 ##
DOM的五个方法：getElementById、getElementsByTagName、getElementsByClassName、getAttribute、setAttribute;
DOM的其他属性和方法：nodeName、nodeValue、childNodes、nextSibling和parentsNode等；
# 四、案例研究：JavaScript图片库 #
DEMO:[index.html](http://oboiq86te.bkt.clouddn.com/gellery/index.html)
## 1. 标记 ##
使用ul》li>a建立一个无需列表；
## 2. JavaScript ##
```javascript
function showPic(whichpic){
    var source = whichpic.getAttribute("href");
    var text = whichpic.getAttribute("title");
    //两种实现赋值的方法
    //使用setAttribute赋值（setAttribute方法是“第一级DOM”的组成部分，它可以设置任意元素节点的任意属性）
    placeholder.setAttribute("src",source);

    //非DOM解决方案（可以解决大部分元素的属性）
    //placeholder.src = source;
}
```
## 3. 应用这个JavaScript函数 ##
`onclick= showPic(this);return false;`
## 4. 对这个函数进行扩展 ##
让图片链接的title属性显示在页面上；
### 4.1 childNodes ###
在一棵节点树上，childNodes属性可以用来获取任何一个元素的所有子元素，他是一个包含这个元素全部子元素的数组：`element.childNodes`，获取body原色的全体子元素，使用`document.getElementsByTagName("body")[0].childNodes`
### 4.2 nodeType属性 ###
由childNodes属性返回的数组包含所有类型的节点，不仅仅是元素节点。事实上，文档里几乎每一样东西都是一个节点，甚至连空格和换行符都会被解释为节点，而它们也包含在childNodes属性所返回的数组中；  
每一个节点都有nodeType属性`node.nodeType`，nodeType的值是一个数字，共有12种可取值，其中：①元素节点的nodeType属性值是1；②属性节点的nodeType属性值是2；③文本节点的 nodeType属性值是3；   
### 4.3 在标记里增加一段描述 ###
定义一个文本节点，在显示图片时，把这个文本节点的值，替换成目标图片链接的title值；
### 4.4 用JavaScript改变这段描述 ###
```javascript
    //首先，获取whichpic对象的title属性值，并赋值给变量
    var text =whichpic.getAttribute("title");
    //创建新的变量存放文本段落
    var description = document.getElementById("description");
```
### 4.5 nodeValue属性 ###
nodeValue属性得到（和设置）一个节点的值`node.nodValue`；   
在用nodeValue属性获得description属性的值时，得到的并不是包含在这个段落里的文本，而是返回一个null值； p元素里的文本，是p元素的第一个子节点，要想获取p元素的文本值，用`description.childNode[0].nodeValue`;
### 4.6 firstChild和lastChild属性 ###
数组元素childNodes[0]有个更直观易读的同义词firstChild；   
node.lastChild代表这childNodes数组的最后一个元素，等同于node.childNodes[node.childNodes.length - 1];
### 4.7 利用nodeValue属性刷新这段描述 ###
使用`description.firstChild.nodeValue = text;`可以刷新描述文字
# 五、最佳实践 #
## 1. 过去的错误 ##
- 不要怪罪JavaScript：不是语言的问题，而是使用语言的问题；
- Flash的遭遇：没有不好的技术，只有没有用好的技术； 
- 质疑一切：使用JavaScript时考虑是否必要？对用户的浏览体验产生怎样的影响？浏览器不支持JavaScript怎么办？
## 2. 平稳退化 ##
让浏览器不支持JavaScript的情况下仍能顺利地浏览网页，这就是所谓的平稳退化；
- "JavaScript:"伪协议：通过一个链接调用JavaScript函数，`如<a href="javascript:popup('http://www.baidu.com')";>baidu</a>`；**“真”协议用来在因特网上的计算机之间传输数据包，如HTTP协议（http://）、FTP协议（ftp://）等，伪协议则是一种非标准化的协议；**
- 内嵌的事件处理函数：`如<a href="#" onclick="popup('http://www.baidu.com');return false;">baidu</a>`；
- 谁关心这个：搜索引擎、用户等；
## 3. 像CSS学习 ##
- 结构和样式的分离
- 渐进增强：就是用一些额外的信息层去包裹原始数据；按照“渐进增强”原则创建出来的页面几乎都符合“平稳退化”原则；
## 4. 分离JavaScript ##
JavaScript代码和HTML文档分离，文档里面的JavaScript属性也进行分离；   
通过window.onload加载函数；
## 5. 向后兼容 ##
- 对象检查：`if(method){statements}`,使用`if(!method) return false;`更好；如果需要检查多个方法或属性是否存在，可以用`if (!method-one || method-two) return false;`
- 浏览器嗅探技术：指通过提取浏览器供应商提供的信息来解决向后兼容问题，这是一种风险非常大的技术（原因：①浏览器有时会“撒谎”；②为了适应多种不同的浏览器，嗅探脚本会变的越来越复杂；③许多浏览器嗅探脚本在进行这类测试时要求浏览器的版本号必须得到精确的匹配；）
## 6. 性能考虑 ##
- 尽量少访问DOM和尽量减少标记；
- 合并和放置代码：多代码合并到一个文件，放到</body>的前面；
- 压缩脚本；
# 六、案例研究：图片库改进版 #
## 1. 平稳退化 ##
```html
//代码1：
<a href="images/one.jpg" onclick="showPic(this);return false;" title="A">Fireworks</a>
//代码2：
<a href="javascript:showPic('images/one.jpg');return false;" title="A">Fireworks</a>
//代码3：
<a href="#" onclick="showPic('images/one.jpg');return false;" title="A">Fireworks</a>

代码1能够平稳退化，代码2和代码3不可以；
```
## 2. JavaScript和HTML标签分离 ##
上面的代码1没能做到，如何添加：
### 2.1 添加事件处理函数 ###
```javascript
//定义函数
function prepareGallery(){
    if(!document.getElementsByTagName || !document.getElementById) return false;
    if(!document.getElementById("imagegallery"))return false;
    var gellery = document.getElementById("imagegallery");
    var links = gellery.getElementsByTagName("a");
    for(var i=0; i<links.length; i++){
        links[i].onclick = function(){
            //判断是否能够正常执行showPic的函数，并进行取反，如果正常执行函数，那么取消默认事件；否则执行默认事件；
            //return !showPic(this);
            return showPic(this)?false:true;
        }
        //键盘访问
        links[i].onkeypress = links[i].onclick;
    }
}
1. 检查点：确保当前浏览器能够执行正常运行DOM方法，如果无法使用则不执行此函数；
2. 定义变量，减少工作量；
3. 遍历处理links数组里的各个元素，用for循环完成；
4. 通过onclick事件添加匿名函数，改变各个元素的行为；
```
### 2.2 共享onload事件 ###
如下面代码所示，页面上有两个（或更多）函数同时绑定在onload事件上，只有最后那个才能被实际执行；
```javascript
window.onload = firstFunction;
window.onload = secondFunction;
```
通过匿名函数可以容纳两个（或更多）函数,能够解决不能同时执行的问题，但是在需要绑定的函数有很多场合需要的时候，不能很好的工作（必须写在一起，而不能随时随地的执行）；
```javascript
window.onload = function (){
    firstFunction();
    secondFunction();
}
```
定义一个函数共享onload事件：
```javascript
function addLoadEvent(func){
	var oldonload = window.onload;
	if(typeof window.onload != 'function'){
		window.onload = func;
	}else{
		window.onload = function(){
			oldonload();
			func();
		}
	}
}
addLoadEvent(firstFunction);
addLoadEvent(secondFunction);
```
## 3. 不要做太多的假设 ##
修改showPic函数，需要对元素做检查
```javascript
function showPic(whichpic){
	if(!document.getElementById("placeholder")) return false;
	var source = whichpic.getAttribute("href");	
	var placeholder = document.getElementById("placeholder");
	placeholder.setAttribute("src",source);
	if(document.getElementById("description")){
		var text = whichpic.getAttribute("title");
		var description = document.getElementById("description");		
		description.firstChild.nodeValue = text;
	}
	return true;
}
```
## 4. 优化 ##
```javascript
//检查title属性是否存在
var text = whichpic.getAttribute("title")?whichpic.getAttribute("title"):"";
//检查图片是否存在
if(placeholder.nodeName != "IMG") return false;
//检查是否是文本元素
if(description.firstChild.nodeType == 3){
    description.firstChild.nodeValue = text;
}
```
## 5. 键盘访问 ##
```javascript
 links[i].onclick = function(){
    return showPic(this)?false:true;
}

 links[i].onkeypress = function(){
    return showPic(this)?false:true;
}
//上面的代码可以简化为
links[i].onkeypress = links[i].onclick;
```
## 6. 把JavaScript与CSS结合起来 ##
css引入外部文件
## 7. DOM Core和HTML-DOM ##
getElementById、getElementsByTagName、getAttribute、setAttribute，这些方法都是DOM Core的组成部分，它们并不属于JavaScript，支持DOM的任何一种程序设计语言都可以使用它们，它们的用途并非仅限于处理网页，它们可以用来处理任何一种标记语言（如XML）编写出来的文档；   
属性onclick属于HTML-DOM，HTML-DOM提供了许多描述各种HTML元素的属性，例如
```
document.getElementsByTagName("form")
简化为：
documents.forms

element.getAttribute("src")
简化为：
element.src

element.setAttribute("src",source)
简化为：
element.src = source;
```
HTML-DOM代码通常会更短，但是它们只能用来处理Web文档；
# 七、动态创建标记 #
## 1. 一些传统的方法 ##
document.write和innerHTML
- document.write最大的缺点是它违背了“行为应该与表现分离”的原则；通过document.write创建的文档容易导致验证错误；MIME类型applocation/xhtml+xml与document.write不兼容，浏览器在程序这种XHTML文档时根本不会执行document.write方法；
- innerHTML属性不是W3C DOM标准的组成部分，不过已经包含在HTML5规范中，它可以用来读、写某给定元素的HTML内容；innerHTML只能进行赋值，如果被赋值的元素有内容，则会替换；innerHTML属性比document.write()方法耿直的推荐；innerHTML也是HTML专有属性，不能用于任何其他标记语言文档,这一点和document.write方法一样；(DEMO:[test.html](http://oboiq86te.bkt.clouddn.com/gellery/test.html))
## 2.DOM方法 ##
DOM是文档的表示，是一条双向车道；DOM不仅可以获取文档的内容，还可以更新文档的内容；在浏览器看来，DOM节点数才是文档；    
- `document.createElement(nodeName)`用来创建元素节点；
- 把新创建的节点插入某个文档的节点数的最简单的方法是让它成为这个文档某个现有节点的一个子节点，可以使用`parent.appendChild(child)`来实现；
- `document.createTextNode(text)`用来创建一个文本节点；
## 3. 重回图片库 ##
### 3.1 在已有元素前插入一个新元素 ###
DOM提供了名为insertBefore()方法，这个方法把一个新元素插入到一个现有元素的前面，使用`parentElement.insertBefore(newElement,targetElement)`来调用，在调用此方法时，需要告诉它三件事：
- 新目标：你想插入的元素（newElement）；
- 目标元素：你想把这个新元素插入到那个元素（targetElement）之前；
- 父元素：目标元素的父元素（parentElement）； 

我们不必搞清楚父元素到底是哪个，因为targetElement元素的parentNode属性值就是它，所以`parentElement`可以用`targetElement.parentNode`来替换；     
### 3.2 在现有方法后插入一个新元素 ###
DOM没有提供现成的方法，需要进行编写；
```javascript
//首先，函数有两个参数，一个是将被插入的新元素（newElement）,另一个是目标元素（targetElement）；
function  insertAfter(newElement,targetElement){
//把目标元素的parentNode属性值包含到变量parent里
    var parent = targetElement.parentNode;
//接下来，检查目标元素是不是parent的最后一个子元素，即比较parent元素的lastChild属性值与目标元素是否存在“等于”关系
    if(parent.lastChild == targetElement){
//如果是，就用appendChild方法把新元素追加到parent元素上，这样新元素就恰好被插入到目标元素之后
        parent.appendChild(newElement);    
    }else{
//如果不是，就把新元素插入到目标元素和目标元素的下一个兄弟元素之间；目标元素的下一个兄弟元素即目标元素的nextSibling属性；用insertBefore方法把新元素插入到目标元素大的下一个兄弟元素之前；
        parent.insertBefore(newElement,targetElement.nextSibling);
    }
}
```
上面编写的函数用到了以下DOM方法和属性：parentNode属性、lastChild属性、appendChild方法、insertBefore方法、nextSibling属性；   
## 4. Ajax ##               
Ajax的主要优势就是对页面的请求以异步的方式发送到服务器；Ajax依赖JavaScript；搜索引擎的蜘蛛程序也不会抓取到Ajax的有关内容；    
Ajax技术的核心就是XMLHttpRequest对象，这个对象充当着浏览器中的脚本（客户端）与服务器之间的中间人的脚色；以往的请求都是有浏览器发出，而JavaScript通过这个对象可以自己发送请求，同事也自己处理响应；    
不同的浏览器实现XMLHttpRequest对象的方式不太一样，为了保证跨浏览器，需要进行兼容性JavaScript代码编写：
```javascript
function getHTTPObject(){
    if(typeof XMLHttpRequest == "underfinde")
        XMLHttpRequest = function(){
            try {return new ActiveXObject("Msxml2.XMLHTTP.6.0");}
                catch(e){}
            try {return new ActiveXObject("Msxml2.XMLHTTP.3.0");}
                catch(e){}
            try {return new ActiveXObject("Msxml2.XMLHTTP");}
                catch(e){}
            return false;
        }
    return new XMLHttpRequest();
}
```
XMLHttpRequest对象有许多的方法，最有用的是open方法，它用来指定服务器上要访问的文档，请求指定类型：GET、POST和SEND，这个方法的第三个参数用来指定请求是否以异步的方式发送和处理；
```javascript
function getNewContent(){
    var request = getHTTPObeject();
    if(request){
        request.open("GET","需要获取的文件url",true);
        request.onreadystatechange = function(){
            if(request.readyState == 4){
                //如果成功,执行此代码
            }
        };
        request.send(null);
    }else{
        alert("Sorry,your browser doesn\'t support XMLHttpRequest");
    }
}
addLoadEvent(getNewContent);
```
需要获取的文件url：这个可以使用绝对定位，也可以使用相对定位，如果不在同一个域名下面的话会出现跨域问题，只能获取相同域名下面的数据；有些浏览器会限制Ajax请求使用的协议；   
服务器在向XMLHttpRequest对象发回响应时，该对象有多种属性可用，浏览器会在不同阶段更新readyState属性的值，它有5个可能的值：0表示未初始化，1表示正在加载，2表示加载完成，3表示正在交互，4表示完成；只要readyState属性的值变成了4，就可以访问服务器发送回来的数据了；     
访问服务器发回来的数据要通过两个属性完成；一个是reponseText属性，这个属性用于保存文本字符串形式的数据；另一个属性是responseXML属性，用于保存Content-Type头部中指定为“text/xml”的数据，是其是一个DocumentFragment对象；     
构建Ajax网站的最好方法，是先构建一个常规网站，然后Hijax（渐进增强地使用Ajax）它；    
DEMO:[ajax.html](http://oboiq86te.bkt.clouddn.com/gellery/ajax.html)
# 八、充实文档的内容 #
## 1. 不应该做什么 ##
应该时刻牢记两项原则：渐进增强和平稳退化；不要通过JavaScript把重要的内容添加到网页上，这样一来JavaScript就没有任何空间去平稳退化了；
## 2. 把“不可见”变成“可见” ##
绝大多数属性的内容（即属性值）在Web浏览器里都是不显示的，只有极少数属性例外，但不同的浏览器在呈现这些属性的时候却常常千态百姿；比如title属性和alt属性；
## 3. 内容 ##
- 选用标记语言：使用HTML、XHTML、HTML5都可以，推荐使用HTML5，它的文档声明类型非常简单，并且向下兼容；
- CSS：可以自定义CSS样式；
- JavaScript：使用DOM改变浏览器的默认行为，比如让title属性集中显示；
## 4. 显示“缩略语列表”（实例） ##
实现方法:
1. 编写displayAbbreviations函数：遍历文档中的所有abbr元素，保存每个abbr元素的title属性及包含的文本；
2. 创建标记：创建一个“定义列表”元素（dl）,遍历刚刚保存的title属性和abbr元素的文本；创建一个“定义标题”元素（dt），把abbr元素的文本插入到这个dt元素；创建一个“定义描述”元素（dd）,把title属性插入到这个dd元素；把dt元素追加到dl元素上，把dd元素追加到dl元素上；
3. 添加到文档：把dl元素追加到文档的body元素上并检查兼容性；

注意：低版本的IE浏览器（IE6及以前）不支持abbr元素，需要做到平稳退化；    
显示“文献来源链接表”同上面的显示“缩略图列表”；    
DEMO:[explanation.html](http://oboiq86te.bkt.clouddn.com/gellery/explanation.html)
# 九、CSS-DOM #
## 1. 三位一体的页面 ##
网页是有一下三层信息构成的一个共同体，并且进行分离：
- 结构层：由HTML、XHTML或HTML5之类的标记语言负责创建；
- 表示层：由CSS负责完成，用来描述页面内容应该如何呈现；
- 行为层：负责内容应该如何相应事件这一问题，这是JavaScript语言和DOM主宰的领域；
## 2. style属性 ##
```
<p id="example" style="color:grey;font-family:'Arial',sans-serif;">An example of a paragraph</p>

var para = document.getElementById("example);
alert(typeof para.nodeName);//返回字符串“string”
alert(typeof para.style);//返回字符串“object”
alert("This color is"+ para.style.color);//返回值“grey”
alert("This font-family is"+ para.style.fontFamily);//返回值“Arial',sans-serif”
para.style.color = "black";//设置样式
```
不管css样式属性的名字有多少个连字符，DOM一律采用驼峰命名法来表示它们；   
style属性只能返回内嵌样式；
通过`element.style.property=value`设置样式；   
DEMO:[example.html](http://oboiq86te.bkt.clouddn.com/gellery/example.html)
## 3. 何时该用DOM脚本设置样式 ##
- 根据元素在节点树里的位置来设置样式：遍历所有的h1（可以是其它元素）元素，把当前h1元素的下一个节点找出来，把这个选择的节点进行赋值；
- 根据某种条件反复设置某种样式：遍历所有的table元素，对每个table元素创建odd变量并把它初始化为false；遍历这个表格的所有数据行；如果变量odd的值为true，设置样式并把odd变量修改为false；如果变量odd的值为false，设置样式并把odd变量修改为true；
- 响应事件：类似:hover实现的效果，通过JavaScript实现；在这一类场合，需要利用DOM设置样式还是采用纯粹的CSS来解决需要考虑一下因素：①这个问题最简单的解决方案是什么；②哪种解决方案会得到更多的浏览器支持；    
DEMO:[story.html](http://oboiq86te.bkt.clouddn.com/gellery/story.html) / [itinerary.html](http://oboiq86te.bkt.clouddn.com/gellery/itinerary.html)
## 4. className属性 ##
通过`elem.className = name`设置某个元素的class样式，但这样是替换（而不是追加）该元素原有的class样式；   
通过`elem.className += name`可以利用字符串拼接操作，把新的class设置追加到className属性上去（主要name的一个字符是空格，比如" intro"）,但只有在原来确实有一个class的情况下才能这么做；    
在需要给一个元素追加新的class时，可以按照以下步骤操作：
检查className属性的值是否为null；如果是，把新的class属性值直接赋值给className属性；如果不是，把一个空格和新的class设置值追加到className属性上去；

把函数进行抽象，能够使一个非常具体的东西改进为一个较为通用的东西；
# 十、用JavaScript实现动画效果 #
## 1. 动画基础知识 ##
- 位置：通过设置position、left、top等值进行定位；
- 时间：setTimeout能够让某个函数在经过一定预定的时间之后才开始执行`var variable = setTimeout("function",interval)`；想要取消某个正在排队等待执行的函数，必须事先把setTimeout函数的返回值赋值给一个变量`clearTimeout(variable)`；
- 时间递增量：让元素的移动等以渐变的方式发生：①获取元素的当前位置；②如果元素已经到达目的地，则退出这个函数；如果元素尚未到达目的地，则把它向目的地移近一点；④经过一段时间间隔之后从步骤①开始重复上述步骤；
- 抽象：把一个只能完成一下非常特定任务的函数改成一个能够通用的函数，这就是抽象了，比如把一些常量变为变量；    
DEMO:[message.html](http://oboiq86te.bkt.clouddn.com/gellery/message.html)    
DEMO:[list.html](http://oboiq86te.bkt.clouddn.com/gellery/list.html)
# 十一、HTML5 #
## 1. HTML5简介 ##
结构层、样式层和行为层共同构成了一个网页，共同组成了HTML5；   
- 在结构层，HTML5添加了新的标记元素，如`<section>、<article>、<header>、<footer>`；HTML5还提供了更多交互及媒体元素，例如`<canvas>、<audio>、<video>`；表单得到了加强，新增了颜色拾取器、数据拾取器、滑动条和进度条；(DEMO:[canvas.html](http://oboiq86te.bkt.clouddn.com/gellery/canvas.html) / [grayscale.html](http://oboiq86te.bkt.clouddn.com/gellery/grayscale.html))
- 在行为层，HTML5规定了DOM中每个元素的交互方式，以及新的API；新JavaScript API还包含其他很多模块，比如Geolocation、Storage、Drap-and-Drop、Socket以及多线程等；(DEMO:[movie.html](http://oboiq86te.bkt.clouddn.com/gellery/movie.html))
- 在表现层，CSS3的多个模块囊括了高级选择器、渐变、变换，还有动画；
## 2. 来做朋友的忠告 ##
Modernizr是一个开源的JavaScript库，利用它的富特性检测功能，可以对HTML5文档进行更好的控制；
HTML5在低版本的浏览器上支持不好，需要进行降级处理，平稳退化；HTML5需要Safari 5+、Chrome 6+、Mozilla Firefox 3.6+、Opera 10.6+、IE 9+；
## 3. 几个示例 ##
- Canvas：可以动态创建和操作图形图像；
- video和audio：视频和音频，对于视频格式的支持有点问，目前主要有Ogg、MP4、WebM等格式；可以进行自定义控件；
- 表单：HTML5中新的输入类型包括email、url、date、number、range、search、tel、color等；HTML5中新增的表单属性包括autocomplete、autofocus、form、min、max、step、pattern、placeholder、required等；需要对浏览器进行兼容性测试；

