---
layout: post
title:  "java collection容器 LinkedList"
date:   2017-8-7
categories: Java
tag: collection容器
---


* content
{:toc}


## LinkedList

> 底层使用双向链表实现

- 继承实现树

```java

public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
```

```java
    //内部类
    private static class Node<E> {
        E item; //当前元素
        Node<E> next; //下一个节点
        Node<E> prev; //上一个节点

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```