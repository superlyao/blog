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
        //transient声明的字段不会被序列化
        transient Object[] elementData;
        private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};
        private static final Object[] EMPTY_ELEMENTDATA = {};
        //list的元素总数
        private int size;
        //初始化增量，当为无参构造出来list的时候，每次
        private static final int DEFAULT_CAPACITY = 10;

        //无参构造方法
        public ArrayList() {
            this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
        }

        //初始化大小的构造方法
        public ArrayList(int initialCapacity) {
            if (initialCapacity > 0) {
                this.elementData = new Object[initialCapacity];
            } else if (initialCapacity == 0) {
                this.elementData = EMPTY_ELEMENTDATA;
            } else {
                throw new IllegalArgumentException("Illegal Capacity: "+
                                               initialCapacity);
        }
    }
```
> 在初始化发现一点与jdk1.7不同的地方是：1.7是在创建对象的时候就初始化了大小(大小为10),但是在1.8是在add方法执行的时候
在初始化了大小，实例化的时候只是一个空数组。优点可能是为了节约内存。

### get方法

```java
    public E get(int index) {
        rangeCheck(index);  

        return elementData(index);
    }
        //判断index是不是超过长度，是就抛出异常
    private void rangeCheck(int index) {
        if (index >= size)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }

    @SuppressWarnings("unchecked")
    E elementData(int index) {
        return (E) elementData[index];
    }
```

### set 方法

```java
    //返回原下标的值
    public E set(int index, E element) {
        rangeCheck(index);

        E oldValue = elementData(index);
        elementData[index] = element;
        return oldValue;
    }
```

### add 方法

```java
    public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // 增加更改次数
        elementData[size++] = e;
        return true;
    }

    /**
    * minCapacity 是list元素的个数
    */
    private void ensureCapacityInternal(int minCapacity) {
        //如果数组等于无参构造的数组
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            //Math.max()返回其中较大的一个，第一次就是10
            minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
        }

        ensureExplicitCapacity(minCapacity);
    }

    //是不是需要扩容
    private void ensureExplicitCapacity(int minCapacity) {
        //更改次数加1
        modCount++;

        // 判断list的长度是不是大鱼数组此时的长度，如果大于就扩容，不大就按原容量增加元素
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }

    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        //扩容量,一次扩容多少这个和原数组的length有关
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // 数组复制，并将数组设置新的长度
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```

```java
    //在特定的下标设置元素
    public void add(int index, E element) {
        rangeCheckForAdd(index);
        //检查是不是需要扩容
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        //复制数组，复制目标位置的
        System.arraycopy(elementData, index, elementData, index + 1,
                         size - index);
        elementData[index] = element;
        //元素个数加1
        size++;
    }

    //检查下标是不是合法
    private void rangeCheckForAdd(int index) {
        if (index > size || index < 0)
            throw new IndexOutOfBoundsException(outOfBoundsMsg(index));
    }
```