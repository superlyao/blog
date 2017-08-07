---
layout: post
title:  "java collection容器"
date:   2017-8-7
categories: Java
tag: collection容器
---


* content
{:toc}


## ArrayList (jdk1.8)

- 继承实现树

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```
> 在初始化发现一点与jdk1.7不同的地方是：1.7是在创建对象的时候就初始化了大小(大小为10),但是在1.8是在add方法执行的时候
在初始化了大小，实例化的时候只是一个空数组。优点可能是为了节约内存。