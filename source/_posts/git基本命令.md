---
title: git基本命令
date: 2019-09-29 23:47:44 
categories: "日常积累" 
tags: 日常积累
description: git操作命令记录

---



####  1.本地

1. git add -A  :往本地仓库保存

2. git commit -m "提交备注信息" :往本地仓库提交

3. git push ：往github提交

4. 在一个新的文件夹里往现有的工程进行提交

   ```java
//初始化
   $git init 
   //提交 add-commit
   $git add -A
   $git commit -m "message"
   //关联仓库
   $ git remote add origin git@github.com:yr602294677/yrHeart.git
   // --allow-unrelated-histories 允许无关提交历史
   $ git pull origin master --allow-unrelated-histories
   //推送至仓库
   $git push origin master
   //这样会在本地建一个新的仓库
   
   ```
   
   5.退出vim编辑器：先按esc，再输入 :x  。 
   
   6.contribution在github不显示，可能是邮箱问题。
   
   $git show    展示当前邮箱
   
   <img src="./gitshow.png" style="zoom:60%" />
   
   然后在github将本邮箱添加进去
   
   <img src="./设置github邮箱.png" style="zoom:60%" />

然后就会在首页展示了。

7.已经上传过的文件怎么在.gitignore中设置为忽略又不删除本地文件

```
1.git rm -r --cached 要忽略的文件
2.git add .
3.git commit -m " commet for commit ....."
4.git push
```

