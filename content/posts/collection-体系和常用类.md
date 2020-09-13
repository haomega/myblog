---
title: "Collection 体系和常用类"
date: 2020-05-12T17:55:28+08:00
draft: false
---

# Collection体系
Collection：是一组数据的集合
* Set 集 （不包含重复、无序）
* List 列表 （包含重复、有序)
* Quene 队列 （先进后出）

![Colection体系](/collections.jpg)

## Collection接口
定义了基本的集合方法
* add/addAll	添加一个到集合中
* remove/removeAll/removeIf	从集合中移除元素
* contains/containsAll	判断集合是否包含
* size	集合大小
* clear	清空集合
* retainAll	交集

## Set
完全是Collection的实现，没有新增什么方法。

## List
增加了基于Index操作的相关方法：
* get(i)/set(i)/remove 根据下标获取/设置/删除
* indexOf/lastIndexOf 

## Quene
增加了队列的相关操作：
* poll/remove 	删除头部的一个元素
* peek 偷看


## 常用类

从Collection体系图中可以看出：
* Set：HashSet
* List：ArrayList
* Quene：

### HashSet
内部维护了一个HashMap，基本上都是在间接操作里面的HashMap

### ArrayList
日常用到的最多，如果没有特殊的需求，一般都会用它。
特点是内部维护了数组，查找快、增删慢（如果删除中间的元素，后面的元素还要依次进一）
**内部数据结构：** Object数组


# Map体系
键值对映射，不属于Collection
![Map体系](/Map.png)

## Map接口
定义了键值对操作的方法，内部还包含了Entry接口
* put/putAll 新增键值对
* remove 	删除
* get	根据key获取value
* containsKey/containsValue 	判断包含
* clear	清空
* keySet/values/entrySet	返回Map的key视图/value视图/entry视图
* replace 替换

__注意: Map视图是map内的真实映射，对视图操作就是对map操作__


## Map常用类

* HashMap
* TreeMap
* LinkedHashMap 继承自HashMap

### HashMap
因为元素的存放是根据key的hash来的，所以当查找一个key时非常快，直接计算key的hash，找到存放位置。
**内部数据结构** 数组加链表`Node<K,V>[] table`

### TreeMap
TreeMap 实现了SortedMap接口，增加了firtKey/lastKey/headMap/tailMap等方法。
在实例化TreeMap时，可传入一个比较器Comparator


