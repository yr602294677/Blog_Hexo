---
title: ## 编写bat文件启动jar
date: 2019-10-09 15:47:44 
categories: "日常积累" 
tags: -日常积累
description: ## 编写bat文件启动jar

---



1、新建一个名为demo.bat，打开编辑，写入以下内容

``` xml
cd /d E:/demo
java -jar demo.jar
exit

```

 注意，如果cd失败，可以加上/d

2、保存。下次启动时就可以直接点击demo.bat启动了。

