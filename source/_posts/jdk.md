---
title: JDK8和JDK17 在Windows同时安装配置指南
date: 2023-11-02 11:02:24
tags:
---

[JDK8](https://www.oracle.com/java/technologies/downloads/#java8-windows)
[JDK17](https://www.oracle.com/java/technologies/downloads/#jdk17-windows)

## 环境变量

需要添加 **2** 个系统变量来指定两个JDK的安装目录：

​	变量名：JAVA8_HOME

​	变量值：`JDK8安装所在目录` 例如`D:\java\jdk1.8.0_xxx\`

​	变量名：JAVA17_HOME

​	变量值：`JDK17安装所在目录` 例如`D:\java\jdk17.0.1\`

需要添加 **1** 个系统变量来指定具体要使用哪个JDK版本(这里指定JDK8，如果要指定JDK17改为`%JAVA17_HOME%`即可)：

​	变量名：JAVA_HOME

​	变量值：%JAVA8_HOME%

需要添加 **1** 个系统变量来配置JAVA编译环境：

​	变量名：CLASSPATH

​	变量值：.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;

需要配置 **Path** 环境变量来指定JAVA编译工具的安装目录	

​	变量名：Path

​	变量值：%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

![image](./config.png)

PATH 环境变量:

![](./path.png)

## 切换版本

将`JAVA_HOME`的变量值改为`%JAVA17_HOME%`即可。

