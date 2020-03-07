---
title: Jar包注册为windows服务
date: 2019-09-29 23:47:44 
categories: "日常积累" 
tags: 日常积累
description: Jar包注册为windows服务


---



1. 从github上下载WinSW.NET4.exe，下载地址https://github.com/kohsuke/winsw/releases，然后把名字改成你想要的名字，比如demo.exe。

2. 没有安装.net的需要先安装。

3. 创建xml配置文件

   ```xml
    <service> 
        <id>demo</id> 
        <name>demo</name>
        <description>这是服务介绍</description>
        <!-- java环境变量 -->
        <!--可以选择jdk -->
   	<env name="JAVA_HOME" value="%JAVA_HOME%"/>-->
   	 <!--<env name="JAVA_HOME" value="D:\Tools\Java\jdk1.8_32"/>-->
        <executable>java</executable> 
       <arguments>-jar "F:\demo\demo.jar"</arguments>
        <!-- 开机启动 -->
        <startmode>Automatic</startmode>
        <!-- 日志配置 产生位置-->
        <logpath>%BASE%\log</logpath>
        <logmode>rotate</logmode>
    </service>
   
   ```

   

4. 将xml和exe文件与jar包放到同一目录下。

5. 打开cmd，cd到jar包目录下 执行 demo.exe install安装服务，就可以在windows的服务里看到了

   ![服务](C:\Users\yangrui-lc\Desktop\博客园\服务.png)



