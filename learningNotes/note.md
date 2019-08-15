### 1、内核态和用户态

内核态和用户态是操作系统的两种运行级别

内核态是操作系统内核运行的模式，运行在内核态的代码可以无限制地对系统存储、外部设备进行访问

用户态只能访问受限内存，且不允许访问外围设备，所有的用户程序都运行在用户态

内核态和用户态的切换有三种方式：系统调用，异常，外围设备的中断

### 2、5种IO模型及IO多路复用

#### IO过程分两个阶段：

数据准备阶段。从设备读取数据到内核空间的缓冲区

内核空间赋值会用户空间进程缓冲区阶段。

*阻塞IO  进程等待，直到读写完成

![](<https://github.com/xrg123/note/blob/master/image/IO1.png>)

*非阻塞IO 进程调用recvfrom操作，如果IO没有注备好，立即返回ERROR，进程不阻塞。用户可以轮询，如果内核已经准备好了，就阻塞，然后复制数据到用户空间。

![](<https://github.com/xrg123/note/blob/master/image/IO2.png>)

*IO多路复用   一个线程，通过记录IO流的状态来同时管理多个IO，可以提高服务器的吞吐能力

进程调用select,进程被阻塞   内核监视所有select负责的socket,当socket的数据准备好后，就立即返回

进程再调用read操作，数据就会从内核拷贝到进程。

​	select

​	![](<https://github.com/xrg123/note/blob/master/image/IO3.png>)

​	将关注的IO操作告诉select函数并调用，进程阻塞，内核“监视”select关注的文件描述符fd，被关注的任何一个fd对应的IO准备好了数据，select返回。再使用read将数据复制到用户进程。

- 一般情况下，select最多能监听1024个fd(文件描述符，监听数量可以修改，但不建议修改)，但是由于select采用轮询的方式，当管理的IO多了，每次都要遍历全部fd,效率低下。

​	将一个存放文件描述符的信息结构体从用户空间拷贝到内核空间，注册回调函数，调用pull方法，pull将返回一个描述读写是否就绪的mask掩码，根据掩码给信息结构体赋值。若遍历完所有fd都没有返回一个可读写的mask掩码，就会让select的进程进入休眠状态，直到发现可读写的资源后，重新唤醒等待队列上休眠的进程。如果再规定时间内没有唤醒休眠进程，那么进程会唤醒并重新获得CPU，再去遍历一次fd,将文件描述符的信息结构体从内核空间拷贝到用户空间。

缺点：两次拷贝耗时，轮询所有fd耗时，支持的文件描述符太小

优点：跨平台支持

​	pull

​	函数调用过程与select完全一致

​	优点：连接数（也就是文件描述符）没有限制（链表存储）

​	缺点:大量拷贝

​	epull

​	epoll没有管理的fd的上限，且是回调机制，不需遍历，效率很高。

​	延迟处理：检测到描述符事件通知应用程序，应用程序不立即处理该事件。那么下次会再次通知此事件

​	立即处理：检测到描述符事件通知应用程序，应用程序会立处理

*信号驱动IO

![](<https://github.com/xrg123/note/blob/master/image/IO4.png>)

- 进程在IO访问时，先通过sigaction系统调用，提交一个信号处理函数，立即返回。
- 进程不阻塞。当内核准备好数据后，产生一个SIGIO信号(**电平触发**)并投递给信号处理函数。可以在此函数中调用recvfrom函数操作数据从内核控件复制到用户控件，这段过程进程阻塞。

*异步IO模型

![](<https://github.com/xrg123/note/blob/master/image/IO5.png>)

在进程发起异步IO请求，立即返回。内核完成IO的两个阶段，内核给进程发一个信号

- 举例：来打饭，跟大师傅说饭好了叫你，饭菜准备好了，窗口服务员把饭盛好了打电话叫你。两个阶段都是异步的。整个过程中，进程都可以忙别的，等好了才过来。
- 举例：今天不想出去到饭店吃饭了，点外卖，饭菜在饭店做好了(第一阶段),快递员从饭店送到你家门口(第二阶段)。