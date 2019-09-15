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

  ​

  ![](<https://github.com/xrg123/note/blob/master/image/concurrentHashMap.jpg>)

ConcurrentHashMap是由Segment数组结构和HashEntry数组结构组成。Segment实际继承自可重入锁（ReentrantLock），在ConcurrentHashMap里扮演锁的角色；HashEntry则用于存储键值对数据。一个ConcurrentHashMap里包含一个Segment数组，每个Segment里包含一个HashEntry数组，我们称之为table，每个HashEntry是一个链表结构的元素。

**面试常问：**

1. **ConcurrentHashMap****实现原理是怎么样的或者问ConcurrentHashMap****如何在保证高并发下线程安全的同时实现了性能提升？**

答：ConcurrentHashMap允许多个修改操作并发进行，其关键在于使用了**锁分离**技术。它使用了多个锁来控制对hash表的不同部分进行的修改。内部使用段(Segment)来表示这些不同的部分，每个段其实就是一个小的hash table，只要多个修改操作发生在不同的段上，它们就可以并发进行。

- **初始化做了什么事？**

初始化有三个参数

**initialCapacity**：初始容量大小 ，默认16。

**loadFactor,** 扩容因子，默认0.75，当一个Segment存储的元素数量大于initialCapacity* loadFactor时，该Segment会进行一次扩容。

**concurrencyLevel **并发度，默认16。并发度可以理解为程序运行时能够同时更新ConccurentHashMap且不产生锁竞争的最大线程数，实际上就是ConcurrentHashMap中的分段锁个数，即Segment[]的数组长度。如果并发度设置的过小，会带来严重的锁竞争问题；如果并发度设置的过大，原本位于同一个Segment内的访问会扩散到不同的Segment中，CPU cache命中率会下降，从而引起程序性能下降。

源码解惑：

```java
 while (ssize < DEFAULT_CONCURRENCY_LEVEL) {
            ++sshift;
            ssize <<= 1;
        }
```

保证segment数组的大小一定为2的幂，例如用户输入17，实际数组为32

```java
 int segmentShift = 32 - sshift;
 int segmentMask = ssize - 1;
```

保证每个segment中table数组的大小一定为2的幂，初始化时，table默认大小为2



初始化时，实际只填充segment数组的第0个元素

- **size方法**

size的时候进行两次不加锁的统计，两次一致直接返回结果，不一致，重新加锁再次统计

### **1.8中的原理和实现**

- **数据结构**

JDK1.8的实现已经摒弃了Segment的概念，而是直接用Node数组+链表+红黑树的数据结构来实现，并发控制使用Synchronized和CAS来操作，整个看起来就像是优化过且线程安全的HashMap，虽然在JDK1.8中还能看到Segment的数据结构，但是已经简化了属性，只是为了兼容旧版本
![img](https://oscimg.oschina.net/oscnet/4102b1f94ad6ab6adc33293e31ff32543e9.jpg)

put的过程很清晰，对当前的table进行无条件自循环直到put成功，可以分成以下六步流程来概述

1. 如果没有初始化就先调用initTable（）方法来进行初始化过程

2. 如果没有hash冲突就直接CAS插入

3. 如果还在进行扩容操作就先进行扩容

4. 如果存在hash冲突，就加锁来保证线程安全，这里有两种情况，一种是链表形式就直接遍历到尾端插入，一种是红黑树就按照红黑树结构插入，

5. 最后一个如果该链表的数量大于阈值8，就要先转换成黑红树的结构，break再一次进入循环

6. 如果添加成功就调用addCount（）方法统计size，并且检查是否需要扩容

   ### 总结

   1. JDK1.8取消了segment数组，直接用table保存数据，锁的粒度更小，减少并发冲突的概率。
   2. JDK1.8存储数据时采用了链表+红黑树的形式，纯链表的形式时间复杂度为O(n)，红黑树则为O（logn），性能提升很大。什么时候链表转红黑树？当key值相等的元素形成的链表中元素个数超过8个的时候。
   3. JDK1.8的实现降低锁的粒度，JDK1.7版本锁的粒度是基于Segment的，包含多个HashEntry，而JDK1.8锁的粒度就是HashEntry（首节点）
   4. JDK1.8版本的数据结构变得更加简单，使得操作也更加清晰流畅，因为已经使用synchronized来进行同步，所以不需要分段锁的概念，也就不需要Segment这种数据结构了，由于粒度的降低，实现的复杂度也增加了
   5. JDK1.8使用红黑树来优化链表，基于长度很长的链表的遍历是一个很漫长的过程，而红黑树的遍历效率是很快的，代替一定阈值的链表，这样形成一个最佳拍档
   6. JDK1.8为什么使用内置锁synchronized来代替重入锁ReentrantLock，我觉得有以下几点
      1. 因为粒度降低了，在相对而言的低粒度加锁方式，synchronized并不比ReentrantLock差，在粗粒度加锁中ReentrantLock可能通过Condition来控制各个低粒度的边界，更加的灵活，而在低粒度中，Condition的优势就没有了
      2. JVM的开发团队从来都没有放弃synchronized，而且基于JVM的synchronized优化空间更大，使用内嵌的关键字比使用API更加自然
      3. 在大量的数据操作下，对于JVM的内存压力，基于API的ReentrantLock会开销更多的内存，虽然不是瓶颈，但是也是一个选择依据


### 6、javaee是什么

javaME是用来开发嵌入式的，javaSE是用来开发桌面应用的，javaEE是用来开发企业端的。

jdk不分javaME、javaSE、javaEE的

javaEE可以理解为java企业级应用开发的规范，hibernate、spring是两种javaEE组件，Servlet、JSP等都是javaEE规范

 Java SE是Java的标准版，主要用于桌面应用开发，同时也是Java的基础，它包含Java语言基础、JDBC（Java数据库连接性）操作、I/O（输出输出）操作、网络通信、多线程等技术。

### 7、hashMap在多线程情况下会发生什么

1）产生死循环，使cpu使用率飙升

多线程进行put操作后，如果发生扩容的话，可能线程一的A节点指向B节点，线程二B节点指向A节点，这样就产生循环链表，当执行get操作时，就会发生死循环。

2）丢失元素

扩容操作时，线程一A元素执行B元素，线程二C元素指向B元素，那么就会有一个节点断开

3）map.size()与实际数量不符

丢失元素后，size()会与实际不符

### 8、线程池参数

corePoolSize:核心线程数

maxPoolSize:最大线程数

keepAliveTime：空闲线程存活时间

allowCoreThreadTimeOut: 是否允许核心线程空闲退出，默认值为false。

workQueue: 任务队列容量

RejectedExecutionHandler: 任务拒绝策略，有四种，第一种丢弃任务并抛出异常，第二种丢弃任务，第三种执行任务并丢弃任务队列第一个任务，第四种由调用线程执行当前任务。

TimeUnit:   计量时间单位

### 9、Java.util.concurrent包下面用过哪些类

1）线程池

接口：Eexcutor、ExecutorService

类：AbstractExecutorService、Executors、ThreadPoolExecutor

2）阻塞队列

非阻塞队列：ArrayDeque、LinkedList、PriorityQueue  这三个队列在java.util包中

​			ConcurrentLinkedQueue   这个队列在java.util.Concurrent包下

阻塞队列： 

​       接口：BolckingQueue、BlockingDeque

​       类：ArrayBlockingQueue、LinkedBlockingQueue、LinkedBolcingDeque、PriorityBlockingQueue、DelayQueue、SynchronousQueue

3）ConcurrentHashMap

4)线程类

接口：Callable、Future

类：FutureTask

### 10、AQS

AQS（Abustact Queued Synchronizer 抽象队列化同步器）是用来为Java的并发同步组件提供统一的底层支持，例如 `ReentrantLock, CountdowLatch` 都是基于 AQS 实现的。

AQS有2个重要组成部分：

1. state 同步状态，int 类型，volatile关键字修饰

由三种方法：getState()、setState()、compareAndSetState()这三种操作均是原子操作

1. 一个同步队列

当一个线程尝试获取锁时，如果已经被占用，此线程就作为一个节点添加到队尾，对头是成功获取锁的节点，对头释放锁后，会唤醒后面的节点，并出队。

资源共享方式：

AQS定义了2种共享方式：

1. 独占 Exclusive（独占，只有一个线程能执行，如ReentrantLock）
2. 共享 Share（共享，多个线程可同时执行，如Semaphore/CountDownLatch）

获取锁和释放锁的流程：

- 获取锁

调用获取方法，如果成功则返回，否则构造node节点加入到队尾，以自旋的方式判断是否可以成为头节点，如果不能，就进入等待状态。

- 释放锁

调用释放方法，获取当前节点的下一个节点，唤醒后面的节点。

在细节上2中方式有一些差异：

1. 独占锁中 state 为1，代表一次只能一个线程执行，而在共享锁中 state > 1，同时可以有多个线程成功获取同步状态。
2. 释放锁时，独占锁只唤醒后面的那一个节点，因为 state 为 1，叫醒一个就够了，而共享锁会唤醒后面所有节点，因为 state > 1，把后面的都唤醒，至于哪些线程能获取同步状态就看他们自己的了。


### 11、forEach实现原理

forEach对Collection是通过Iterator实现的，对数组是通过下标遍历实现的。

java编译器隐藏了基于iteration和下标遍历的内部实现



