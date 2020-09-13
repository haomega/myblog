---
title: "collection 常用类的数据结构"
date: 2020-06-17T14:54:52+08:00
draft: false
---

## Collection体系常用类

### Set接口常用类
* HashSet
* LinkedHashSet
* TreeSet

### List接口常用类
* ArrayList
* LinkedList
* Stack
* Vector（提供了一些线程安全的方法）

### Map接口常用类
* HashMap
* HashTable
* LinkedHashMap
* TreeMap

## Set常用类数据结构

HashSet 内部维护了一个HashMap`private transient HashMap<E,Object> map;`，所有方法都是靠HashMap来完成。

LinkedHashMap 继承了HashSet，唯一与之不同的是内部维护的是LinkedHashMap而不是HashMap：
``` 
/**
     * Constructs a new, empty linked hash set.  (This package private
     * constructor is only used by LinkedHashSet.)...
**/
HashSet(int initialCapacity, float loadFactor, boolean dummy) {
        map = new LinkedHashMap<>(initialCapacity, loadFactor);
    }
```

TreeSet内部也是维护了一个NavigableMap（TreeMap）。
详情请看Map。

## List常用类数据结构

ArrayList内部维护了一个Object数组`transient Object[] elementData`;

LinkedList是链表结构，内部构造了含有前后指针的Node;

Stack extend Vector，所以内部也是一个Object数组，通过数组实现栈（先进后出），每次出栈最后一个数组元素。

## Map常用类数据结构

HashMap/HashTable
> HashMap 大致相当于HashTable，除了HashMap不是线程安全的，并且允许null作为Key或Value;

HashMap的数据结构是Hash桶（数组加链表）`transient Node<K,V>[] table`;

put逻辑：计算key的hash，根据hash通过取模（%）`(n - 1) & hash`计算桶位置，判空，非空的话遍历链表，如果key相等会替换原来的值，没有相同的就加到链表后。

LinkedHashMap extend HashMap，与之不通的是，它维护了一个双向链表（重新实现了桶，使之包含前后两个指向）
```
/**
     * HashMap.Node subclass for normal LinkedHashMap entries.
     */
    static class Entry<K,V> extends HashMap.Node<K,V> {
        Entry<K,V> before, after;
        Entry(int hash, K key, V value, Node<K,V> next) {
            super(hash, key, value, next);
        }
    }
```

TreeMap是红黑树的实现，具体可看[这里](https://juejin.im/post/5be529a5f265da615704fd45)
‭

## 总结:
Set的实现基本靠内部维护的HashMap类；

List有数组和链表实现，数组可以根据下标快速获取元素，删除慢；链表删除快，随机读写会比较慢，因为每次获取元素都要从第一个元素开始找。

HashMap的实现比较复杂，数据结构是数组加链表，虽然有链表实现，但是数据结构也是相同的，只不过桶的数据结构变成了具有双向链表的结构，也由于根据计算hash来确定元素存放位置，使得查找非常快。