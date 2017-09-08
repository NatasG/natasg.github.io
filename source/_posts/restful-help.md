---
title: "restful api"
date: 2014/6/11 18:00:00
description: ""
category: ""
tags: []
---
#协议
	HTTP或HTTPS协议
#域名
	https://api.example.com

如果api比较简单，可以考虑放在主域名下。

	https://www.example.com/api/

#版本
API的版本号应该放入URL中。

	https://www.example.com/api/v1/

另一种做法是，将版本号放在HTTP头信息中，但不如放入URL方便和直观。

#HTTP动词
常用的HTTP动词有下面五个(括号里是对应的SQL命令)。

	 GET(SELECT):从服务器取出资源（一项或多项）。
	 POST(CREATE):在服务器新建一个资源。
	 PUT(UPDATE):在服务器更新资源（客户端提供改变后的完整资源）。
	 PATCH(UPDATE):在服务器更新资源（客户端提供改变的属性）。
	 DELETE(DELETE):从服务器删除资源。

 还有两个不常用的HTTP动词。

	HEAD:获取资源的元数据。
	OPTIONS:获取信息，关于资源的哪些属性是客户端可以改变的。

api例子：

	GET /zoos：列出所有动物园
	POST /zoos：新建一个动物园
	GET /zoos/ID：获取某个指定动物园的信息
	PUT /zoos/ID：更新某个指定动物园的信息（提供该动物园的全部信息）
	PATCH /zoos/ID：更新某个指定动物园的信息（提供该动物园的部分信息）
	DELETE /zoos/ID：删除某个动物园
	GET /zoos/ID/animals：列出某个指定动物园的所有动物
	DELETE /zoos/ID/animals/ID：删除某个指定动物园的指定动物
