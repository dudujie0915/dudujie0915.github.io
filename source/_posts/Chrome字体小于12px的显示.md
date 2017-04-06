---
title: Chrome字体小于12px的显示
date: 2017-03-31 16:23:43
tags: ['浏览器','CSS','HARK']
categories: HARK
---
在IE、Firefox浏览器下，字体可以小于12px显示，但是在Chrome浏览器下字体最小显示为12px，但是有时候需要显示小于12px的字体，如何显示呢？
**历史解决方案：**`-webkit-font-size-adjust:none;`,新版浏览器已经不支持了；    
**现在解决方案：**配合html，-webkit-transform:scale(num)来解决问题
```html
<p><span>字体为10px</span></p>
<style>
p span{font-size:10px;-webkit-transform:scale(0.8);display:inline-block;}
</style>
/*
* 如果<p>元素有背景的话，transform会是背景随之变化，所有嵌套一个<span>；
* 因为transfrom只为可以缩放可以定义宽高的元素起作用，<span>是行内元素，所有设置display:inline-block;
*/
```