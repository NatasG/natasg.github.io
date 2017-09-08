---
title: "jekyll常用命令"
date: 2014/3/25 18:00:00
category: ""
tags: ["jekyll","help"]
---
启动jekyll服务

	jekyll serve

启动jekyll服务（**支持动态修改代码**）

	jekyll serve -w

创建post

	rake post title="post的名字"

创建page

	rake page name="page的名字"
	 1. rake page name="page1.html"
	 2. rake page name="page2.md"
	 3. rake page name="pages/page3" `这个将会生成./pages/page3/index.html`


通过git发布

	 1. git add .
	 2. git commit -m "Add new content"
	 3. git push origin master
