---
title: "jsonp原理"
date: 2014/3/26 18:00:00
description: ""
category: ""
tags: ["jsonp"]
---
首先解释一个名词Same-Origin Policy，即同源策略，
指**JavaScript只能访问与包含它的文档在同一域下的内容。**  
如果碰到一个需求，比如说ajax从http://a.com上拿数据，处理完之后在http://b.html显示。
那肯定显示不出来的，因为Same-Origin Policy。这个时候就可以使用**jsonp**。  
原理慢慢说，首先认识下哪些东西可以跨域：

```javascript
<script src="..."></script>标签嵌入跨域脚本。
<link rel="stylesheet" href="...">标签嵌入CSS。
<img>嵌入图片。
<video> 和 <audio>嵌入多媒体资源。
<object>, <embed> 和 <applet>的插件。
@font-face引入的字体。一些浏览器允许跨域字体（ cross-origin fonts），一些需要同源字体（same-origin fonts）。
 <frame> 和 <iframe>载入的任何资源。
```

jsonp嘛，使用的就是`<script>` 标签的`src` 属性进行跨域的。这个很容易理解，比如：

```javascript
<script type="text/javascript" src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
```
像这样的跨域src写法，我们肯定没少写过。所以说`<script>` 标签的`src` 属性可以跨域，是不难理解的。
现在举个例子，假设当前页面的地址是`http://natasg.github.io/air/index.html`，而且这个index.html中引用到了下面这个js：

```javascript
<script type="text/javascript" src="http://iremember.duapp.com/remote.js"></script>
```
这个js中的内容是：
```javascript
alert("I'm remote");
```
当index.html页面loaded之后，浏览器会弹出这个提示框,打印出"I'm remote"。  
那如果remote.js中的内容是：
```javascript
parseData({"id":1,"name":"natasg"});
```
而且index.html页面中有以下代码：
```javascript
	<script>
		function parseData(data){
			alert(data.id+" "+data.name);
		}
	</script>
```
这种情况下，当index.html页面loaded之后，浏览器会发生什么事情呢？  
当然，浏览器会弹出一个对话框，打印出"1 natasg"。

####OK，现在就说说jsonp的思路。
1.首先，在客户端编写js代码，用来处理服务器传回来的数据。（听起来跟ajax一模一样）如上面的:
```javascript
	<script>
		function parseData(data){
			alert(data.id+" "+data.name);
		}
	</script>
```
2.然后，在服务端将数据以类似`parseData(data);`的格式拼装。比如：
```java
	@RequestMapping("getJsonp")
	public void getJsonP(HttpServletRequest request, HttpServletResponse response) {
		response.setContentType("application/javascript");
		try {
			response.getWriter().print("parseData({'id':1,'name':'natasg'});");
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
```
3.在客户端将第二步服务端的请求写入`<script>`标签的`src`属性。如：
```javascript
	var url="http://iremember.duapp.com/getJsonp.htm";
	// 创建script标签，设置其属性
    var script = document.createElement('script');
    script.setAttribute('src', url);
    // 把script标签加入head，此时调用开始
    document.getElementsByTagName('head')[0].appendChild(script);
```
如此，在index.html加载完成之后，浏览器就会打印出"1 natasg"。  
这个就是jsonp的实现原理,jQuery对$.ajax()做了处理，支持jsonp操作。  
**但是请明白，jsonp跟ajax本质上完全是两码事**。
jQuery中使用jsonp如下：
```javascript
	$.ajax({
	    url: "http://iremember.duapp.com/getJsonp.htm",

	    jsonp: "callback",

	    dataType: "jsonp",

	    data: "",

	    success: function( data ) {

	    }
	});
```
其中,
1. url：服务端请求地址。
2. dataType：设置为jsonp表示客户端以jsonp格式获取服务端返回的数据。
3. data：客户端向服务端传递的参数。
4. jsonp：callback名称可以自定义，表示回调函数名，服务端必须提供同名函数返回，客户端会在success中对函数中的参数进行处理。
5. success：data为服务端返回的javascript函数的参数，此方法即为客户端处理jsonp数据的方法。
