---
title: JDK的安装的那些事
date: 2020-01-21 15:22:39
categories: 
- Java
tags: 
- Java
- JDK
- 环境变量
---
# JDK版本选择
目前JDK已更新至JDK13，登陆[Oracle官网](https://www.oracle.com/technetwork/java/javase/downloads/index.html)可以看到JDK13、JDK11和JDK8三个，其中JDK11和JDK8为长期支持版本。目前官方已停止对JDK9、JDK10的维护，这里推荐使用作为长期支持版的JDK8和JDK11。在Oracle官网上，对于非当前维护的JDK版本，都需要登录后才能进行下载。
<!-- more -->

# 环境变量

## Path

根据[JDK官方安装文档](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html#CHDEBCCJ)，如果未设置`PATH`变量，则每次运行时都需要指定可执行文件的完整路径，如：

```CMD
C:\>"C:\Program Files\Java\jdk1.8.0_241\bin\javac" MyClass.java
```

## JAVA_HOME

`JAVA_HOME`指向JDK安装目录，供其他应用程序搜索，如：Eclipse/NetBeans/Tomcat

在`Path`变量中引用`JAVA_HOME`有利于在安装多个JDK版本时进行切换。

（在`Path`引用`JAVA_HOME`：`%JAVA_HOME%/bin`，可以通过修改`JAVA_HOME`指向的位置来切换JDK版本）

## CLASS_PATH

`CLASS_PATH`是JVM使用的一个环境变量，它指示JVM如何搜索class。

因为Java是编译型语言，源码文件是`.java`，而编译后的`.class`文件才是真正可以被JVM执行的字节码。因此，JVM需要知道，如果要加载一个类，应该去哪搜索对应的`.class`文件。

不推荐在系统环境变量中设置`CLASS_PATH`，应在启动JVM时设置`CLASS_PATH`，即使用`java`命令传入`-classpath`或`-cp`参数。

*不要把任何Java核心库添加到`CLASS_PATH`中！JVM根本不依赖`CLASS_PATH`加载核心库！*

如果没有设置系统环境变量，也没有传入`-cp`参数，那么JVM默认的`classpath`为`.`（`.`表示当前目录，默认的当前目录`.`对于绝大多数情况都够用了）
