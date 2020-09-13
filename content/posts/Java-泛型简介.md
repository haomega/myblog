---
title: "Java 泛型简介"
date: 2020-07-03T13:46:53+08:00
draft: false
---

## Java泛型历史
Java是从Jdk1.7之后引入泛型的，现在我们已经习惯声明一个类型绑定的Collection类`new ArrayList<String>();`

Collection体系是从JDK1.2引入的`@since 1.2`

也就是说在JDK1.2之后JDK1.7之前，只能使用原始类型的Collection`new ArrayList()`,原始类型接受任何类型的元素也就是Object。


## 为什么要引入泛型

* 为了类型安全

我们使用数组的时候：`new String[1]`，非String类型是不能放入String数组的，在编译阶段就会报错。

然而，原始类型的Collection能存放任何元素，如果要实现类型安全，只能新建类，比如：CollectionString；
这样会导致每有一个类型你就要一次实现，比较啰嗦。

* 省去不必要的类型转换操作

原始类型在进行元素读取操作时，因为存的都是Object元素，每次读取都需要进行类型转换，增加了不必要的操作。


## Java如何实现泛型的
Java的泛型只是在编译阶段的泛型，泛型类经过编译后的class都是经过**类型擦除**的原始类型。

也就是说，我们在声明一个泛型类时，如果往其中放入一个其他类型元素，Java编译器会报错，泛型类在编译通过后，
虽然会被擦除为原始类型，但因为经过了编译器检查，我们默认里面存的元素全部都是统一的泛型。

类似的面向对象语言C++，采用的时另一种实现方式：独立出原始类型，新创建一套泛型的类，与Java相比，C++的做法更简单，
但是不方便维护；Java则是需要在编译阶段做更多的操作。


## 泛型的限定符

? extends `boolean addAll(Collection<? extends E> c)` 限定是E或者是E的子类，一个E类型的Collection，当然E的子类也能被添加。
? super `default void sort(Comparator<? super E> c)` 限定E或者E的父类实现了的Comparator，E的父类实现了Comparator接口，当然E也实现了该接口。

`public static <T extends Comparable<? super T>> void sort(List<T> list)` 
对List<T>进行排序，T元素限定为 `<T extends Comparable<? super T>>`
需要排序的T是实现了Comparable接口的任意类型, 而任意类型是类型T或者类型T的父类.，


## 问题
1. 有了泛型还需要原始类型吗？
需要，Java在编译时会进行类型擦除，泛型类最后都会变成原始类型。

2. 泛型类是一个新的类吗？
是也不是，是是因为泛型类都是从同一个Class文件创建的，不是是因为泛型类并不能由一个子类接受一个父类引用。




