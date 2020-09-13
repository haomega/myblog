---
title: "Collection:ArrayList源码/扩容机制"
date: 2020-06-17T14:53:38+08:00
draft: false
---

## ArrayList继承体系

```public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

你会发现既然ArrayList继承了AbstractList（它`implement List`接口），为啥后面还加了个`implement List<E>`，网上给出的解释是：

> `implement List<E>` 是可以省略的，只是为了直观显示ArrayList实现了List接口，因为AbstractList只是为了减少实现List接口的代码。

RandomAccess、Cloneable、Serializable，可随机读写、可克隆、可序列化。

## Field

`private static final int DEFAULT_CAPACITY = 10`默认容量10

`private static final Object[] EMPTY_ELEMENTDATA = {}` 共享的空数组

` private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {}` 共享的空数组

`transient Object[] elementData` ArrayList元素存放的数据结构-数组

你会注意到EMPTY_ELEMENTDATA和DEFAULTCAPACITY_EMPTY_ELEMENTDATA只是两个名字不通的空数组，为啥会需要两个呢？

观察构造器`public ArrayList(int initialCapacity)`指定容量为0的话，ArrayList会使用EMPTY_ELEMENTDATA，

而无参构造器则会使用DEFAULTCAPACITY_EMPTY_ELEMENTDATA

这两个有什么不通呢？答案是容量增长方式不一样
```
private static int calculateCapacity(Object[] elementData, int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        }
        return minCapacity;
}
```
可以看到第二个默认容量是10，而第一个是0，表现为：

EMPTY_ELEMENTDATA：0-1-2-3-4-6-9······
DEFAULTCAPACITY_EMPTY_ELEMENTDATA：0-10-15-22-33······

## 方法与实现

除了AbstractList帮忙实现的外，ArrayList实现了List的其他接口。

## 扩容机制

```
private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```

新生成一个原来**1.5**倍容量的数组，然后将old数组拷贝到新数组。


