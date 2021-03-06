---
title: "Exception 体系概要"
date: 2020-05-28T13:55:18+08:00
draft: false
tags: ["exception","java"]
---

# 概要

程序并不是每次都能按照理想情况运行，总是有着不可预测的异常情况发生。

## 作用
* 正确处理异常可以使程序更健壮；
* 异常给方法提供了除了return之外的额外的返回途径；

## Java中的异常结构
Java中的异常大致分为两类：`Exception`和`Error`，他们都继承自`Throwable`，意思是可抛出的异常;

Exception:(checked) 往往可以通过正确处理来避免；例如NullPointorException
 	* runtimeException：运行时异常（unchecked）
Error：（unchecked） 程序无能为力的异常；例如NoSuchClassError、OutOfmemoryError


# 异常的处理

有两种方式来处理异常
* 抛出
* 捕获

当你的的程序在某些情况不能正确执行：你可以抛出一个异常来警告调用者，或者捕获异常并处理。
当你的程序调用一个抛出异常的接口时：
	* 继续抛出这个异常
	* 捕获并处理它（切记不可捕获了异常时不做任何处理）
	* 捕获它，doSomething并继续抛出此异常或另一个异常

## 异常处理原则

* 能用if/else或者其他能处理的，不要用异常
* 尽早抛出异常
* 带出重要信息
* 一旦捕获异常除非特别的，必须进行处理或者重新抛出。
····

# 其他

### 不捕获，一直抛出会发生什么？
异常会击穿方法，直到被捕获，如果一直到最外层都没有捕获，则会杀掉当前线程。

### catch/finally里的return
finally一定会被执行，所以最终return的是finally块里的，另：不要再catch里return，这是不好的做法。

### 日志里的caused by是什么？
出现caused by是异常被捕获后，重新由新的异常包裹（throw new XXXException("some things", e)）并抛出。