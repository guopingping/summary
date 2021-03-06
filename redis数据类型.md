 #### 1. Redis是什么？ 
```
 		Remote Dictionary Server
 		被称为数据结构服务器。
 		完全开源、非关系型、高性能的key-value存储系统。
 		支持5中数据类型：存储string、list、set、zset和hash
```

#### 2.Redis的特点
```
	redis是单线程的，操作是安全的；
	redis支持数据的持久化，可将内存中的数据保持在磁盘中，重启的时候可以再次加载进行使用；
	redis支持key-value，并提供list、set、zset、hash等数据结构的存储；
	redis支持数据的备份，即master-slave模式的数据备份；
	redis单个value的最大限制1GB；
```
 		
#### 3.五种数据类型介绍及使用场景
```

应用场景：
    会话缓存；
    消息队列，比如支付；
    活动排行榜或计数；
    发布，订阅消息（消息通知）；
    商品列表，评论列表等；


	1) String 
				key-value，可以包含任何数据，一个键最大能存储512MB。
				比如图片或者序列化的对象。
			
			set：设置存储在指定键中的值；
			get：获取存储在指定键中的值；
			del：删除存储在指定键中的值；

	使用场景:
		incr 自增 ；eg：生成id；
		decr 减少；eg：库存；
		计数器缓存；
		缓存–过期时间设置，模拟session；
        微博数、粉丝数；

	使用案例：
	
	2） List
        redis列表，按照插入顺序可以添加一个元素到列表的头部或尾部。

        rpush：将给定值推入列表的右端；
        lrange：获取列表在指定范围上的所有值；
        lindex：获取列表在指定范围上的单个元素；

        使用场景：
            多任务调度队列；
            利用lrange命令，做基于redis的分页功能，性能极佳，用户体验好；
            微博发表文章，使关注的人都能看到（使用列表做一个消息队列）；
            生产者消费者模型（多线程）；

    3）Set
        string类型的无序集合。集合是通过哈希表实现的，增删查复杂度都是O(1)

        sadd：将给定元素添加到集合；
        smembers：返回集合包含的所有元素；
        sismember：检查指定元素是否存在于集合中；

        使用场景：
            微博关注数。
            利用交集、并集、差集等操作，可以计算共同爱好，全部的喜好，自己独有的喜好等功能。

    4）hash
        键值对集合。是string类型的field和value的映射表，适用于存储对象。

        hset：散列里面关联起指定的键值对；
        hget：获取指定散列键的值；
        hgetall：散列包含的所有键值对
        hdel：如果给定键存在于散列中，移出这个键；

        使用场景：
            购物车
            单点登录，用这种数据结构存储用户信息，一cookie作为key，设置30分钟为缓存过期时间，
            能很好地模拟类似session效果。

    5）zset
        集合，不允许重复的成员。每个元素都会关联一个double类型的分数。
        redis通过分数来为集合中成员进行从小到大的排序。
        zset的成员是唯一的，但分数却可以重复。

        zadd：将一个带有给定分值的成员添加到有序集合里面；
        zrange：根据元素在有序排列中所处的位置，从有序集合里面获取多个元素；
        zrangebyscore：获取有序集合在给定分值范围内的所有元素；
        zrem：如果指定成员存在于有序集合中，那么移出这个成员

        使用场景
            排行榜，取Top N操作；
            延时任务
            范围查找

```

#### 3.持久化
```
两种方式：

1）rdb快照：
    默认redis是会以快照的形式将数据持久化到磁盘（一个二进制文件，dump.rdb，这个文件名字可以指定），
    在配置文件（redis.conf)中的格式是：save
    N M表示在N秒之内，redis至少发生M次修改则redis抓快照到磁盘。

    保存 900 1：900秒内如果超过1个key被修改，则启动快照保存；
    保存300 10：300秒内如果超过10个key被修改，则启动快照保存；
    保存60 10000：60秒内如果超过10000个重点被修改，则启动快照保存；

2）aof仅附加文件
    使用aof持久时，服务将每个收到的写命令通过写函数追加到文件中（appendonly.aof)
    aof持久化存储方式参数说明：
        appendonly yes：开启aof持久化存储方式；
        appendfsync always：收到写命令后就立即写入磁盘，效率最差，效果最好；
        appendfsync everysec：每秒写入磁盘一次，效率与效果居中；
        appendfsync no：完全依赖操作系统，效果最佳，效果没法保证；

```

#### 4.redis性能、并发
```
性能：
    在碰到需要执行耗时特别久，且结果不频繁变动的sql，特别适合将运行结果放入魂村，
这样后面的请求就去缓存中读取，使得请求能够迅速响应。

并发：
    在大并发的情况下，所有的请求直接访问数据库，数据库会出现连接异常。
    这个时候，需要使用redis做一个缓冲操作，让请求先访问到redis，而不是直接访问数据库。

```

#### 5.优点
```
1）性能极高。
    redis能读的速度是110000次/s,写的速度是81000次/s；
2）丰富的数据类型。
    redis支持二进制案例的strings、lists、hashes、sets及ordered sets数据类型操作；
3）原子。
    redis的所有操作都是原子性的，意思是要么成功要么失败完全不执行。
    单个操作都是原子性的，多个操作也支持事务，即原子性，通过Multi和Exec指令包起来。
4）丰富的特性。
    可用于缓存，消息，redis支持publish、subscribe，通知，key过期等特性。
5）速度快。
    数据存在内存中，类似于HashMap、HashMap的优势就是查找和操作的时间复杂度都是O(1).
6）支持事务。
    操作都是原子性，所谓的原子性就是对数据的更改要么全部执行，要么全部不执行。


```

#### 6.缺点
```
1）缓存和数据库双写一致性问题
2）缓存雪崩问题
3）缓存击穿问题
4）缓存并发竞争问题

```

#### 7.单线程的redis为什么这么快？
```
redis是单线程工作模型
1）纯内存操作
2）单线程操作，避免了频繁的上下文切换
3）采用非阻塞的I/o多路复用机制
```

#### 8.redis的过期策略及内存淘汰机制
```
eg：redis只能存5G数据，可是写了10G，那会删除5G的数据。怎么删除？
    你的数据设置了过期时间，但是时间到了，内存占用率还是比较高，原因是什么？

    --redis：采用的是定期删除+惰性删除策略。

为什么不用定时删除策略？
    定时删除，用一个定时器来负责监视key，过期则自动删除。
    虽然内存即使释放，但是十分消耗CPU资源。
    在大并发情况下，CPU要将时间应用在处理请求，而不是删除key，因此没有用这一策略。

定期删除+惰性删除是如何工作的？
    定期删除，redis默认每个100ms检查，是否有过期的key，有则删除。
    需要说明的是，redis不是每个100ms将所有key检查一次，而是随机抽取检查。
    因此，如果只采用定期删除策略，会导致很多key到期时间没有删除。

    所以，惰性删除是在获取某个key的时候，redis会检查一遍，这个key如果设置了过期时间，那么
    是否过期了？如果过期了，此时就会删除。

采用定期删除+惰性删除就没有其他问题了吗？
    如果定期删除没有删除key，然后你也没及时请求key，也就是说惰性删除也没生效。
    这样，redis的内存会越来越高，那么就应该采用内存淘汰机制。

```

#### 9.redis和数据库双写一致性的问题
```
一致性问题是分布式常见问题，还可以再分为最终一致性和强一致性。
数据库和缓存双写，就必然会存在不一致的问题。
如果对数据有强一致性要求，不能放缓存。
我们所做的一切，只能保证最终一致性。另外，从根本来上说，只能说降低不一致发生的概率，无法完全避免。
因此，有强一致性的要求的数据，不能放缓存。

首先，采用正确更新策略，先更新数据库，再删除缓存，其次，因为可能存在删除缓存失败的问题，提供了一个补偿措施即可
如消息队列。

```

#### 10.如何应对缓存穿透和缓存雪崩问题
```
缓存穿透：即黑客故意去请求缓存中不存在的数据，导致所有的请求都怼到数据库上，从而数据库连接异常。
解决方案：
    1）利用互斥锁，缓存失效的时候，先去获得锁，得到锁了，再去请求数据库。没得到锁，则休眠一段时间重试；
    2）采用异步更新策略，无论key是否取到值，都直接返回。
        value值中维护一个缓存失效时间，缓存如果过期，异步起一个线程去读数据库，更新缓存。需做环迅预热。
    3）提供一个能迅速判断请求是否有效的拦截机制

缓存雪崩：即缓存同一时间大面积的失效，这个时候又来了一波请求，结果请求都怼到数据库上，从而导致数据库连接异常。
解决方案：
    1）给缓存的失效时间，加上一个随机值，避免集体失效；
    2）使用互斥锁，但是该方案吞吐量明显下降了；
    3）双缓存。
```
#### 11.如何解决redis的并发竞争key问题
```
即：同时有多个子系统去set一个key，需要注意什么？
1）如果对这个key操作，不要求顺序
    这种情况，准备一个分布式锁，大家去抢锁，抢到锁就做set操作即可，比较简单。
2）如果对这个key操作，要求顺序
    假设有一个key1，系统A需要将key1设置为value1，系统B需要将key1设置为valueB，系统C将key1设置为valueC，
    期望按照key1的value值按照valueA-->valueB-->valueC的顺序变化。这种时候我们在数据写入数据库的时候，需要保存一个
    时间戳，
        系统A key1 {valueA 3:00}
        系统B key1 {valueB 3:05}
        系统C key1 {valueC 3:10}
    那么，假设这会系统B先抢到锁，将key1设置为{valueB 3:05},接下来系统A抢到锁，发现自己的valueA的时间戳
    早于缓存时间戳，那就不做set操作。

    其他方法，比如利用队列，将set方法变成串行访问也可以。

```


