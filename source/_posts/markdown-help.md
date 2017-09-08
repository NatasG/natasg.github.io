---
title: "Markdown基本语法"
date: 2013/7/13 20:46:25
description: ""
category: ""
tags: ["markdown","help"]
---
<!-- Markdown的目标实现是**[简单易读]** -->

Markdown 的目标是：**成为一种适用于网络的书写语言**
####特殊字符的替换

在HTML文件中，有两个字符需要特殊处理: `<` 和 `&` 。其中 `<` 用于起始标签 。 `&` 用于标记 HTML 实体。
Markdown会自动识别这两个字符，如果你使用的 `&` 字符是 HTML 字符实体的一部分，它会保留原状，否则它会被转换成 `&amp;`。  
如果要插入一个版权符号 &copy;，可以这样写：

	&copy;
如果想输入这样的字符A&T，直接写：

	A&T
####段落和换行
*段落* 是最基本的元素，无任何标记。  
*换行* 有两种方式：
1. 段落末尾插入两个或以上的空格，然后回车。相当于`<br/>`
2. 段落末尾敲入两个回车。相当于另起一个`<p>`  
####标题
Markdown 支持两种标题的语法。第一种是任意数量的`=`或任意数量的`-` ，表示`h1`或`h2` ,如：

	I'm h1
	===========
表示：
I'm h1
===========
第二种语法是：在行首插入1到6个`#` ，分别表示`h1` 到`h6` ，如：

	#I'm h1
	##I'm h2
	###I'm h3
	####I'm h4
	#####I'm h5
	######I'm h6
表示：
#I'm h1
##I'm h2
###I'm h3
####I'm h4
#####I'm h5
######I'm h6

####区域Blockquotes
Markdown中的区域引用使用类似email中用`>`的方式，如：

	>I'm first Blockquotes
	>I'm first Blockquotes
	>I'm first Blockquotes
	>>I'm second Blockquotes
	>I'm first Blockquotes

	也可以偷懒写为：

	>I'm first Blockquotes
	I'm first Blockquotes
	I'm first Blockquotes
	>>I'm second Blockquotes
	>I'm first Blockquotes
表示：
>I'm first Blockquotes
>I'm first Blockquotes
>I'm first Blockquotes
>>I'm second Blockquotes
>I'm first Blockquotes  
####列表
列表分为两种，无序列表的语法是：`*` `+` 或者`-` 作为标记，如：

	 * ul li 1
	 * ul li 2
	 * ul li 3

	或者

	 ＋ ul li 1
	 ＋ ul li 2
	 ＋ ul li 3

	或者

	 － ul li 1
	 － ul li 2
	 － ul li 3
表示：
* ul li 1
* ul li 2
* ul li 3  

有序列表的语法是:`1.` 数字加句号作为标记，如：

	 1. ol li 1
     2. ol li 2
     3. ol li 3

     或者

     1. ol li 1
     1. ol li 2
     1. ol li 3

     或者

     9. ol li 1
     2. ol li 2
     1. ol li 3
都表示：
1. ol li 1
2. ol li 2
3. ol li 3  

####代码区域
代码区域就是文章中的源代码引用。首先解释代码，如：

	`code`
表示：
`code`,
代码区域就是用`<pre>` 和`<code>`包围起来的内容。  
代码区域的语法为：文本之前使用4个空格或者一个tab缩进，如：

	I'm a p.

		String hello="Hello World!";
		System.out.print(hello);
表示：  
I'm a p.

	String hello="Hello World!";
	System.out.print(hello);
`注意`：**列表元素需要多加一个空格。**
####分割线
你可以在一行中用三个以上的`*` `-` 或者`_`来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。效果如下：

--------
上面是条分割线
####强调
被一个`*` 或者`_`包围，相当于被`<em>`包围，被两个`*` 或者`_`包围，相当于被`<strong>`包围。如：

    hello kitty!
	*hello kitty!*
	_hello kitty!_
	**hello kitty!**
	__hello kitty!__
效果如下：
hello kitty!
*hello kitty!*
_hello kitty!_
**hello kitty!**
__hello kitty!__
####链接
链接有两种语法，*行内式* 和 *参考式* ，其中行内式的语法如下：

	This is [natas's github url](https://github.com/natasg "Natasg") inline link.

	[natas's github url with no title](https://github.com/natasg "Natasg") has no title attribute.

	这个链接指向本目录资源,[NatasAir](/air)
表示：
This is [natas's github url](https://github.com/natasg "Natasg") inline link.

[Natas's github url with no title](https://github.com/natasg "Natasg") has no title attribute.

这个链接指向本目录资源,[NatasAir](/air)  
参考式的语法如下：

	CSS [表格] [table].
	CSS [主页] [home].
	CSS [表单] [form].

	[table]: http://natasg.github.io/zen/table.html "表格的标题"
	[home]: http://natasg.github.io/zen/home.html "主页的标题"
	[form]: zen/form.html "表单的标题"
表示：
1. CSS [表格] [table].  
2. CSS [主页] [home].  
3. CSS [表单] [form].  

[table]: http://natasg.github.io/zen/table.html "表格的标题"
[home]: http://natasg.github.io/zen/home.html "主页的标题"
[form]: /zen/form.html "表单的标题"

参考式还可以这样写：

	[table]: http://natasg.github.io/zen/table.html "表格的标题"
	[home]: http://natasg.github.io/zen/home.html '主页的标题'
	[form]: zen/form.html (表单的标题)

	网址也可以用方括号括起来。
	[table]: <http://natasg.github.io/zen/table.html> "表格的标题"
**链接辨别标签可以有字母、数字、空白和标点符号，但是并不区分大小写。**
还可以使用隐式链接，这种情形下，链接标记会视为等同于链接文字：

	[Google][]

	[Google]: http://google.com/
还有自动链接：

	<http://example.com/>
	相当于html代码：
	<a href="http://example.com/">http://example.com/</a>
####图片
Markdown 使用一种和链接很相似的语法来标记图片，同样也允许两种样式： 行内式和参考式。如：

	![狗狗](/images/k.jpg)

	![狗狗](/images/k.jpg "阿黄")

	![狗狗][dog]

	[dog]:/images/k.jpg "阿黄"

表示：  
![狗狗](/images/k.jpg)

![狗狗](/images/k.jpg "阿黄")

![狗狗][dog]

[dog]:/images/k.jpg "阿黄"
####反斜杠
Markdown 可以利用反斜杠来插入一些在语法中有其它意义的符号，目前支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

	\   反斜线
	`   反引号
	 *   星号
	_   底线
	{}  花括号
	[]  方括号
	()  括弧
	#   井字号
	 +   加号
	 -   减号
	.   英文句点
	!   惊叹号
