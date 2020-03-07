---
title: Clean Code
date: 2019-09-29 23:47:44 
categories: "读书笔记" 
tags: -读书笔记
description: 《代码整洁之道》读书笔记
---

> *一个函数应该只做一件事。*

前言：虽然这本书现在在我看来没啥用，因为日常代码不可能让你仔细雕琢（虽然这句话不对，但现实情况就是这样。），但还是记录一下自己看书的收获，省的看了就忘，顺便用我的新键盘打打字。

1.抽离Try/Catch代码块

```java
public void delete(Page page){//只与错误处理有关
	try{
		deletePage(page);	
    }catch{
		logError(e);
	}
}
private void deletePage(page) throws Excepyion{//核心逻辑
    deletePage(page);
}
private void logError(Excepyion e){//捕获异常
    Logger.log(e.getMessage());
}
```

2.将重复出现的代码整合到一个函数中再调用。

3.对象暴露行为，隐藏数据，便于增加新对象类型而无需改变现有行为。

  数据结构暴露数据，没有明显的行为，便于向既有数据结构中国增加新行为。

```java
public class Point(){
    public double x;
    public double y;
}
```

```

```

4.使用异常替代返回错误码。