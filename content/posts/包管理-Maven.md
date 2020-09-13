---
title: "Java的包管理与Maven"
date: 2020-05-11T17:30:59+08:00
draft: false
---


## Java程序如何执行？
在Jvm中，它只做很简单的一件事，找到这个类并执行它，如果类中引用了其他的类，则继续找到引用的这个类，继续执行。

## Jvm如何找到类？
在Jvm中，所有的类使用全限定类名，Jvm也是根据全限定类名找到这个类；
查询机制：与熟悉的Path环境变量相同，Jvm从classpath按照Path的顺序依次查找。

## 当我们引入第三方包时，需要怎么做？
首先你需要有源文件（jar文件)，然后告诉Jvm去哪里可以找到它，也就是指定classpath。

## Maven做了什么？
在管理依赖的方面，Maven就是从它的仓库中通过你定义的**坐标**
```
 	<groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
```
找到并下载该jar。

## 包冲突
根据Jvm执行的机制可以知道，包冲突就是在classpath中存在全限定类名相同的类，我们想要使用的jar包的path排在了不想要的后面，导致了错误的引用。
解决方法也是围绕着能够让Jvm能够正确读取我们想要的类为前提来进行。




