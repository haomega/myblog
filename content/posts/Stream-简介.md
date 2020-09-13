---
title: "Stream 简介"
date: 2020-07-07T15:08:32+08:00
draft: false
---

## JDK1.8 Stream is comming!

JDK1.8引入了一个新的功能，Stream流操作，通过将Collection、数组等转换成stream，通过stream进行筛选、转换等操作，简直不要太爽。

Stream流操作，主要用于数据处理方面，以前十几行能实现的功能，使用Stream往往只需要一行，Cool！

## 使用Strema

流的处理包括两个部分:	
	* 一系列的中间操作，比如：过滤、转换等
	* 终结操作，将经过一系列中间操作的流进行收集，比如：计算个数、收集为Set/List、分组等等。

注意：一个流在执行终结操作后就会被关闭，是不能够复用的。

### 生成一个Stream

1. Collection类，使用Collection.stream()方法。
2. 数组：Arrays.steam(int[] arr) 
3. 
 * Stream.of(T ...)通过给定的元素生成，
 * Stream.generate(Supplier T)通过给定的函数接口生成, 
 * Stream.empty()空流，
 * Strema.concat(Stream<? extends T> a, Stream<? extends T> b)合并两个流。

除了常规的对象流之外，还有IntStream、LongStream、DoubleStream

### 中间操作

* 筛选：filter、limit、skip
* 映射：map、flatMap
* 排序：sorted


### 终结操作

* 查找与匹配：anyMatch、allMatch、findFirst、findAny
* 归约：reduce
* **收集** ：collect(Collector)

>collect 是一个非常有用的终端操作，它可以将流中的元素转变成另外一个不同的对象，例如一个List，Set或Map。collect 接受入参为Collector（收集器），它由四个不同的操作组成：供应器（supplier）、累加器（accumulator）、组合器（combiner）和终止器（finisher）。
这些都是个啥？别慌，看上去非常复杂的样子，但好在大多数情况下，您并不需要自己去实现收集器。因为 Java 8通过Collectors类内置了各种常用的收集器，你直接拿来用就行了。



