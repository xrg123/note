### 1、webserver是什么，什么情况下才会用到

web server是web服务器，可以解析http协议，当web服务器收到一个http请求后，会返回一个http响应。可以说web server是专门用来处理http请求的。常用的web服务器有nginx\apache. tomcat不属于web服务器，而是属于java应用服务器。web服务器是用来处理静态页面的，tomcat可以处理动态页面，如servlet、jsp。

### 2、default关键字

jdk1.8之前，接口中不允许存在方法的实现，但是如果接口中新添加的方法之后，原来实现接口的代码就会出错，为了解决这个问题，jdk1.8中提出了default关键字，打破之前对接口的限制，允许接口中实现方法体。（解决接口的修改与现有实现不兼容的问题）

```java
//iteratable接口中的方法
default Spliterator<T> spliterator() {
        return Spliterators.spliteratorUnknownSize(iterator(), 0);
    }
```

若一个类同时继承两个接口，这两个接口中含有同样的默认方法，这时候会报错，原因是编译器不知道该执行哪个方法，解决方式为实现该方法。

接口中有static关键字修饰的方法时，也需要实现其方法体。

### 3、为什么继承优先于接口实现呢

编译器规则

### 4、[集合类中modCount、expectedmodCount字段的作用](https://www.cnblogs.com/nevermorewang/p/7808197.html)

ArrayList、LinkedList、HashMap中都有一个字段叫modCount和expectedmodCount

```java
protected transient int modCount = 0;
 int expectedModCount = modCount;
```

modCount表示list结构上被修改的次数。结构上的修改指的是那些改变了list的长度大小或者使得遍历过程中产生不正确的结果的其它方式。该字段被Iterator以及ListIterator的实现类所使用，如果该值被意外更改，Iterator或者ListIterator 将抛出ConcurrentModificationException异常，这是jdk在面对迭代遍历的时候为了避免不确定性而采取的快速失败原则。子类对此字段的使用是可选的，如果子类希望支持快速失败，只需要覆盖该字段相关的所有方法即可。单线程调用不能添加删除terator正在遍历的对象，否则将可能抛ConcurrentModificationException异常，如果子类不希望支持快速失败，该字段可以直接忽略。

```java
 while (iterator.hasNext()) {
            int a = iterator.next();
            list.remove(5);
        }
```

抛出异常

	Exception in thread "main" java.util.ConcurrentModificationException
	at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:901)
	at java.util.ArrayList$Itr.next(ArrayList.java:851)
	at test5.Test3.main(Test3.java:15)
iterator.remove(）为了防止ConcurrentModificationException异常，手动修复了修改计数的期望值

### 4、fail-fast 和 fail-safe

1.什么是同步修改？

当一个或多个线程正在遍历一个集合Collection，此时另一个线程修改了这个集合的内容（添加，删除或者修改）。这就是并发修改

2.什么是 fail-fast 机制?

fail-fast机制在遍历一个集合时，当集合结构被修改，会抛出Concurrent Modification Exception。

fail-fast会在以下两种情况下抛出ConcurrentModificationException

（1）单线程环境

集合被创建后，在遍历它的过程中修改了结构。

注意 remove()方法会让expectModcount和modcount 相等，所以是不会抛出这个异常。

（2）多线程环境

当一个线程在遍历这个集合，而另一个线程对这个集合的结构进行了修改。

注意，迭代器的快速失败行为无法得到保证，因为一般来说，不可能对是否出现不同步并发修改做出任何硬性保证。快速失败迭代器会尽最大努力抛出 ConcurrentModificationException。因此，为提高这类迭代器的正确性而编写一个依赖于此异常的程序是错误的做法：迭代器的快速失败行为应该仅用于检测 bug。

3. fail-fast机制是如何检测的？

迭代器在遍历过程中是直接访问内部数据的，因此内部的数据在遍历的过程中无法被修改。为了保证不被修改，迭代器内部维护了一个标记 “mode” ，当集合结构改变（添加删除或者修改），标记"mode"会被修改，而迭代器每次的hasNext()和next()方法都会检查该"mode"是否被改变，当检测到被修改时，抛出Concurrent Modification Exception

4. fail-safe机制

fail-safe任何对集合结构的修改都会在一个复制的集合上进行修改，因此不会抛出ConcurrentModificationException

fail-safe机制有两个问题

（1）需要复制集合，产生大量的无效对象，开销大

（2）无法保证读取的数据是目前原始数据结构中的数据。

|                                        | Fail Fast Iterator               | Fail Safe Iterator                     |
| -------------------------------------- | -------------------------------- | -------------------------------------- |
| Throw ConcurrentModification Exception | Yes                              | No                                     |
| Clone object                           | No                               | Yes                                    |
| Memory Overhead                        | No                               | Yes                                    |
| Examples                               | HashMap,Vector,ArrayList,HashSet | CopyOnWriteArrayList,ConcurrentHashMap |

一：快速失败（fail—fast）

​          在用迭代器遍历一个集合对象时，如果遍历过程中对集合对象的内容进行了修改（增加、删除、修改），则会抛出Concurrent Modification Exception。

​          原理：迭代器在遍历时直接访问集合中的内容，并且在遍历过程中使用一个 modCount 变量。集合在被遍历期间如果内容发生变化，就会改变modCount的值。每当迭代器使用hashNext()/next()遍历下一个元素之前，都会检测modCount变量是否为expectedmodCount值，是的话就返回遍历；否则抛出异常，终止遍历。

​      注意：这里异常的抛出条件是检测到 modCount！=expectedmodCount 这个条件。如果集合发生变化时修改modCount值刚好又设置为了expectedmodCount值，则异常不会抛出。因此，不能依赖于这个异常是否抛出而进行并发操作的编程，这个异常只建议用于检测并发修改的bug。

​      场景：java.util包下的集合类都是快速失败的，不能在多线程下发生并发修改（迭代过程中被修改）。

二：安全失败（fail—safe）

​      采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。

​      原理：由于迭代时是对原集合的拷贝进行遍历，所以在遍历过程中对原集合所作的修改并不能被迭代器检测到，所以不会触发Concurrent Modification Exception。

​      缺点：基于拷贝内容的优点是避免了Concurrent Modification Exception，但同样地，迭代器并不能访问到修改后的内容，即：迭代器遍历的是开始遍历那一刻拿到的集合拷贝，在遍历期间原集合发生的修改迭代器是不知道的。

​          场景：java.util.concurrent包下的容器都是安全失败，可以在多线程下并发使用，并发修改。

### 5、HashMap、HashTable、ConcurrentHashMap区别

HashTable:

- 底层数组+链表实现，无论key还是value都**不能为null**，线程**安全**，实现线程安全的方式是在修改数据时锁住整个HashTable，效率低，ConcurrentHashMap做了相关优化
- 初始size为**11**，扩容：newsize = olesize*2+1
- 计算index的方法：index = (hash & 0x7FFFFFFF) % tab.length
- 默认加载因子：0.75

HashMap:

- 底层数组+链表实现，可**以存储null键和null值**，线程**不安全**
- 初始size为**16**，扩容：newsize = oldsize*2，size一定为2的n次幂
- 扩容针对整个Map，每次扩容时，原来数组中的元素依次重新计算存放位置，并重新插入
- 插入元素后才判断该不该扩容，有可能无效扩容（插入后如果扩容，如果没有再次插入，就会产生无效扩容）
- 当Map中元素总数超过Entry数组的75%，触发扩容操作，为了减少链表长度，元素分配更均匀
- 计算index方法：index = hash & (tab.length – 1)

ConcurrentHashMap:

- 底层采用分段的数组+链表实现，线程**安全**

- 通过把整个Map分为N个Segment，可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。(读操作不加锁，由于HashEntry的value变量是 volatile的，也能保证读取到最新的值。

- Hashtable的synchronized是针对整张Hash表的，即每次锁住整张表让线程独占，ConcurrentHashMap允许多个修改操作并发进行，其关键在于使用了锁分离技术

- 有些方法需要跨段，比如size()和containsValue()，它们可能需要锁定整个表而而不仅仅是某个段，这需要按顺序锁定所有段，操作完毕后，又按顺序释放所有段的锁

- 扩容：段内扩容（段内元素超过该段对应Entry数组长度的75%触发扩容，不会对整个Map进行扩容），插入前检测需不需要扩容，有效避免无效扩容

- 在存储结构中ConcurrentHashMap比HashMap多出了一个类Segment，而Segment是一个可重入锁。

  ConcurrentHashMap是使用了锁分段技术来保证线程安全的。

  **锁分段技术**：首先将数据分成一段一段的存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据的时候，其他段的数据也能被其他线程访问。 

  ConcurrentHashMap提供了与Hashtable和SynchronizedMap不同的锁机制。Hashtable中采用的锁机制是一次锁住整个hash表，从而在同一时刻只能由一个线程对其进行操作；而ConcurrentHashMap中则是一次锁住一个桶。

  ConcurrentHashMap默认将hash表分为16个桶，诸如get、put、remove等常用操作只锁住当前需要用到的桶。这样，原来只能一个线程进入，现在却能同时有16个写线程执行，并发性能的提升是显而易见的。

  ====================================================================================

  提炼总结：

  hashMap和hashTable区别：

  1、继承的父类不同：hashMap继承的是AbstractMap类，hashTable继承的是Dictionary类。二者都实现了Map接口

  2、对null对象的支持不同。hashMap中key和value都可以为null,hashTable中都不能为null

  3、容量大小及扩容方式不同。hashMap初始容量为16，扩容时变为原来的两倍，hashTable初始容量为11，扩容为原来容量2倍加1。hashMap计算桶的位置时，采用hash值与数字长度减1的值取余运算，hashTable是通过index = (hash & 0x7FFFFFFF) % tab.length。&0x7FFFFFFF（2的31次方，与运算取绝对值）是为了将负的哈希值转化为正数，而&0x7FFFFFFF后，只有符号位改变，而后面的位都不变。

  4、线程安全不同。hashMap适用于单线程，hashTable适用与多线程。HashTable中的public方法都用synchronized关键字修饰。在单线程的情况下，hashTable要比HashMap慢。其线程安全是通过在修改数据时，锁住整个表来实现，当数据量增大到一定程度时，性能会急剧下降，可使用concurrentHashMap

  5、hashMap可以方便的转化为LinkedHashMap,可以通过插入顺序进行遍历

  6、HashMap的迭代器（Iterator）是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常

  ConcurrentHashMap:

  1、继承关系：继承AbstractMap,实现了ConcurrentMap接口

  2、Node中的value和next指针的值为volatile修饰

  ```java
  final int hash;
  final K key;
  volatile V val;
  volatile Node<K,V> next;
  ```

  3、扩容：concurrentHashMap扩容时不会进行全局扩容，而是对某一个segment进行扩容，当segment容量达到其加载因子时，进行扩容。