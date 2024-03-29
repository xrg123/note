### 1、在项目中缓存是如何使用的，为什么要用缓存，缓存使用不当会造成什么后果？

在项目中哪里用到了缓存，为什么要用，不用行不行，用了可能会有什么不良后果

驿术交易系统中，用户登录后，会将用户信息存储到redis中，第一，每一次访问都要验证用户是否登录，频繁访问数据库的话会使数据库压力很大，查询效率低。第二，系统中很多地方都需要用到用户信息，如交易/交换、转让等。同时，将一些用户频繁访问到的数据存储到redis中，例如，在项目启动初始化时，将团购商品的信息放到redis中，一方面可以提高用户体验，另一方面可以通过预减库存减小数据库压力。       redis可以减小数据库压力，提高系统系统并发行能和用户体验。

-------------------------------------------------------------------------------------------------------------------------------------------------------

### 为什么要用缓存？

用缓存，主要有两个用途：**高性能**、**高并发**。

#### 高性能

假设这么个场景，你有个操作，一个请求过来，吭哧吭哧你各种乱七八糟操作 mysql，半天查出来一个结果，耗时 600ms。但是这个结果可能接下来几个小时都不会变了，或者变了也可以不用立即反馈给用户。那么此时咋办？

缓存啊，折腾 600ms 查出来的结果，扔缓存里，一个 key 对应一个 value，下次再有人查，别走 mysql 折腾 600ms 了，直接从缓存里，通过一个 key 查出来一个 value，2ms 搞定。性能提升 300 倍。

就是说对于一些需要复杂操作耗时查出来的结果，且确定后面不怎么变化，但是有很多读请求，那么直接将查询出来的结果放在缓存中，后面直接读缓存就好。

#### 高并发

mysql 这么重的数据库，压根儿设计不是让你玩儿高并发的，虽然也可以玩儿，但是天然支持不好。mysql 单机支撑到 `2000QPS` 也开始容易报警了。

所以要是你有个系统，高峰期一秒钟过来的请求有 1万，那一个 mysql 单机绝对会死掉。你这个时候就只能上缓存，把很多数据放缓存，别放 mysql。缓存功能简单，说白了就是 `key-value` 式操作，单机支撑的并发量轻松一秒几万十几万，支撑高并发 so easy。单机承载并发量是 mysql 单机的几十倍。

> 缓存是走内存的，内存天然就支撑高并发。

### 2、如何保证缓存与数据库的双写一致性

你只要用缓存，就可能会涉及到缓存与数据库双存储双写，你只要是双写，就一定会有数据一致性的问题，那么你如何解决一致性问题？

如果缓存与数据库要保持严格一致性的话，可以采用：读请求与写请求串行化，，串到一个内存队列里去。

--------------------------------------------------------------------------------------------------------------------------------------------------------

### Cache Aside Pattern

最经典的缓存+数据库读写的模式，就是 Cache Aside Pattern。

- 读的时候，先读缓存，缓存没有的话，就读数据库，然后取出数据后放入缓存，同时返回响应。
- 更新的时候，**先更新数据库，然后再删除缓存**。

**为什么是删除缓存，而不是更新缓存？**

原因很简单，很多时候，在复杂点的缓存场景，缓存不单单是数据库中直接取出来的值。

比如可能更新了某个表的一个字段，然后其对应的缓存，是需要查询另外两个表的数据并进行运算，才能计算出缓存最新的值的。

另外更新缓存的代价有时候是很高的。是不是说，每次修改数据库的时候，都一定要将其对应的缓存更新一份？也许有的场景是这样，但是对于**比较复杂的缓存数据计算的场景**，就不是这样了。如果你频繁修改一个缓存涉及的多个表，缓存也频繁更新。但是问题在于，**这个缓存到底会不会被频繁访问到？**

举个栗子，一个缓存涉及的表的字段，在 1 分钟内就修改了 20 次，或者是 100 次，那么缓存更新 20 次、100 次；但是这个缓存在 1 分钟内只被读取了 1 次，有**大量的冷数据**。实际上，如果你只是删除缓存的话，那么在 1 分钟内，这个缓存不过就重新计算一次而已，开销大幅度降低。**用到缓存才去算缓存。**

其实删除缓存，而不是更新缓存，就是一个 lazy 计算的思想，不要每次都重新做复杂的计算，不管它会不会用到，而是让它到需要被使用的时候再重新计算。

----------------------------------------------------------------------------------------------------------------------------------------------------

先更新数据库，再删除缓存。如果删除缓存失败了，那么会导致数据库中是新数据，缓存中是旧数据，数据就出现了不一致。

解决思路：先删除缓存，再更新数据库。如果数据库更新失败了，那么数据库中是旧数据，缓存中是空的，那么数据不会不一致。因为读的时候缓存没有，所以去读了数据库中的旧数据，然后更新到缓存中。

---------------------------------------------------------------------------------------------------------------------------------------------------------

### 比较复杂的数据不一致问题分析

数据发生了变更，先删除了缓存，然后要去修改数据库，此时还没修改。一个请求过来，去读缓存，发现缓存空了，去查询数据库，**查到了修改前的旧数据**，放到了缓存中。随后数据变更的程序完成了数据库的修改。完了，数据库和缓存中的数据不一样了...

=======================================================================================

首先，如果使用缓存的话，数据一致性问题是不可避免，且无解的，如果对数据一致性要求很高，那就不能使用缓存。

方案一：给缓存设置过期时间。所有的写操作以数据库为准，对缓存操作只是进最大努力交付。

如果数据库更新成功，缓存更新失败，只要达到过期时间，后面的缓存自然会从数据库中读取新值然后回填缓存。

方案二：先删除缓存，再更新数据库。

可能出现缓存与数据库不一致的原因是，线程A删除缓存后，再对数据库进行更新前，线程B进行查询操作，并将查询结果写入到缓存中。当线程A进行完数据库的更新后，缓存与数据库发生不一致。

可采用延时双删策略。删除缓存，更新数据库，休眠一秒后再删除缓存。

```java
public void write(String key,Object data){
    redisUtils.del(key);
    db.update(data);
    Thread.Sleep(100);
    redisUtils.del(key);
}
```

如果你用了mysql的读写分离架构怎么办？ 
ok，在这种情况下，造成数据不一致的原因如下，还是两个请求，一个请求A进行更新操作，另一个请求B进行查询操作。 
（1）请求A进行写操作，删除缓存 
（2）请求A将数据写入数据库了， 
（3）请求B查询缓存发现，缓存没有值 
（4）请求B去从库查询，这时，还没有完成主从同步，因此查询到的是旧值 
（5）请求B将旧值写入缓存 
（6）数据库完成主从同步，从库变为新值 
上述情形，就是数据不一致的原因。还是使用双删延时策略。只是，睡眠时间修改为在主从同步的延时时间基础上，加几百ms。 
采用这种同步淘汰策略，吞吐量降低怎么办？ 
ok，那就将第二次删除作为异步的。自己起一个线程，异步删除。这样，写的请求就不用沉睡一段时间后了，再返回。这么做，加大吞吐量。 
第二次删除,如果删除失败怎么办？ 
这是个非常好的问题，因为第二次删除失败，就会出现如下情形。还是有两个请求，一个请求A进行更新操作，另一个请求B进行查询操作，为了方便，假设是单库： 
（1）请求A进行写操作，删除缓存 
（2）请求B查询发现缓存不存在 
（3）请求B去数据库查询得到旧值 
（4）请求B将旧值写入缓存 
（5）请求A将新值写入数据库 
（6）请求A试图去删除请求B写入对缓存值，结果失败了。 
ok,这也就是说。如果第二次删除缓存失败，会再次出现缓存和数据库不一致的问题。 
如何解决呢？ 

方案三:先更新数据库，再删除缓存

（1）更新数据库数据； 
（2）缓存因为种种问题删除失败 
（3）将需要删除的key发送至消息队列 
（4）自己消费消息，获得需要删除的key 
（5）继续重试删除操作，直到成功 

然而，该方案有一个缺点，对业务线代码造成大量的侵入。于是有了方案二，在方案二中，启动一个订阅程序去订阅数据库的binlog，获得需要操作的数据。在应用程序中，另起一段程序，获得这个订阅程序传来的信息，进行删除缓存操作。 

然而，该方案有一个缺点，对业务线代码造成大量的侵入。于是有了方案二，在方案二中，启动一个订阅程序去订阅数据库的binlog，获得需要操作的数据。在应用程序中，另起一段程序，获得这个订阅程序传来的信息，进行删除缓存操作。 

<https://blog.csdn.net/qq_28740207/article/details/80877079>

### 3、什么是redis的雪崩、穿透和击穿？redis崩溃之后会怎样？系统应该如何应对这种情况？如何处理redis的穿透？

缓存雪崩：是指在某一个时间段，缓存集中过期失效，或缓存机器发生意外全盘宕机。这个时候所有请求全盘落在数据库上，数据库必然也扛不住。

产生雪崩的原因之一，比如在写本文的时候，马上就要到双十二零点，很快就会迎来一波抢购，这波商品时间比较集中的放入了缓存，假设缓存一个小时。那么到了凌晨一点钟的时候，这批商品的缓存就都过期了。而对这批商品的访问查询，都落到了数据库上，对于数据库而言，就会产生周期性的压力波峰。

一般是采取不同分类商品，缓存不同周期。在同一分类中的商品，加上一个随机因子。这样能尽可能分散缓存过期时间，而且，热门类目的商品缓存时间长一些，冷门类目的商品缓存时间短一些，也能节省缓存服务的资源

其实集中过期，倒不是非常致命，比较致命的缓存雪崩，是缓存服务器某个节点宕机或断网。因为自然形成的缓存雪崩，一定是在某个时间段集中创建缓存，那么那个时候数据库能顶住压力，这个时候，数据库也是可以顶住压力的。无非就是对数据库产生周期性的压力而已。而缓存服务节点的宕机，对数据库服务器造成的压力是不可预知的，很有可能瞬间就把数据库压垮。

缓存雪崩的事前事中事后的解决方案如下。

- 事前：redis 高可用，主从+哨兵，redis cluster，避免全盘崩溃。

- 事中：本地 ehcache 缓存 + hystrix 限流&降级，避免 MySQL 被打死。

- 事后：redis 持久化，一旦重启，自动从磁盘上加载数据，快速恢复缓存数据。

- 用户发送一个请求，系统 A 收到请求后，先查本地 ehcache 缓存，如果没查到再查 redis。如果 ehcache 和 redis 都没有，再查数据库，将数据库中的结果，写入 ehcache 和 redis 中。

  限流组件，可以设置每秒的请求，有多少能通过组件，剩余的未通过的请求，怎么办？**走降级**！可以返回一些默认的值，或者友情提示，或者空白的值。

  好处：

  - 数据库绝对不会死，限流组件确保了每秒只有多少个请求能通过。
  - 只要数据库不死，就是说，对用户来说，2/5 的请求都是可以被处理的。
  - 只要有 2/5 的请求可以被处理，就意味着你的系统没死，对用户来说，可能就是点击几次刷不出来页面，但是多点几次，就可以刷出来一次。

----------------------------------------------------------------------------------------------------------------------------------------------------------

缓存穿透：是指查询一个数据库一定不存在的数据。正常的使用缓存流程大致是，数据查询先进行缓存查询，如果key不存在或者key已经过期，再对数据库进行查询，并把查询到的对象，放进缓存。如果数据库查询对象为空，则不放进缓存。对于系统A，假设一秒 5000 个请求，结果其中 4000 个请求是黑客发出的恶意攻击。黑客发出的那 4000 个攻击，缓存中查不到，每次你去数据库里查，也查不到。举个栗子。数据库 id 是从 1 开始的，结果黑客发过来的请求 id 全部都是负数。这样的话，缓存中不会有，请求每次都“视缓存于无物”，直接查询数据库。这种恶意攻击场景的缓存穿透就会直接把数据库给打死。

解决方式很简单，每次系统 A 从数据库中只要没查到，就写一个空值到缓存里去，比如 `set -999 UNKNOWN`。然后设置一个过期时间，这样的话，下次有相同的 key 来访问的时候，在缓存失效之前，都可以直接从缓存中取数据

-----------------------------------------------------------------------------------------------------------------------------------------------------------

缓存击穿，就是说某个 key 非常热点，访问非常频繁，处于集中式高并发访问的情况，当这个 key 在失效的瞬间，大量的请求就击穿了缓存，直接请求数据库，就像是在一道屏障上凿开了一个洞。

解决方式也很简单，可以将热点数据设置为永远不过期

### 4、redis的并发竞争问题是什么，如何解决这个问题？了解 redis 事务的 CAS 方案吗？

这个也是线上非常常见的一个问题，就是**多客户端同时并发写**一个 key，可能本来应该先到的数据后到了，导致数据版本错了；或者是多客户端同时获取一个 key，修改值之后再写回去，只要顺序错了，数据就错了。

而且 redis 自己就有天然解决这个问题的 CAS 类的乐观锁方案。

某个时刻，多个系统实例都去更新某个 key。可以基于 zookeeper 实现分布式锁。每个系统通过 zookeeper 获取分布式锁，确保同一时间，只能有一个系统实例在操作某个 key，别人都不允许读和写。

你要写入缓存的数据，都是从 mysql 里查出来的，都得写入 mysql 中，写入 mysql 中的时候必须保存一个时间戳，从 mysql 查出来的时候，时间戳也查出来。

每次要**写之前，先判断**一下当前这个 value 的时间戳是否比缓存里的 value 的时间戳要新。如果是的话，那么可以写，否则，就不能用旧的数据覆盖新的数据。

### 5、redis和 memcached 有什么区别？redis 的线程模型是什么？为什么 redis 单线程却能支撑高并发？

#### redis 支持复杂的数据结构

redis 相比 memcached 来说，拥有[更多的数据结构](https://github.com/yujianmeng/advanced-java/blob/master/docs/high-concurrency/redis-data-types.md)，能支持更丰富的数据操作。如果需要缓存能够支持更复杂的结构和操作， redis 会是不错的选择。

#### redis 原生支持集群模式

在 redis3.x 版本中，便能支持 cluster 模式，而 memcached 没有原生的集群模式，需要依靠客户端来实现往集群中分片写入数据。

#### 性能对比

由于 redis 只使用**单核**，而 memcached 可以使用**多核**，所以平均每一个核上 redis 在存储小数据时比 memcached 性能更高。而在 100k 以上的数据中，memcached 性能要高于 redis。虽然 redis 最近也在存储大数据的性能上进行优化，但是比起 memcached，还是稍有逊色。

redis支持持久化

### 6、redis常用命令

keys pattern:  keys *  查询所有键       keys  *test    查询所有test结束的键

exists key：   查看key键是否存在（存在返回1， 不存在返回0）

expire key seconds:   给key设置过期时间

persist key:  删除key的过期时间

rename key newkey: 给key重命名

type key: 返回key的类型

set key value:  设定键值对

del key:  删除键

hset  hashname key value:   赋值hash表

hget  hashname key:  获取值

lpush key value: list中插入

lpop key:  移除list中的最后一个元素

sadd key value: set中插入值

spop key: 获取set的值

zadd name num value: zset中设定值

incr key: key的值增加1

decr key：key的值减1

### 7、zset数据结构

zset是一个字符串集合，每一个字符串关联一个double类型的分数，redis正是通过分数来排序的

zSet在redis中有两种实现：压缩双向链表（zipList)、跳表(skipList)

----------------------------------------------------------------------------------------------------------------------------------------------------

zipList是一个固定的数据结构，定义了链表字节长度、节点个数、尾节点偏移字节等内容

redis配置文件中用来控制zset到底是使用ziplist(压缩双向链表)还是skiplist(跳表)的参数:

zset-max-ziplist-entries 128

zset-max-ziplist-value 64

zset-max-ziplist-entries: zset使用ziplist存储的时候，最大限制存储entries的个数
zset-max-ziplist-value: zset使用ziplist存储的时候，每个节点最大存储字节数

违反上述两个限制条件，均会导致zset将ziplist的数据结构切换为skiplist数据结构

而zset使用ziplist的原因，主要是出于在零散数据量少的时候，节省内存的占用

### 8、HashMap

redis的数据结构体是redisDB,存储在server.h文件中。redisDB存储数据库id(redis服务器默认有16个数据库)，键空间，过期键空间等数据。

    typedef struct redisDb {
    dict *dict;                 /* 键空间 */  存储key - value
    dict *expires;              /* 过期键空间 */  存储key的过期时间
    dict *blocking_keys;        /* 客户端在等待的键 (BLPOP) */
    dict *ready_keys;           /* 接收到 push 的阻塞键 */
    dict *watched_keys;         /* WATCHED keys for MULTI/EXEC CAS */
    struct evictionPoolEntry *eviction_pool;    /* Eviction pool of keys */
    int id;                     /* Database ID */
    long long avg_ttl;          /* Average TTL, just for stats */
    } redisDb;


dict是dict.h文件中定义的结构体：

      typedef struct dict {
    	    dictType *type; // 类型特定函数  type 指向 操作字典增删改查的函数
    	    void *privdata;  // 私有数据  保存着不同类型需要传递给type函数的可选参数  说白了不同类型选择						不同的操作函数
    	    dictht ht[2];   // 保存两个hash表，ht[1]在扩容的时候会用到，是ht[0]的2倍
    	    int rehashidx;   // rehash 索引 当rehash不进行时为-1   
    	} dict;
    
    typedef struct dictht {
    	    dictEntry **table;   // hash数组，元素为指向dicEntry的指针
    	    unsigned long size;  // hash表的大小
    	    unsigned long sizemask;  // hash 表的掩码 size-1
    	    unsigned long used;     // hash表已使用的大小
    	} dictht;
    
    typedef struct dictEntry {
        void *key;     //键值
        union {    // 值
            void *val;
            uint64_t u64;
            int64_t s64;
        } v;
        struct dictEntry *next;  //指向hash冲突的下一个元素
    } dictEntry;	
redis的数据结构是reidsDB,redisDB中存储者键空间，过期键，redis数据库的id等数据。键空间中的内容有rehash索引，一大一小两个hash表等内容，hash表中存储hash数组，数组长度已使用大小等，hash数组中存储entry。

与jkd中hashMap有所不同的是，redis中hashMap扩容时，采用的时渐进式扩容，每次查询获更新时，判断rehash索引值是否维-1，若不是，则每次将查询获更新的键值对从ht[0]中搬迁到ht[1]中去，并减少ht[0]中used的值，直到used值为0时，ht[1]变为ht[0];

redis之所以不采用一次性拷贝，主要原因是当数据量较大时，这种拷贝就会比较耗时，这段时间redis就无法对外提供服务了。采用渐进式拷贝的方法虽然增加了复杂度，但提高了效率。

开始rehash后，当进行查找、更新、删除时会遍历ht[0]和ht[1];

redis中也是采用拉链的方法处理hash冲突的。







